## [React Hook] useState

useState는 컴포넌트에 상태 변수 (state variable)를 추가할 수 있는 React Hook이다. 여기서 상태 변수란 각 컴포넌트 별 메모리를 의미하는 '상태 (state)' 를 저장하기 위한 변수이다.

일반적으로 다음과 같은 형태로 선언한다.[1]

```
const [state, setState] = useState(initialState);
```

<br>

useState는 렌더링 간에 어떠한 상태를 유지하기 위해 사용한다. 예를 들어, 다음과 같이 페이지를 변경하는 코드는 작동하지 않는다.[2]

```
  let page = 0;

  function handleClick() {
    page = page + 1;
  }
```

버튼 클릭 시 page 로컬 변수 값이 변하게 되어 있으나, 페이지가 변경되며 리렌더링이 발생할 때에는 지역 변수가 유지되지 않으므로 리액트는 변화된 로컬 변수를 사용해 컴포넌트를 새로 렌더링해야 한다는 것을 모른다.

다시 말해, 로컬 변수를 변동시키는 것은 컴포넌트 렌더링을 트리거하지 못한다.

<br>

useState를 사용하면 다음과 같이 코드를 작성할 수 있다.

```
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
<br>

##
[1] https://react.dev/reference/react/useState<br>
[2] https://react.dev/learn/state-a-components-memory<br>
