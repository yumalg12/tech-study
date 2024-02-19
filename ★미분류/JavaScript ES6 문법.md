## JavaScript ES6 문법

JavaScript ES6, 혹은 ECMAScript 2015라고 불리는 버전은 JavaScript의 주요 업데이트 중 하나이다.
ES6에서는 코드를 효율적으로 작성할 수 있는 수많은 신기능과 개선 사항이 도입되었다.

1. `let`과 `const` 키워드: `var`의 대안으로 도입된 새로운 변수 선언 키워드이다. `let`은 블록 스코프 변수를 선언하며, `const`는 블록 스코프 상수를 선언한다. 이들은 `var`와 달리 블록 단위의 스코프를 가진다.
   ```javascript
   let a = 10;
   const b = 20;
   ```

2. 화살표 함수: 함수 표현식의 새로운 형태이다. {}와 return 키워드를 생략할 수 있어 코드를 더욱 짧고 명확하게 만들 수 있다.
   ```javascript
   const func = (a, b) => a + b;
   ```

3. 템플릿 리터럴: 보다 쉽게 문자열 연결을 할 수 있으며, 표현식을 삽입할 수 있게 된다. 
   ```javascript
   const name = 'ES6';
   console.log(`Hello, ${name}!`); // "Hello, ES6!"
   ```

4. 디스트럭처링 할당 (구조분해 할당): 배열이나 객체의 속성을 해체하여 개별 변수에 할당하는 것이다.
   ```javascript
   const obj = { a: 1, b: 2 };
   const { a, b } = obj; // a = 1, b = 2
   ```

5. 기본 매개변수: 함수에 대한 매개변수가 제공되지 않을 경우에 대한 기본값을 설정할 수 있다. 
   ```javascript
   function greet(name = 'Guest') {
     return `Hello, ${name}!`;
   }
   console.log(greet()); // "Hello, Guest!"
   ```

6. 클래스: 객체 지향 패턴을 편리하게 만들어주는 클래스 구문을 도입하였다. 내부적으로는 여전히 프로토타입 체인이 작동하는 것이지만, 개발자에게는 클래스 기반의 문법을 제공함으로써 코드를 더욱 간결하고 이해하기 쉽게 만든다.
   ```javascript
   class Person {
     constructor(name) {
       this.name = name;
     }
     greet() {
       console.log(`Hello, ${this.name}!`);
     }
   }
   ```

7. 모듈: 코드를 여러 파일로 분리하고 재사용 가능한 모듈을 생성할 수 있게 해주는 `import`와 `export` 키워드가 도입되었다.
   ```javascript
   // lib.js
   export const sqrt = Math.sqrt;
   // main.js
   import { sqrt } from 'lib';
   console.log(sqrt(4)); // 2
   ```

8. 프로미스: 비동기 작업을 더 효과적으로 처리할 수 있게 해주는 객체이다. 콜백 함수를 사용하는 것보다 가독성이 높고, 비동기 코드의 흐름을 더 쉽게 제어할 수 있다.
   ```javascript
   const promise = new Promise((resolve, reject) => {
     // 비동기 작업 수행
   });
   ```

<br>
<br>

##
https://github.com/lukehoban/es6features
