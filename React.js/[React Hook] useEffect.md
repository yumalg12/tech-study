## useEffect

useEffect는 React 함수형 컴포넌트에서 비동기 동작을 다루거나 side effect를 발생시키고 사용하기 위한 Hook이다.[1]

이를 통해 외부 시스템*과의 동기화, 데이터 가져오기, 구독 설정, 수동 DOM 조작, 타이머 설정 및 제거, 이벤트 리스너 등과 같은 작업을 수행할 수 있다.
```
*외부 시스템 (external): 페이지에 표시되는 동안 네트워크나 브라우저 API, 또는 서드파티 라이브러리와의 연결이 유지되어야 하는 컴포넌트 등, React에 의해 제어되지 않는 시스템들의 통칭
```

컴포넌트를 외부 시스템과 연결하려면 컴포넌트의 최상위 레벨에서 useEffect를 호출해야 한다.

<br>

### 핵심 구성 요소
useEffect Hook은 2개의 인수를 사용한다.
```
useEffect(setup, dependencies?)
```

#### 1. setup 매개변수
Side effect를 정의하는 함수이다. 컴포넌트가 렌더링될 때마다 실행되며, 컴포넌트가 DOM에 추가된 후에 실행된다.

setup에서는 부수 effect의 정리 작업을 담당하는 clean up 함수를 반환할 수 있으며, clean up 함수를 반환하는 것이 권장된다.
이를 통해 컴포넌트의 메모리 누수를 방지하고 예기치 않은 동작을 최소화할 수 있다.
이 정리 함수는 컴포넌트가 DOM에서 제거되기 직전 또는 의존성 변화로 인해 컴포넌트가 업데이트(리렌더링)되기 직전에 실행된다.
```
useEffect(() => {
  //  외부 시스템과의 연결, 구독 설정, 이벤트 리스너 등의 Side effect

  return () => {
    // clean up 작업 수행
    // 예를 들어, 외부 리소스 구독 해제 또는 설정 해제 등
  };
}, [/* dependencies */]);
```

Clean up 함수를 반환하지 않는 경우 useEffect의 반환값은 undefined이다.

<br>

#### 2. dependency 매개변수 (선택사항)
setup 함수 내에서 사용하는 (의존하는) 컴포넌트의 상태나 변수들을 담는 배열이다.
이 의존성 배열은 setup 함수 내에서 참조된 props, state, 컴포넌트 내에서 새로 선언된 함수 등을 포함한다.

useEffect는 의존성 배열의 각 항목을 Object.is 메서드**를 사용해 이전 값과 비교한다. 
```
**Object.is 메서드의 사용 예
console.log(Object.is(0, -0)); // false
console.log(Object.is(NaN, NaN)); // true
```
의존성 배열 내의 값 중 하나라도 변경되면 effect를 다시 실행한다. 

따라서 의존성 배열을 생략하면 useEffect는 컴포넌트가 렌더링될 때마다 매번 실행된다. 반면 의존성을 명시하면 해당 값이 변경될 때에만 effect가 실행된다.


예를 들어, 아래 코드에서 의존성 배열이 `[count]`로 설정되었다면, count 값이 변경될 때마다 useEffect 내의 effect 함수가 실행된다.
```
useEffect(() => {
  // 특정 effect 설정
}, [count]); // count 값이 변경될 때만 effect가 실행됨
```

이때 의존성이 객체이거나 컴포넌트 내부에 선언된 함수일 때는 주의가 필요하다.

React에서는 의존성 추적을 위해 '얕은 비교'를 수행해 객체나 배열 등의 참조형 데이터의 변경 여부를 확인한다.
객체와 컴포넌트 내부에 선언된 함수는 매 렌더링마다 새로운 참조가 생성되므로, 값이 변하지 않았더라도 의존성이 변경된 것으로 간주되어 useEffect의 불필요한 재실행이 발생할 수 있다.

따라서, setup 함수 내부에서 외부 의존성을 가져와서 객체나 함수를 선언하는 것이 좋다.
```
const serverUrl = 'https://localhost:1234';

function ChatRoom({ roomId }) {
  const [message, setMessage] = useState('');

  useEffect(() => {
    const options = { // options 객체는 외부의 serverUrl과 roomID를 가져와 useEffect 내부에서 선언되었다.
      serverUrl: serverUrl,
      roomId: roomId
    };
    const connection = createConnection(options);
    connection.connect();
    return () => connection.disconnect();
  }, [roomId]);
  // ...
```

반대로 정적 객체와 함수를 컴포넌트 외부로 이동시킬 수도 있다. 이렇게 되면 불필요한 의존성을 제거할 수 있다.
```
const options = {
  serverUrl: 'https://localhost:1234',
  roomId: 'music'
};

function ChatRoom() {
  const [message, setMessage] = useState('');

  useEffect(() => {
    const connection = createConnection(options);
    connection.connect();
    return () => connection.disconnect();
  }, []); // ✅ All dependencies declared
  // ...
```

<br>

### useEffect의 동작

useEffect는 함수형 컴포넌트의 최상위 레벨 또는 커스텀 Hook에서만 호출해야 한다. 다시 말해, 반복문이나 조건문 안에서는 호출할 수 없다.

Effect는 컴포넌트가 화면에 추가, 업데이트, 제거될 때 특정 동작을 수행한다. React는 설정 함수와 정리 함수가 필요할 때마다 useEffect를 여러 번 호출할 수 있다.

useEffect는 다음과 같은 절차로 동작한다.

1. React는 컴포넌트가 렌더링될 때 (마운트 시) useEffect의 setup 함수를 실행한다.
2. 해당 함수 안에서 외부 리소스를 구독하거나 설정하는 등 메모리를 사용하는 작업을 하게 되면, React는 이러한 작업들이 컴포넌트의 생명 주기 동안 계속 유지되어 메모리 누수를 일으킬 수 있다는 것을 인지하고, 이에 대한 정리(clean up) 작업을 수행해야 함을 파악한다.
3. 이때 React는 해당 effect가 종료되기 전, 자동으로 생성된 정리 함수를 만들어냅니다. 만일 정리 함수가 명시적으로 제공되지 않았더라도 React는 이를 대신 생성한다. 
4. 의존성이 변경된 컴포넌트가 리렌더링 될 때마다 아래 동작을 수행한다.
    - 먼저 clean up 코드가 오래된 props 및 state와 함께 실행된다.
    - 이후 setup 코드가 새로운 props 및 state와 함께 실행된다.
5. 컴포넌트가 화면에서 제거된 이후에 (마운트 해제 시) clean up 코드가 마지막으로 실행된다.

useEffect는 브라우저의 DOM과 상호작용하기 때문에 클라이언트 환경에서만 동작한다.
초기 서버 사이드 렌더링 과정에서 생성한 HTML이 클라이언트로 전달되어 렌더링된 이후에만 실행된다.

클라이언트에서의 페이지 렌더링 후 useEffect가 실행되면서 추가적인 데이터 요청이 발생한다.

따라서 useEffect를 초기 페이지를 위한 데이터 요청에 사용하는 것은 적합하지 않다.
초기 페이지는 서버 렌더링 시점에 작성되며, 이 때는 useEffect 훅이 실행되지 않는 시점이기 때문이다.

<br>

### useEffect를 이용한 데이터 페칭 

컴포넌트에 외부 데이터를 불러오기 위해 useEffect를 사용할 수 있다.

```
import { useState, useEffect } from 'react';
import { fetchBio } from './api.js';

export default function Page() {
  const [person, setPerson] = useState('Alice');
  const [bio, setBio] = useState(null);
  useEffect(() => {
    async function startFetching() {
      setBio(null);
      const result = await fetchBio(person);
      if (!ignore) {
        setBio(result);
      }
    }

    let ignore = false;
    startFetching();
    return () => {
      ignore = true;
    }
  }, [person]);

  return (
    <>
      <select value={person} onChange={e => {
        setPerson(e.target.value);
      }}>
        <option value="Alice">Alice</option>
        <option value="Bob">Bob</option>
        <option value="Taylor">Taylor</option>
      </select>
      <hr />
      <p><i>{bio ?? 'Loading...'}</i></p>
    </>
  );
}
```
ignore 변수는 처음에는 false로 설정되어 있고, 정리 함수가 실행되는 도중에 true로 변경된다.
이러한 로직은 '경쟁 상태 (race conditions)***'를 방지하기 위함이다.
```
***경쟁 상태 (race conditions): 네트워크 요청을 보내고 그에 대한 응답을 받는 순서가 서로 다를 수 있는 상황
```
async/await 구문을 사용하면 비동기 작업을 순차적으로 처리할 수 있어서 '경쟁 상태'와 같은 문제를 방지할 수 있다.
async 키워드를 함수 앞에 사용하여 해당 함수가 비동기적으로 동작한다는 것을 명시하고, await 키워드를 사용하여 비동기 작업이 완료될 때까지 기다리는 동기적인 코드 스타일로 작성하는 것이다.
이렇게 하면 코드의 가독성과 유지보수성이 향상된다.

<br>

그러나, 데이터 fetch 로직을 useEffect 내부에 직접 작성하는 것은 최적화와 관련된 기능을 추가하기 어려울 수 있다.

이러한 접근 방식의 단점은 다음과 같다.

- **서버에서 실행되지 않음**: useEffect는 서버에서 실행되지 않는다. 초기 서버 렌더링된 HTML은 데이터가 없는 상태만을 가지고 있다. 클라이언트는 자바스크립트를 다운로드하고 앱을 렌더링한 후 데이터를 로드한다. 이로 인해 초기 로딩이 느릴 수 있다.

- **네트워크 폭포 effect 생성**: Effect 내부에서 직접 페칭하는 것은 네트워크 폭포 effect를 발생시킬 수 있다. 부모 컴포넌트가 렌더링된 후에 데이터를 가져오고, 그 후 자식 컴포넌트가 렌더링되어 자체 데이터를 가져오는 경우, 데이터를 병렬로 가져오는 것보다 훨씬 느릴 수 있다.

- **데이터를 미리 로드하지 않음**: Effect 내부에서 직접 데이터를 페칭하는 것은 일반적으로 데이터를 미리 로드하거나 캐싱하지 않는다. 컴포넌트가 마운트 해제되고 다시 마운트될 때마다 데이터를 다시 가져와야 한다.

- **불편한 사용성**: 직접 데이터를 페칭하는 것은 버그를 발생시키지 않도록 하는데 많은 보일러 플레이트 코드****를 필요로 할 수 있다.
```
****보일러플레이트 코드 (Boilerplate code)': 개발 프로젝트에서 반복적으로 발생하지만 핵심 기능과는 직접적으로 관련이 없는 무의미한 코드 또는 템플릿. 주로 프로젝트의 초기 설정, 공통된 구조, 환경 설정을 위한 코드를 말한다.
```

따라서, React 공식 문서에서는 프레임워크에 내장된 데이터 페칭 메커니즘을 활용하거나 React Query, useSWR, React Router 6.4+와 같은 인기 있는 라이브러리나 클라이언트 측 캐시를 활용하여 데이터를 관리하는 것을 권장한다.

<br>

### Effect에서 이전 state를 기반으로 state 업데이트하기 

useEffect에서 불필요한 의존성을 제거하면 코드의 실행 효율성을 높일 수 있다.

예를 들어, Effect에서 기존 state의 값으로부터 새로운 값을 계산해 state를 업데이트할 때 문제가 발생할 수 있다.

```
function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const intervalId = setInterval(() => {
      setCount(count + 1); // count를 초당 1씩 늘리고자 한다.
    }, 1000)
    return () => clearInterval(intervalId);
  }, [count]); // 🚩 그러나 count는 1이 증가했을 때 0으로 초기화된다.
  // ...
}
```
count는 반응형 값이므로 반드시 의존성 배열에 추가해야만 한다.
그러나 count 값의 변화는 useEffect 훅의 실행을 트리거한다. useEffect 실행 시점에 count는 초기값인 0으로 초기화된다. 따라서 count는 영원히 1로 고정된 것처럼 보인다.

다음 코드와 같이, state를 변경하는 함수를 추가해 위 문제를 해결할 수 있다.

```
export default function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const intervalId = setInterval(() => {
      setCount(c => c + 1); // ✅ 이전 count 값을 사용하여 1씩 증가시키는 함수형 업데이트 패턴 적용
    }, 1000);
    return () => clearInterval(intervalId);
  }, []); // ✅ 이제 count는 더 이상 의존성이 아님

  return <h1>{count}</h1>;
}
```
익명 함수 `c => c + 1`을 `count + 1` 대신 전달하고 있으므로, Effect는 더 이상 count에 의존하지 않는다.
따라서 count가 변경될 때마다 Effect가 clean up 및 setup을 다시 실행할 필요가 없게 된다.

<br>

이와 같이 React에서 useState 훅으로 상태를 업데이트할 때 **함수형 업데이트 패턴**을 사용할 수 있다.
함수형 업데이트를 사용하면 이전 상태 값을 기반으로 새로운 상태 값을 업데이트하는 함수를 전달할 수 있다.
이는 비동기 상태 업데이트나 이전 상태를 기반으로 새로운 상태를 계산해야 하는 경우에 유용하다.

`setCount(c => c + 1)`에서는 이전의 count 값이 매개변수로 입력된다. 따라서 항상 현재 count 값을 기반으로 업데이트를 수행하게 된다.
반면, `setCount(count + 1)`은 setCount가 호출되는 시점의 현재 count 값을 기반으로 업데이트를 수행한다.
count가 setup 함수 내에 있으므로 의존성 배열에 포함되기 때문에 count 값 업데이트가 발생하는 시점에서 재렌더링이 발생하므로 '현재 count 값' 은 계속 0이다. 따라서 count 값은 영원히 1이 되는 것이다.

<br>
<br>

##
[1] https://ko.react.dev/reference/react/useEffect
