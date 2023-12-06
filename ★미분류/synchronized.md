## Synchronized(동기화)

**동기화는 여러 스레드가 하나의 자원에 접근하려 할 때 주어진 순간에는 단 하나의 쓰레드만이 접근 가능하도록 하는 것이다.**

둘 이상의 쓰레드가 공동의 자원(파일이나 메모리 블록)을 공유하는 경우,<br>
순서를 잘 맞추어 다른 쓰레드가 자원을 사용하고 있는 동안 한 쓰레드가 절대 자원을 변경할 수 없도록 해야한다.<br>
만약 한 쓰레드가 파일에서 레코드를 수정하는데, 다른 쓰레드가 동시에 같은 레코드를 수정하면 심각한 문제가 발생할 수 있기 때문이다.

공유데이터가 사용되어 동기화가 필요한 부분을 임계영역(critical section)이라고 부르며, 자바에서는 이 임계영역에 synchronized 키워드를 사용하여 여러 스레드가 동시에 접근하는 것을 금지함으로써 동기화를 할 수 있습니다. 

<br>
<hr>
<br>

### 동기화 사용방법

**1. synchronized 함수(메서드)를 만들어 사용합니다.**

메소드 이름 앞에 synchronized 키워드를 사용하면 해당 메소드 전체를 임계영역으로 설정할 수 있다.
```
synchronized void increase() {
	count++;
	System.out.println(count);
}
```

**2. synchronized 블록(block) 사용합니다.**

동기화를 많이 사용하면 효율이 떨어지게 되므로 꼭 필요한 부분에만 블럭을 지정하여 임계영역으로 설정할 수 있다.
예제와 같이 synchronized(this)로 지정하게 되면 참조변수(this) 객체의 lock을 사용하게 된다.
```
void increase() {
	synchronized(this) {
		count++;
	}
	System.out.println(count);
}
```

##

[출처]
https://kadosholy.tistory.com/123
