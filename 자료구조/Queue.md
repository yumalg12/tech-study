# Queue

> 자료의 입력과 출력을 양쪽 끝으로 제한한 자료구조   
> 먼저 들어간 요소가 먼저 나오는 **선입선출(FIFO: First In First Out)** 구조

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F5NOv1%2FbtqSTINnoq8%2F4f8bjzzf6W4POewlq8At31%2Fimg.png" />

<br>

### 연산 종류
- enQueue() : 끝(rear)에 item 추가 (JAVA에서는 add())
- deQueue() : 맨 앞(front)에 데이터 제거 (JAVA에서는 remove())
- peak() : 맨 앞에 있는 데이터 반환
- isEmpty() : 큐가 비어있는지 확인

<br>

### 시간복잡도
데이터 삽입은 rear에서만 삭제는 front에서만 발생하기 때문에 **삽입과 삭제** 에 대한 시간복잡도는 **O(1)**   
**특정 데이터 검색** 은 찾을 때까지 수행되어야하므로 **O(n)** 의 시간복잡도를 갖는다.

<br>

### 종류
1. 선형 큐(Linear Queue)
    - **기본적인 큐 형태로 막대 모양의 큐**
    - 배열로 구현 시 크기가 제한되어 있고 빈 공간을 사용하려면 모든 자료를 꺼내거나 자료를 한칸씩 옮겨야한다는 단점이 있다.
    - 초기 공백 상태일 때 front == rear == 1
    - deQueue함수를 쓰면서 맨 앞에 있던 값이 빠져나가면서 front가 한칸씩 뒤로 밀려나 가용범위가 줄면서, 어느 시점(rear이 끝에 도달했을 때)에는 큐가 비어있어도 삽입하지 못하는 경우도 발생한다.

2. 환형 큐(Circular Queue)
    - 1차원 배열 형태의 큐를 원형으로 구성하여 배열의 처음과 끝을 연결해서 만들었다.(인덱스가 큐 끝에 도달하면 다시 처음을 가르키도록 짜서 마치 원형처럼 순환) 
    - 선형 큐의 문제점을 보완
    - 초기 공백 상태일 때 front == rear == 0
    - 공백, 포화 상태를 쉽게 구분하기 위해 자리 하나를 항상 비워둔다. ((index + 1) % size로 순환시킨다)
    - 배열로 구현되어 있어 큐의 크기가 제한되어 있다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRrA1R%2FbtqSPFc4BIJ%2FTLULef3Qof0kzKSXe7khZ1%2Fimg.png" />

<br>

### 사용예시
1. 스케줄링 큐
    - CPU 사용을 요청한 프로세서들의 순서를 스케줄링하기 위해 사용

2. 서로 다른 쓰레드 또는 프로세스 사이에서 자료를 주고 받을 때 자료를 일시적으로 저장하는 용도 (비동기 전송)
    - IO 버퍼, 파이프, 파일 IO

3. 프린터
    - 프린터의 인쇄 대기열을 Queue로 구현하면, 먼저 요청된 작업부터 차례대로 수행할 수 있다.

<br>

##

[출처]<br>
https://yoongrammer.tistory.com/46
https://kwin0825.tistory.com/157
https://kwin0825.tistory.com/54
https://laurent.tistory.com/entry/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%9B%90%ED%98%95-%ED%81%90
