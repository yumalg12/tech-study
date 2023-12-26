## Side Effect (부작용)

Side effect는 프로그래밍에서 중요한 개념이다.
컴퓨터 과학에서, 어떠한 함수가 결과값 이외에 다른 상태를 변경시킬 때 Side effect가 있다고 말한다.[1]

다음과 같이 표현할 수 있다.[2]
> 함수 내 특정 동작이 함수 외부에 영향을 끼쳐, 프로그램의 동작을 이해하기 어렵게 만드는 행위

따라서 Side effect를 최소화하면 코드를 예측 가능하고 유지보수가 쉬워지며, 버그를 줄일 수 있다.

그렇다면 Side effect를 지양해야 하는 것으로 보일 수 있으나, side effect는 흔히 사용되는 많은 동작에서 발생하고 있다.

- **서버와의 통신**: 사용자가 페이지에 접근했을 때 초기화 작업을 서버와 통신하여 처리하는 경우, 이는 네트워크 호출에 의한 side effect이다.
- **setTimeout, setInterval**: 시간 기반의 함수들은 예측이 어렵기 때문에 side effect를 일으키기 쉽다.
- **외부 라이브러리와 상호작용**: React.js와 함께 다른 라이브러리를 사용할 때, 그 라이브러리들이 DOM이나 브라우저 API와 상호작용하면 side effect가 발생할 수 있다.

이렇듯 side effect는 무조건 지양해야 하는 개념이 아닌, 사용에 주의가 필요한 내용으로 이해해야 한다.[1,2]

React에서는 위와 같은 상황에서 useEffect 훅을 사용하여 **컴포넌트의 렌더링이 완료된 후**에 특정 작업을 수행할 수 있다. useEffect를 올바르게 활용하면 Side effect를 효과적으로 관리하고 컴포넌트를 순수하게 유지하여 코드의 예측 가능성을 높일 수 있다. (더 알아보기: [React Hook] useEffect.md)

<br>

### 참조 투명성

Side effect와 관련하여 "참조 투명성 (Referential transparency)"이라는 개념이 있다. 참조 투명성이란 함수가 동일한 입력에 대해 항상 동일한 결과를 반환하는 특성을 말한다.
참조 투명성을 갖는 함수를 "순수 함수 (Pure Function)"이라고 하며, 순수 함수들은 외부 상태에 의존하지 않고 외부에 영향을 끼치지 않는다.[1]

참조 투명성은 다음과 같이 표현할 수 있다.[2]
> Same input will always return same output.

다음은 참조 투명성에 대한 React.js 컴포넌트의 예시이다.
```
const App({name}) {
  return (<div>{name}</div>);
};
```
위 App 컴포넌트는 name이라는 인자 (props)를 받고, div를 반환한다.

App 함수는 같은 입력에 대해 항상 같은 결과를 반환해 줄 것이다. 즉 외부와 전혀 관련이 없고, 함수 외부에 영향을 주지 않는다. 그러므로 여기서의 App 함수는 순수함수(pure function)의 조건을 만족한다.

반대로 어떠한 함수가 같은 입력임에도 다른 결과를 내거나 함수 외부에 영향을 미치게 될 때 side effect가 있다고 하며, 이러한 함수들을 참조에 불투명(referentially opaque)하다고 한다.

React.js는 컴포넌트가 최대한 순수 함수를 유지할 것을 권장하고 있으며, 실제로 그렇게 구현해야 컴포넌트 재사용성이 증가하고 예측 및 테스트를 쉽게 할 수 있다.[2,3]

<br>
<br>

##
[1] https://ko.wikipedia.org/wiki/%EB%B6%80%EC%9E%91%EC%9A%A9_(%EC%BB%B4%ED%93%A8%ED%84%B0_%EA%B3%BC%ED%95%99)<br>
[2] https://velog.io/@sucream/%EA%B7%B8%EB%9E%98%EC%84%9C-useEffect%EB%8A%94-%EC%96%B8%EC%A0%9C-%EC%93%B0%EB%8A%94%EA%B1%B4%EB%8D%B0%EC%9A%94<br>
[3] https://ko.react.dev/learn/keeping-components-pure#side-effects-unintended-consequences<br>
