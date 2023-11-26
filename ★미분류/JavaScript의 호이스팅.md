## JavaScript의 호이스팅

### 정의

JavaScript의 호이스팅 (Hoisting)은 코드 실행 전에 변수, 함수, 클래스, 또는 import 선언문을 해당 스코프(scope)의 최상단으로 이동시키는 것을 말한다. [1,2]

호이스팅은 ECMAScript 사양 (JavaScript 언어의 규격)에서 공식적으로 정의된 용어는 아니지만, JavaScript에서 변수 및 함수 선언을 처리하는 방식을 설명하는 데 사용된다. [1]

호이스팅은 JavaScript 엔진이 코드를 해석하는 과정에서 발생하는 것으로, 코드 실행 전에 변수 및 함수 선언을 메모리에 먼저 올려놓는 것을 의미한다.

자바스크립트 엔진은 코드를 실행하기 전에 실행 가능한 코드를 형상화하고 구분하는데, 이 과정의 결과로 호이스팅 현상이 나타나게 된다.
변수 및 함수 선언을 먼저 메모리에 등록하는 과정 (실행 컨텍스트를 위한 과정)에서 선언된 변수나 함수가 메모리에 미리 저장된다.
따라서, 코드에서 참조나 호출이 선언문보다 먼저 나와도 이미 메모리에 존재하므로 오류 없이 동작할 수 있게 된다. 
그러므로 엄밀히 말해 선언이 실제로 코드 최상단으로 이동한 것은 아니며, 끌어올려진 것**처럼** 동작하는 것이다. [2]

다시 말해, 호이스팅은 선언된 코드를 실제로 위로 올리는 것이 아니라 해당 선언을 메모리에 등록하는 과정으로 이해해야 한다.

<br>

### 호이스팅의 유형

호이스팅으로 간주되는 동작의 유형은 다음과 같다. [1]

1. **값 호이스팅 (Value Hoisting)**: 변수의 값을 선언 이전에 해당 스코프 내에서 사용할 수 있는 경우를 말합니다.
2. **선언 호이스팅 (Declaration Hoisting)**: 변수를 선언 이전에 해당 변수를 참조할 수 있지만, 값이 정의되지 않은 경우를 말합니다. ReferenceError는 발생하지 않지만 값은 항상 정의되지 않은 상태입니다.
3. **변수 선언**은 선언된 줄 앞의 범위에서 동작을 변경시킨다.
4. **선언의 부작용**은 선언이 포함된 코드를 평가하기 전에 발생한다.

<br>

자바스크립트의 모든 선언에는 호이스팅이 발생한다.

예를 들어, import 선언은 유형 1 및 유형 4 동작으로 처리된다. 함수 선언은 유형 1 동작인 "값 호이스팅" 으로 간주되며, var 선언은 유형 2 동작인 "선언 호이스팅" 으로 간주된다.

let, const, 및 class 선언은 유형 3 동작으로 처리된다.
이때, var 키워드로 선언된 변수와는 달리 let 키워드로 선언된 변수를 선언문 이전에 참조하면 참조 에러 (ReferenceError)가 발생하므로 호이스팅이 발생하지 않는 것으로 보일 수 있다.
let으로 선언된 변수는 스코프의 시작에서 변수의 선언까지 "일시적 사각지대 (Temporal Dead Zone; TDZ)"에 빠지기 때문이다.

TDZ는 해당 변수가 선언된 위치부터 초기화되기 전까지의 영역을 말한다. TDZ 내에 있는 변수를 참조하면 참조 에러가 발생한다.

let과 const는 선언될 때 초기값을 지정하지 않으면 TDZ에 들어가며, TDZ 내부에서 변수를 참조할 경우 ReferenceError가 발생한다.
반면에 var로 선언된 변수는 선언과 동시에 undefined로 초기화되어 메모리에 등록된다.[1,2]

<br>

### 호이스팅의 예시

다음은 var와 const 변수 호이스팅의 예시이다.
<table>
  <thead>
    <th></th>
    <th>실행문</th>
    <th>결과</th>
  </thead>
  <tbody>
    <tr><td>var</td><td>
var x = 1;<br>
{<br>
  console.log(x);<br>
  var x = 2;<br>
}
    </td><td>1</td></tr>
    <tr><td>const</td><td>
const x = 1;<br>
{<br>
  console.log(x);<br>
  const x = 2;<br>
}
    </td><td>
      VM1808:3 Uncaught ReferenceError: <br>Cannot access 'x' before initialization at <anonymous>:3:15
    </td></tr>
    <tr><td>const</td><td>
const x = 1;<br>
{<br>
  console.log(x);<br>
}
    </td><td>1</td></tr>
  </tbody>
</table>

만약 const x = 2 선언이 호이스팅되지 않았다면 (=실행될 때만 효력이 발생한다면) console.log(x) 문은 var의 예시와 같이 상위 스코프에서 x 값을 읽어들였을 것이다.

그러나 블록 스코프 내에서 선언된 const x = 2 가 호이스팅되었기 때문에 console.log(x) 문은 상위 범위에서 x 값을 읽을 수 없고, 초기화되지 않은 const x = 2 선언으로부터 x를 참조하려고 하여 ReferenceError가 발생하게 된다.


<br>

##
[1] https://hanamon.kr/javascript-%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85%EC%9D%B4%EB%9E%80-hoisting/<br>
[2] https://developer.mozilla.org/ko/docs/Glossary/Hoisting<br>
