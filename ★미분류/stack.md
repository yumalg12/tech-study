# Stack

자료의 입력과 출력을 한 곳으로
**후입선출(LIFO: Last in First Out)** 입출력 형태를 갖는 선형 자료구조

스택은 완전히 꽉 찼을 때 Overflow 상태라고 하며 완전히 비어 있으면 Underflow 상태라고 한다.

<p align="center">
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbcgR9A%2FbtqSX70PCTe%2FdMSMQoJcZhDpq4sRRpu3A0%2Fimg.png" width="30%"/>
</p>

### 연산 종류
- pop() : stack에서 가장 위에 있는 항목 제거
- push(item) : item 하나를 스택의 가장 윗 부분에 추가
- peek() : 스택의 가장 위에 있는 항목 반환
- isEmpty() : 스택이 비어있는 경우 true 반환

<br>

### 스택 구조
- Bottom : 가장 밑에 있는 데이터 또는 인덱스
- Top : 가장 위에 있는 데이터 또는 인덱스
- Capacity : 스택에 담을 수 있는 데이터의 총 용량
- Size : 현재 스택에 담겨져있는 데이터의 개수

<br>

### 스택 시간복잡도
스택의 삽입이나 삭제시 맨 위에서만 발생하기 때문에 **push, pop, isEmpty, peek 모두 시간복잡도는 늘 O(1)** 이다.   
하지만 특정 데이터를 찾을 때는 데이터를 찾을 때까지 순차적으로 수행해야 하므로 **O(n)** 의 시간복잡도를 갖는다.

<br>

### 스택활용
1. 함수 호출
    - 프로그래밍에서의 함수 호출과 복귀에 따른 순서 관리

2. 웹 브라우저 방문기록
    - 마지막으로 방문한 웹 사이트를 가장 먼저 조회할 수 있어 뒤로가기 기능을 구현할 때 유용하다.

3. 역순 문자열 만들기

<br>

##

[출처] <br>
https://velog.io/@alkwen0996/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%8A%A4%ED%83%9DStack
https://yoongrammer.tistory.com/45
