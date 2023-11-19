## 정리
- String                :  문자열 연산이 적고 멀티쓰레드 환경일 경우
- StringBuffer     :  문자열 연산이 많고 멀티쓰레드 환경일 경우
- StringBuilder   :  문자열 연산이 많고 단일쓰레드이거나 동기화를 고려하지 않아도 되는 경우  

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99BE23375E2F133722">


## String  vs  StringBuffer/StringBuilder


String과 StringBuffer/StringBuilder 클래스의 가장 큰 차이점은 String은 불변(immutable)의 속성을 갖는다는 점이다.

> - 할당된 공간이 변하지 않는 특성을 불변(Immutable)성
> - 할당된 공간이 변하는 특성을 가변(mutable)성
<br>

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99948B355E2F13350F">


기존에 "hello" 값이 들어가있던 String 클래스의 참조변수 str이 "hello world"라는 값을 가지고 있는 새로운 메모리영역을 가리키게 변경된다.
처음 hello를 저장했던 메모리 영역은 Garbage로 남아있다가 GC(garbage collection)에 의해 사라진다.
**String 클래스는 불변하기 때문에 문자열을 수정하는 시점에 새로운 String 인스턴스가 생성된다.**

String은 불변성을 가지기 때문에 변하지 않는 문자열을 자주 읽어들이는 경우 사용하면 좋은 성능을 기대할 수 있다.
그러나 문자열 추가,수정,삭제 등의 연산이 빈번하게 발생하는 알고리즘에 String 클래스를 사용하면 힙 메모리(Heap)에 많은 임시 가비지(Garbage)가 생성되어 **힙메모리가 부족으로 어플리케이션 성능에 큰 영향을 끼칠 수 있다.**

StringBuffer/StringBuilder 는 가변성 가지기 때문에 .append() .delete() 등의 API를 이용하여 동일 객체내에서 문자열을 변경하는 것이 가능하다.
따라서 **문자열의 수정(추가, 삭제 등)이 빈번하게 발생할 경우라면 String 클래스가 아닌 StringBuffer/StringBuilder를 사용하는 것이 좋다.**

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F9923A9505E2F133608">

<br>

## StringBuffer  vs  StringBuilder
StringBuffer, StringBuilder의 가장 큰 차이점은 **동기화(Synchronization)의 유무**이다.

- **StringBuffer는 동기화 키워드를 지원하여 멀티쓰레드 환경에서 안전하다는 점(thread-safe)이다.**. 
- 참고로 String도 불변성을 가지기때문에 마찬가지로 멀티쓰레드 환경에서의 안정성(thread-safe)을 가지고 있다.

- **StringBuilder는** 동기화를 지원하지 않기 때문에 멀티쓰레드 환경에서 사용하는 것은 적합하지 않지만 **동기화를 고려하지 않는 단일쓰레드에서의 성능은 StringBuffer보다 뛰어나다.**


##
[출처]
https://ifuwanna.tistory.com/221
