## React Hook

React Hook은 React에서 제공하는 함수 모음으로, 함수형 컴포넌트의 생명 주기를 관리하고 상태를 다루는 등 다양한 React 기능을 사용하기 위한 도구이다.

React Hook은 2015년에 발표된 React 16.8 버전부터 추가되었으며, 함수형 프로그래밍 개념에 기반을 두고 있다.
따라서, 함수형 프로그래밍의 장점을 활용하여 컴포넌트를 작성하고 관리하는 데 도움을 줄 수 있다. ('클래스형 컴포넌트와 함수형 컴포넌트의 차이' 문서 참조)

각 Hook은 특정 목적에 맞게 설계되었으며, 다양한 종류가 있다.

다음은 React가 제공하는 Hook의 종류와 간략한 설명이다.[1]

### 1. State Hook
State Hook은 컴포넌트가 사용자 입력과 같은 정보를 기억하게 만드는 기능을 담당한다.
- `useState`: 상태를 추가하고 관리하는 데 사용된다.
- `useReducer`: 복잡한 상태 로직을 처리하는 데 사용되며, 감소기 함수*를 포함한 상태 변수를 선언한다.
```
*감소기 함수 (reducer function): 두 개의 인자를 받아 하나의 결과를 반환하는 함수. 두 개의 인자 중 하나는 '현재 상태', 다른 하나는 '액션'이다.
'액션'은 어떤 변화를 일으킬지 나타내는 객체로, 주로 type에 대한 필드를 가진다. 이 액션 객체를 기반으로, 감소기 함수는 현재 상태를 다음 상태로 변환하는 로직을 수행한다.

function counterReducer(state, action) {
  switch (action.type) {
    case 'INCREMENT':
      return {count: state.count + 1};
    case 'DECREMENT':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}
```

### 2. Context Hook
Context Hook을 통해 컴포넌트는 멀리 떨어진 부모로부터 정보를 prop으로 전달받지 않고도 정보를 받을 수 있다.
- `useContext`: 컴포넌트 간 데이터를 전달하는 데 사용되며, Context를 활용해 정보를 prop으로 전달받지 않아도 된다.

### 3. Ref Hook
Ref Hook은 컴포넌트가 DOM 노드나 타임아웃 ID와 같은 렌더링에 사용되지 않는 정보를 보유할 수 있게 한다.
ref는 state와는 달리 업데이트해도 컴포넌트가 다시 렌더링되지 않는다.
- `useRef`: 참조를 선언한다. 값을 담을 수 있으며, 대부분 DOM 노드를 담는 데 사용된다.

### 4. Effect Hook
Effect Hook은 컴포넌트가 외부 시스템에 연결하고 동기화할 수 있게 한다. 이는 네트워크, 브라우저 DOM, 애니메이션, 다른 UI 라이브러리를 사용하여 작성된 위젯 및 기타 비 React 코드를 처리하는 것을 포함한다.
- `useEffect`: 외부 시스템에 연결하여 동기화하거나 컴포넌트의 라이프사이클을 관리하는 데 사용된다.

### 5. Performance Hook
Performance Hook은 재렌더링 성능을 최적화하는 데 사용된다.
- `useMemo`: 불필요한 재렌더링을 방지하거나 계산을 캐시하는 데 사용된다.
- `useCallback`: 함수를 캐시하여 최적화된 함수를 전달하는 데 사용된다.

### 6. Resource Hook
Resource Hook은 컴포넌트가 리소스를 상태의 일부로 보유하지 않고도 리소스에 액세스할 수 있게 한다.

- `use`: Promise나 context등, 리소스에서 값을 읽어들이기 위해 사용된다.

### 7. 기타 Hook
이 Hook은 주로 라이브러리 작성자에게 유용하며 애플리케이션 코드에서 일반적으로 사용되지는 않는다.

- useDebugValue: 사용자 정의 Hook에 대해 React 개발자 도구가 표시하는 레이블을 사용자 정의할 수 있다.
- useId: 컴포넌트가 고유 ID를 자신과 연관시킬 수 있게 한다. 일반적으로 접근성 API와 함께 사용된다.
- useSyncExternalStore: 컴포넌트가 외부 저장소에 구독할 수 있게 한다.

### 8. Custom Hooks
JavaScript 함수로 사용자 정의 Hook을 정의한 것이다.
개발자가 필요에 따라 직접 작성하여 재사용 가능한 Hook을 만들 수 있다.

<br>
<br>

##
[1] https://react.dev/reference/react/hooks

