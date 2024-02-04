## Redux

Redux는 전역변수 상태관리 라이브러리 중 하나로, '자바스크립트 앱을 위한 예측 가능한 상태 컨테이너' 라고 소개하고 있다.

<br>

### 전역변수 상태관리의 이해

전역변수 상태관리란, 여러 컴포넌트에서 참조하는 데이터를 컴포넌트 바깥에 저장해 두는 것이다.  
전역변수를 사용하지 않는다면 상위 컴포넌트에서 데이터를 불러온 다음 매개변수로 하위 컴포넌트에 전달해 주어야 한다.  
만일 어떤 컴포넌트의 하위 컴포넌트에 또 하위 컴포넌트가 있는 3depth 구조인데, 1depth의 최상위 컴포넌트와 3depth의 최하위 컴포넌트가 같은 상태를 사용해야 한다면?  
해당 상태를 사용할 필요가 없는 2depth의 중간 컴포넌트의 매개변수로 필요한 상태를 전달한 다음 또다시 2depth에서 3depth로 매개변수를 전달해 주어야 한다.

이것이 비효율적이기 때문에 전역변수 상태관리 라이브러리를 사용하게 된다.
상태관리 라이브러리에는 Redux, Context API, Recoil 등이 있다.

Redux 공식문서에서는 다음과 같은 상황에 Redux를 사용하는 것이 좋다고 말한다.

-   많은 양의 애플리케이션 상태가 앱의 여러 위치에 필요할 때
-   앱 상태가 시간이 지남에 따라 자주 업데이트될 때
-   어떤 상태를 업데이트하는 논리가 복잡할 때
-   앱에 중간 규모 이상의 코드베이스가 있으며 많은 사람들과 협업이 필요할 때

<br>

### Redux 설치

Redux는 그냥 Redux (Redux 코어 라이브러리) 가 있고, Redux toolkit이 있다.

Redux Toolkit은 더 간편하고 효율적인 방법으로 Redux 코드를 작성할 수 있도록 도와주는 라이브러리이다.

```javascript
# NPM
npm install @reduxjs/toolkit

# Yarn
yarn add @reduxjs/toolkit
```

또한 React.js 프로젝트라면, Create React App를 위한 공식 Redux+JS 템플릿을 사용할 수 있다. 이를 통해 Redux Toolkit와 React Redux가 React 컴포넌트와 통합되는 이점을 누릴 수 있다.

```javascript
npx create-react-app my-app --template redux
```

<br>

### Redux 개요

먼저 전체 내용을 요약하자면 다음과 같다.

**1\. Redux는 전역 애플리케이션 상태를 관리하기 위한 라이브러리이다.**

-   Redux는 일반적으로 Redux와 React를 함께 통합하기 위해 React-Redux 라이브러리와 함께 사용한다.
-   Redux Toolkit은 Redux 로직을 작성하는 데 권장되는 방법이다.

**2\. Redux는 "단방향 데이터 흐름" 앱 구조를 사용한다.**

-   State는 특정 시점의 앱 상태를 설명하고 해당 State를 기반으로 UI (React component)가 렌더링된다.
-   앱에서 어떤 동작이 발생하면:
    1.  UI가 action을 전달 (dispatch) 한다.
    2.  store는 reducer를 실행하고, 발생한 상황에 따라 state가 업데이트된다.
    3.  store는 상태가 변경되었음을 UI에 알린다.
-   새로운 state를 기반으로 UI가 다시 렌더링된다.

**3\. Redux는 다음 유형의 코드를 사용한다.**

-   Action: 액션은 'type' 필드가 있는 일반 개체 (plain object) 이며, 앱에서 어떤 동작이 발생했는지 설명한다.
-   Reducer: 리듀서는 이전 state + action을 기반으로 새로운 state 값을 계산하는 함수이다.
-   Redux store: 스토어는 액션이 ​​전달 (dispatch) 될 때마다 root reducer를 실행한다.

<br>

### Redux의 핵심 컨셉

Redux는 앱의 구성 요소를 다음 3가지로 분류한다.

-   **State:** 앱을 구동하기 위한 정보의 원천
-   **View:** 현재 상태를 바탕으로 선언된 UI 표현
-   **Action:** 사용자 입력과 같이 상태를 업데이트하는 트리거에 의해 앱에서 발생하는 이벤트

Redux는 '단방향 이벤트 흐름 (one-way data flow)' 을 원칙으로 한다.

![image](https://github.com/yumalg12/tech-study/assets/134472216/654df43a-3823-425b-9024-169a906c8817)

데이터 업데이트에 대한 다음과 같은 절차가 '단방향 이벤트 흐름' 이다.

-   state가 특정 시점의 상태를 나타낸다.
-   UI는 해당 상태를 기반으로 렌더링된다.
-   어떤 일이 발생하면 (ex. 사용자의 버튼 클릭) 발생한 일에 따라 상태가 업데이트된다.
-   새로운 state에 따라 UI가 다시 렌더링된다.

React에서는 여러 컴포넌트 간에 상태를 공유해야 하는 경우, "lifting state up" 패턴을 사용하여 상태를 부모 컴포넌트로 올릴 수 있다. 그러나 어떤 프로젝트에서는 이 패턴이 복잡성을 증가시킬 수 있다.  
특히 컴포넌트의 위치가 많이 다르다면, 상태 공유를 위해 컴포넌트 트리를 타고 올라가는 것이 충분치 않을 수 있다.  
이에 Redux는 React에서의 "lifting state up" 패턴을 보완하고 복잡성을 해결하기 위한 도구로 사용할 수 있다.

Redux는 공통 상태를 컴포넌트에서 분리하여 컴포넌트 트리 외부에 중앙집중적으로 위치시킨다. 이렇게 하면 컴포넌트 트리는 하나의 큰 "뷰(View)"로 구성되며, 어떤 위치에 있든지 state에 액세스하거나 action을 트리거할 수 있게 된다.

결과적으로 Redux는 애플리케이션의 전역 상태를 하나의 중앙 집중된 장소에 유지하고, 이 상태를 업데이트하는 데 일관된 규칙을 제공하여 코드를 예측 가능하게 만들어 준다.

<br>

### Redux 용어 설명

Redux에서는 다음과 같은 용어가 사용된다.

#### 1\. Action

Action은 'type' 이라는 필드를 갖는 일반 자바스크립트 개체 (plain object) 로, 애플리케이션에서 발생한 동작을 설명하는 이벤트라고 볼 수 있다.  
type은 "domain/eventName" 과 같은 형식으로 작성하는데, 다음과 같이 이벤트가 속해 있는 범주 (domain) 및 발생한 이벤트를 이름만 보고 알 수 있게끔 직관적으로 작성하는 것이 좋다.  
만일 이벤트에 대한 추가 정보 제공이 필요하다면 관례적으로 'payload' 필드에 작성한다.

```javascript
const addTodoAction = {
  type: 'todos/todoAdded',
  payload: 'Buy milk'
}
```

액션은 다음과 같이 '액션 생성자 (action creator)' 를 이용해 선언한다.

```javascript
const addTodo = text => {
  return {
    type: 'todos/todoAdded',
    payload: text
  }
}
```

#### 2\. Reducer

리듀서는 이전 state와 action을 받아 새로운 state 값을 (필요하다면) 리턴하는 함수이다. 일반적인 형태는 '(state, action) => newState' 이다.  
리듀서는 수신된 action (이벤트)의 type을 기반으로 이벤트를 처리하는 이벤트 리스너로 간주할 수 있다.

리듀서는 필수적으로 다음 조건을 만족해야만 한다.

-   받은 state와 action 인수를 이용해 새로운 state 값만을 리턴한다.
-   기존 state를 변경하는 것은 허용되지 않는다. 변경이 필요하다면 기존 state를 복사하여 값을 변경하는 방식만이 허용된다.
-   비동기 로직을 수행하거나, 랜덤 값을 사용하거나, 기타 "side effect"를 일으키지 않아야 한다.

두 번째 조건은 Redux가 기본적으로 '모든 값이 불변성 (Immutability) 을 가질 것으로 기대' 하기 때문이다.

리듀서 함수는 일반적으로 다음과 동일한 일련의 내부 논리 단계를 따른다.

1.  현재 액션이 해당 리듀서에 영향을 미치는지 확인한다.
2.  만약 그렇다면, 현재 상태의 복사본을 만들고, 이를 새로운 값으로 업데이트한 후 반환한다.
3.  그렇지 않다면, 현재 상태를 변경하지 않고 그대로 반환한다.

리듀서는 다음과 같이 조건문이나 반복문을 활용해 내부 로직을 구성할 수 있다.

```javascript
const initialState = { value: 0 }

function counterReducer(state = initialState, action) {
  // Check to see if the reducer cares about this action
  if (action.type === 'counter/increment') {
    // If so, make a copy of `state`
    return {
      ...state,
      // and update the copy with the new value
      value: state.value + 1
    }
  }
  // otherwise return the existing state unchanged
  return state
}
```

#### 3\. Store

Redux 애플리케이션이 갖는 현재 상태는 'store' 라 불리는 개체에 저장된다.  
다음과 같이, configureStore 함수를 사용해 Redux store를 생성한다.  

```javascript
import { configureStore } from '@reduxjs/toolkit'

const store = configureStore({ reducer: counterReducer })

console.log(store.getState())
// {value: 0}
```

구성 객체에 리듀서를 포함시켜 전달할 수 있는데, 리듀서를 전달함으로써 store가 특정 상태 변화에 대한 로직을 알 수 있게 된다.  
현재 상태는 getState 메서드를 통해 접근할 수 있다.

#### 4\. Dispatch

store는 dispatch라는 메서드를 갖는다. state를 업데이트하는 유일한 방법은 store.dispatch()를 호출하고 action 객체를 전달하는 것이다.  
그러면 store는 reducer 함수를 실행하여 새 상태 값을 저장하고, getState()를 호출하여 업데이트된 값을 확인할 수 있다.

```javascript
store.dispatch({ type: 'counter/increment' })

console.log(store.getState())
// {value: 1}
```

dispatch 액션을 애플리케이션에서 '이벤트 트리거' 로 간주할 수 있다. 어떠한 작업이 발생하면, store에 전달된 reducer가 이벤트 리스너처럼 작동해 store가 해당 이벤트를 인지하게 된다. 실행된 동작이 reducer 함수의 실행 조건에 알맞다면, 그에 대한 응답으로 상태 업데이트가 발생한다.

보통 올바른 action을 전달 (dispatch)하기 위해 액션 생성자를 호출하여 사용한다.

```javascript
const increment = () => {
  return {
    type: 'counter/increment'
  }
}

store.dispatch(increment())

console.log(store.getState())
// {value: 2}
```

#### 5\. Selector

Selector는 store의 상태 값에서 특정 정보를 추출하기 위한 함수이다.

```javascript
const selectCounterValue = state => state.value

const currentValue = selectCounterValue(store.getState())
console.log(currentValue)
// 2
```

<br>

### Redux의 작동 단계

Redux의 핵심 컨셉 파트에서 데이터 업데이트에 대한 ' 단방향 데이터 흐름 ' 절차에 대해 서술했다.  
Redux에서는 해당 단계를 보다 자세히 나눌 수 있다. 

-   초기 설정:
    -   루트 리듀서 함수\*를 사용해 Redux store가 생성된다.  
        _(루트 리듀서 함수: Redux 애플리케이션에서 사용되는 여러 리듀서들을 통합하는 역할을 하는 리듀서. Redux는 단일 리듀서만을 허용하므로, 여러 개의 리듀서를 하나로 합치기 위해 root reducer가 사용된다.)_
    -   store는 루트 리듀서를 한 번 호출하고 반환 값을 초기 state 값으로 저장한다.
    -   UI가 처음 렌더링될 때 UI 컴포넌트는 Redux store의 현재 상태에 액세스하고 해당 데이터를 사용하여 렌더링할 항목을 결정한다. 또한 향후 store 업데이트를 구독하여 상태가 변경되었는지 확인한다.
-   업데이트:
    -   사용자가 버튼을 클릭하는 등, 앱에서 어떤 이벤트가 발생한다.
    -   앱 코드는 dispatch({type: 'counter/increment'})와 같이 Redux store에 액션을 전달한다.
    -   store는 이전 상태와 현재 액션으로 리듀서 함수를 다시 실행하고 기존 state를 반환값 (새 state)으로 대체한다.
    -   store는 구독 중인 UI의 모든 부분에 store가 업데이트되었음을 알린다.
    -   store의 데이터가 필요한 각 UI 컴포넌트는 필요한 상태의 일부가 변경되었는지 확인한다.
    -   데이터가 변경된 것을 확인한 각 컴포넌트는 새 데이터로 다시 렌더링하여 화면에 표시되는 내용을 업데이트할 수 있다.

위 흐름을 시각적으로 나타내면 다음과 같다.

![image](https://ko.redux.js.org/assets/images/ReduxDataFlowDiagram-49fa8c3968371d9ef6f2a1486bd40a26.gif)



<br>
<br>

##
[https://ko.redux.js.org/tutorials/essentials/part-1-overview-concepts](https://ko.redux.js.org/tutorials/essentials/part-1-overview-concepts)
