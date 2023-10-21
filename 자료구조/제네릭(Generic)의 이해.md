
## 제네릭(Generic)이란?

제네릭(Generic)은 '데이터 형식에 의존하지 않고, 하나의 값이 여러 다른 데이터 타입들을 가질 수 있도록 하는 방법'이다.
제네릭은 컬렉션 프레임 워크에서 많이 사용되며, 타입 안정성을 유지하면서 다양한 타입의 객체를 저장하고 처리할 수 있다.

예를 들어 우리가 어떤 자료 구조를 만들어 배포하려고 할 때에 String 타입도 지원하고 싶고 Integer 타입도 지원하고 싶을때
String에 대한 클래스, Integer에 대한 클래스 등 하나하나 타입을 만들기에는 너무 비효율적이다.
이러한 문제를 해결하기 위해 우리는 제네릭을 사용할 수 있다.


Generic(제네릭)의 장점

1. 제네릭을 사용하면 잘못된 타입이 들어올 수 있는 것을 컴파일 단계에서 방지할 수 있다.
2. 클래스 외부에서 타입을 지정해주기 때문에 따로 타입을 체크하고 변환해줄 필요가 없다. 즉, 관리하기가 편하다.
3. 비슷한 기능을 지원하는 경우 코드의 재사용성이 높아진다.


>#### Generic(제네릭) 사용방법
> <T>	Type
> <E>	Element
> <K>	Key
> <V>	Value
> <N>	Number


- 클래스 및 인터페이스 선언

(1)
public class ClassName <T> { ... }
public interface InterfaceName <T> { ... }

(2)
public class ClassName <T, K> { ... }
 
public class Main {
	public static void main(String[] args) {
		ClassName<String, Integer> a = new ClassName<String, Integer>();
	}
}

*이 때 주의해야 할 점은 타입 파라미터로 명시할 수 있는 것은 참조 타입(Reference Type)밖에 올 수 없다. 
즉, int, double, char 같은 primitive type은 올 수 없다는 것이다. 
그래서 int형 double형 등 primitive Type의 경우 Integer, Double 같은 Wrapper Type으로 쓰는 이유가 바로 위와같은 이유다.

또한 바꿔 말하면 참조 타입이 올 수 있다는 것은 사용자가 정의한 클래스도 타입으로 올 수 있다는 것이다.


- 제네릭 클래스

class ClassName<E> {
	
	private E element;	// 제네릭 타입 변수
	
	void set(E element) {	// 제네릭 파라미터 메소드
		this.element = element;
	}
	
	E get() {	// 제네릭 타입 반환 메소드
		return element;
	}
	
}
 
class Main {
	public static void main(String[] args) {
		
		ClassName<String> a = new ClassName<String>();
		ClassName<Integer> b = new ClassName<Integer>();
		
		a.set("10");
		b.set(10);
	
		System.out.println("a data : " + a.get());
		// 반환된 변수의 타입 출력 
		System.out.println("a E Type : " + a.get().getClass().getName());
		
		System.out.println();
		System.out.println("b data : " + b.get());
		// 반환된 변수의 타입 출력 
		System.out.println("b E Type : " + b.get().getClass().getName());
		
	}
}
 
보면 ClassName이란 객체를 생성할 때 <> 안에 타입 파라미터(Type parameter)를 지정한다.
 
그러면 a객체의 ClassName의 E 제네릭 타입은 String으로 모두 변환된다.
반대로 b객체의 ClassName의 E 제네릭 타입은 Integer으로 모두 변환된다.
 
실제로 위 코드를 실행시키면 다음과 같이 출력된다.

a data : 10
a E Type : java.lang.String

b data : 10
b E Type : java.lang.Integer



https://st-lab.tistory.com/153
