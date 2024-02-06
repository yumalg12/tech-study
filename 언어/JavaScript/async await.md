## async await

### async await란? [1]

async/await는 비동기적인 작업을 처리할 수 있는 ES2017 문법 이다. async 함수를 정의하면 함수 내부에서 await 키워드를 이용하여 비동기적으로 처리되는 작업이 완료될 때까지 기다린 후, 결과값을 반환하는 처리를 할 수 있다. async/await는 Promise를 기반으로 하며, 코드를 보다 간결하고 직관적으로 작성할 수 있도록 해주며, 콜백 hell을 없애줄 수 있다.

async await의 기본 구조를 아래와 같다. [2]

```
const getSomthing = async () => {
  await doSomething()
}
```
함수 앞에 async를 붙이고, 비동기 처리할 코드 앞에 await를 붙인다.

```
const asyncFunc = async () => {
  console.log('calling')
  await setTimeout(() => console.log('resolved'), 2000)
}

asyncFunc()
```

이렇게 실행하면 먼저 calling이 찍히고, 2초 뒤에 resolved가 찍히는 것을 볼 수 있다.


async await도 try와 catch로 성공 및 에러 여부를 감지할 수 있다. Promise와 async await의 코드 차이를 한번에 보자.

- Promise
```
const promise = new Promise((res, rej) => {
  console.log('first')
  setTimeout(() => {
    res('2초 후')
  }, 2000)
  console.log('end of function')
})

promise.then(res => console.log(res)).catch(err => console.error(err))
async await
```

- async await
```
const asyncFunc = async () => {
  try {
    console.log('first')
    await setTimeout(() => console.log('2초 후'), 2000)
  } catch (err) {
    console.log(err)
  }
  console.log('end of function')
}

asyncFunc()
```
두 함수의 결과 모두 first, end of function이 바로 찍히고, 2초 후에 2초 후가 console에 찍힌다.
같은 비동기 함수임에도 async await을 사용하면 코드를 더 깔끔하게 작성할 수 있다.


### 출처
[1] https://zero-base.co.kr/event/media_insight_contents_FE_frontend_tech_Interview <br>
[2] https://www.howdy-mj.me/javascript/async <br>
