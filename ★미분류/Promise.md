## Promise

Promise는 JavaScript에서 비동기 연산*을 처리하는 객체이다. 
```
*비동기 연산: 결과를 즉시 얻지 못하고 나중에 얻게 되는 연산. 예를 들어, 서버에서 데이터를 불러오는 작업이나 타이머 기능 등이 이에 해당한다.
```

<br>

일반적으로 비동기 작업은 콜백 함수를 사용하여 처리된다. 예를 들어, 파일을 읽는 비동기 작업을 수행할 때, 파일을 읽은 후에 실행할 콜백 함수를 전달해야 하는 상황을 가정하면, 다음과 같이 비동기 콜백 함수 여러 개가 중첩된 콜백 지옥 (callback hell)에 빠질 수 있다.

콜백 함수가 중첩되면 들여쓰기가 깊어지고, 위에서 아래로 코드를 읽는 흐름이 깨진다. 또한 에러 처리도 각 단계에서 중복되어 발생할 수 있다다. 이러한 상황을 "콜백 지옥" 이라고 한다.

```javascript
readFile('file1.txt', function(err, data1) {
    if (err) {
        handleError(err);
    } else {
        // file1.txt를 읽은 후에 실행할 작업
        readFile('file2.txt', function(err, data2) {
            if (err) {
                handleError(err);
            } else {
                // file2.txt를 읽은 후에 실행할 작업
                readFile('file3.txt', function(err, data3) {
                    if (err) {
                        handleError(err);
                    } else {
                        // file3.txt를 읽은 후에 실행할 작업
                        // 계속해서 콜백 함수가 중첩됨
                    }
                });
            }
        });
    }
});
```

<br>

Promise 객체는 비동기 작업이 맞이할 미래의 완료 또는 실패와 그 결과 값을 나타낸다. 기본적으로 promise는 함수에 콜백을 전달하는 대신 콜백을 첨부하는 방식의 객체이므로, 비동기 코드를 더욱 쉽게 작성하고 이해할 수 있도록 한다.

Promise는 다음과 같은 세 가지 상태를 갖는다.

1. **대기 (Pending):** 비동기 처리 로직이 아직 완료되지 않은 상태
2. **이행 (Fulfilled):** 비동기 처리가 완료되어 Promise가 결과 값을 반환한 상태
3. **거부 (Rejected):** 비동기 처리가 실패하거나 오류가 발생한 상태

Promise 객체는 `then`, `catch`, `finally` 등의 메서드를 제공합니다. `then` 메서드는 Promise가 이행될 때 호출할 함수를 등록하며, `catch` 메서드는 Promise가 거부될 때 호출할 함수를 등록한다.
또한 `finally` 메서드는 Promise가 이행되거나 거부될 때 호출할 함수를 등록한다.

![image](https://github.com/yumalg12/tech-study/assets/134472216/a439f623-439e-4d49-ab01-edc151745215)


Promise 사용 예시는 다음과 같다.

```javascript
let promise = new Promise(function(resolve, reject) {
  // 비동기 작업을 수행
  
  if (/* 비동기 작업이 성공적으로 완료되었으면 */) {
    resolve("작업 결과");
  }
  else {
    reject(Error("작업 중 오류 발생"));
  }
});

promise
  .then(result => {
    // promise가 이행되면 실행됨
    console.log(result); // "작업 결과"
  })
  .catch(error => {
    // promise가 거부되면 실행됨
    console.error(error); // Error: 작업 중 오류 발생
  });
```

위 코드에서 `new Promise`는 Promise 객체를 생성하고, `resolve`와 `reject`는 각각 Promise를 이행하거나 거부하는 함수이다.
이 Promise 객체에 `then`과 `catch` 메서드를 사용하여 이행과 거부 시의 콜백 함수를 등록할 수 있다. 이렇게 하면 비동기 작업의 성공 또는 실패에 따른 후속 작업을 쉽게 처리할 수 있다.

<br>
<br>

##
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise
https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Using_promises
