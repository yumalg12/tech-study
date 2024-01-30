## [React Hook] useState

useState는 컴포넌트에 상태 변수 (state variable)를 추가할 수 있는 React Hook이다. 여기서 상태 변수란 각 컴포넌트 별 메모리를 의미하는 '상태 (state)' 를 저장하기 위한 변수이다.

일반적으로 다음과 같은 형태로 선언한다.[1]

```javascript
const [state, setState] = useState(initialState);
```

<br>

useState는 렌더링 간에 어떠한 상태를 유지하기 위해 사용한다. 예를 들어, 다음과 같이 구현된 페이지네이션 코드는 작동하지 않는다.[2]

```javascript
  let page = 0;

  function handleClick() {
    page = page + 1;
  }
```

버튼 클릭 시 page 로컬 변수 값이 변하게 되어 있으나, 페이지가 변경되며 리렌더링이 발생할 때에는 지역 변수가 유지되지 않으므로 리액트는 변동된 로컬 변수를 사용해 컴포넌트를 새로 렌더링해야 한다는 것을 모른다.

다시 말해, 로컬 변수의 변화는 컴포넌트 렌더링을 트리거하지 못한다.

<br>

useState를 사용하면 다음과 같이 코드를 작성할 수 있다.

```javascript
import { useState } from 'react';

const [page, setPage] = useState(0);
function handleClick() {
  setPage(page + 1);
}
```

이때 컴포넌트의 생명 주기는 다음과 같다.

1. 컴포넌트가 `page` 변수의 초기값인 `0`을 이용해 렌더링된다. useState는 `[0, setIndex]` 를 리턴하며, React는 `0`을 최신 상태값으로 기억한다.
2. 사용자가 버튼을 눌러 `setPage(page + 1) = setPage(1)`을 호출해 상태 (`page` 변수)를 업데이트한다. 이제 React는 `page = 1`을 최신 상태값으로 기억하며 새로운 렌더링이 트리거된다.
3. 컴포넌트가 새로 렌더링된다. React에 아직 `useState(0)`이 저장되어 있지만, step 2에서 사용자가 `page = 1`로 변경했기 때문에 useState는 `[1, setIndex]`을 리턴한다.

<br>

### useState의 비동기 동작

`useState`의 상태 설정 함수 (setter)는 비동기적으로 동작한다. 이는 React가 성능을 최적화하기 위해 여러 상태 설정 호출을 한 번에 처리하기 때문이다.

상태 설정 함수를 호출하면, React는 상태 변화를 큐에 넣어 스케줄링하고, 이후에 일괄적으로 업데이트를 수행한다. 따라서 동일한 이벤트 루프에서 여러 번의 상태 업데이트를 효율적으로 처리할 수 있다.

`useState`의 상태 설정 함수의 비동기 동작을 통해 얻는 주요 이점은 다음과 같다:

1. **배치 업데이트:** 여러 상태 설정 함수 호출 (상태 변경)을 모아 한 번의 렌더링으로 처리하는 React의 업데이트 방식이다. 이는 불필요한 렌더링을 줄여 성능을 향상시킬 수 있다.

2. **최신 상태 반영:** 상태 설정 함수는 상태를 즉시 변경하지 않고, 변경을 예약한다. 그래서 여러 번 상태 설정 함수를 호출해도 최종적으로 한 번만 렌더링을 수행하며, 이때 최신 상태가 반영된다.

3. **컴포넌트 렌더링 최적화:** 상태 설정 함수가 비동기로 동작함으로써, React는 상태가 변경될 때마다 즉시 렌더링하는 대신 필요한 시점에만 렌더링을 수행하며 성능을 최적화할 수 있다.

<br>

이러한 특성으로 인해 상태 설정 함수 호출 직후에는 변경된 상태를 즉시 조회할 수 없다. 만약 상태 설정 함수 호출 후 즉시 업데이트된 상태를 필요로 한다면, `useEffect`를 이용하여 상태가 업데이트된 후의 동작을 정의할 수 있다.

```javascript
const [count, setCount] = useState(0);

useEffect(() => {
  console.log(count); // 상태 업데이트 후 "count" 출력
}, [count]);

setCount(1);
```

<br>

React 16.8 버전 이전의 개발 방식인 클래스형 컴포넌트에서 사용되는 `setState` 메서드의 경우 다음과 같이 setState의 두 번째 인자로 콜백 함수를 전달하여 사용할 수 있다.

이 콜백 함수는 상태 업데이트가 완료된 후에 실행되므로 콜백 내에서 this.state를 조회하면 setState로 설정한 최신 상태 값을 바로 확인할 수 있다.

```javascript
this.setState({ count: 1 }, () => {
  console.log(this.state.count); // "1" 출력
});
```

<br>
<br>

##
[1] https://react.dev/reference/react/useState<br>
[2] https://react.dev/learn/state-a-components-memory<br>
