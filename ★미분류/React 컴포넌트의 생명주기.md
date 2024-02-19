## React 컴포넌트의 생명주기

React 컴포넌트의 생명주기 (Lifecycle)는 컴포넌트가 생성되어 화면에 렌더링되고, 업데이트되며 재렌더링되고, 최종적으로 화면에서 사라질 때까지의 과정을 의미한다.

단, 이는 클래스형 컴포넌트에 적용되는 개념이다. 함수형 컴포넌트에는 React Hooks를 통해 생명주기와 관련한 작업을 수행할 수 있다.
예를 들어, useEffect 훅을 이용해 side effects를 수행시킴으로써 컴포넌트가 마운트될 때, 업데이트될 때, 언마운트될 때 등과 같은 특정 시점에 특정 작업을 수행할 수 있다.

<br>

생명주기는 여러 단계로 나뉘며, 각 단계에서 특정 메서드가 호출된다. 이러한 메서드들을 생명주기 메서드(Lifecycle methods)라고 한다.

컴포넌트의 생명주기는 크게 3가지 단계로 나눌 수 있다.

1. **마운트(Mounting):** 컴포넌트 인스턴스가 생성되어 DOM에 삽입되는 단계. 이 단계에서는 `constructor`, `static getDerivedStateFromProps`, `render`, `componentDidMount` 메서드가 차례대로 호출된다.

2. **업데이트(Updating):** 컴포넌트가 재렌더링되는 단계. 이는 props 또는 state의 변경으로 인해 발생합니다. 이 단계에서는 `static getDerivedStateFromProps`, `shouldComponentUpdate`, `render`, `getSnapshotBeforeUpdate`, `componentDidUpdate` 메서드가 차례대로 호출된다.

3. **언마운트(Unmounting):** 컴포넌트가 DOM에서 제거되는 단계. 이 단계에서는 `componentWillUnmount` 메서드가 호출된다.

이외에도 오류 처리를 위한 단계가 별도로 있으며, 이 때는 `static getDerivedStateFromError`와 `componentDidCatch` 메서드가 호출된다.

<br>

함수형 컴포넌트에서는 React Hooks를 사용하여 함수형 컴포넌트에서 생명주기와 비슷한 작업을 구현할 수 있다.

1. **useState**: 컴포넌트의 상태를 추가하고 관리한다. 초기 상태 값을 설정하고, 그 상태를 업데이트하는 함수를 제공한다.
2. **useEffect**: 부수 효과 (side effects)를 수행하거나 생명주기와 유사한 작업을 수행한다. 컴포넌트가 렌더링될 때마다 특정 코드를 실행하거나, 특정 상태나 프로퍼티가 변경될 때마다 실행되는 작업 등이 가능하다.
3. **useRef**: DOM 요소나 다른 값을 저장하고 관리한다. 주로 DOM 요소에 접근하는 경우나 이전 값과 새로운 값을 비교하는 경우에 사용된다.
4. **useContext**: Context를 사용하여 상태를 공유하고 필요한 값에 접근한다. Context Provider로부터 가장 가까운 값을 읽어올 수 있다.
5. **useReducer**: 복잡한 상태 로직을 관리할 때 사용된다. 클래스 컴포넌트에서의 reducer와 유사한 기능을 제공한다.
6. **useCallback**: 함수를 캐싱하여 불필요한 렌더링을 방지한다. 동일한 함수를 재사용하여 불필요한 메모리 사용을 줄일 수 있다.
7. **useMemo**: 계산 비용이 많이 드는 연산의 결과를 캐싱하여 불필요한 계산을 방지한다. 함수의 반환값을 기억하여 동일한 입력이 주어질 때 이전의 결과를 재사용한다.
8. **useLayoutEffect**: 브라우저에 렌더링된 후 DOM 요소에 직접적으로 접근할 때 사용된다. useEffect와 비슷하지만, 렌더링 전에 실행된다.
9. **useImperativeHandle**: 부모 컴포넌트에서 자식 컴포넌트의 인스턴스에 접근할 때 사용된다. 부모 컴포넌트에게 자식 컴포넌트의 메서드나 값을 제공할 수 있다.


##
https://react.dev/learn/lifecycle-of-reactive-effects
