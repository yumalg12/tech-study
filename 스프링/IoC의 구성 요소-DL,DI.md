## IoC의 구성요소 DL, DI

### DL(Dependency Lookup) - 의존성 검색

컨테이너에서는 객체들을 관리하기 위해 별도의 저장소에 빈을 저장하는데 개발자들이 컨테이너에서 제공하는 API를 이용하여 사용하고자 하는빈을 검색하는 방법이다.

아래와 같이 Bean에 대한 정보가 있는 XML 파일이 있다고 가정해 보자.

```
<beans>
	<bean id="myObject" class="com.Hyun.MyObject" />
</beans>
```
Java에서는 해당 XML의 Bean 정보를 보고 검색을 통해 어떤 클래스를 사용할 지 주입한다.

```
String myConfigLoc = "classPath:myAppContect.xml";
AbstractApplicationContext appCtx = new GenericXmlApplicationContext(myConfigLoc);
MyObject myobject = appCtx.getBean("myObject", myobject.class);
```

그 결과 위와같은 코드를 통해 적절한 MyObject 클래스를 검색하여 가져올 수 있다.



### DI(Dependency Injection) - 의존성 주입 

의존성 주입이란 객체가 서로 의존하는 관계가 되게 의존성을 주입하는 것이다. 
객체지향 프로그램에서 의존성이란 하나의 객체가 어떠한 다른 객체를 사용하고 있음을 의미한다. 그렇다면 IoC에서의 DI는 무엇일까?

바로 각 클래스 사이에 필요로 하는 의존관계를 빈 설정 정보를 바탕으로 컨테이너가 자동으로 연결해 주는 것이다.

일반적으로 빈 설정 파일을 바탕으로 의존 관계를 확인하여 주입한다.

이는 객체 레퍼런스를 컨테이너로부터 주입 받아 실행시 동적으로 의존관계가 생성되는 것이다.
따라서 컨테이너가 흐름에 주체가 되어 어플리케이션 코드에 의존 관계를 주입하게 되는 것이다.

<details>
<summary>더보기</summary>

#### 동적으로 의존 관계 생성?
클래스 다이어그램에서 표시되는 정적인 클래스 의존관계는 처음부터 끝까지 절대 변경되지 않는 의존 관계이다. 
반면 객체 다이어그램으로 표시되는 동적인 객체 인스턴스들은 실행 시 어떤 구현객체가 선택될지 결정되는 의존관계이다. 의존관계 주입은 바로 이 동적인 의존관계를 외부에서 주입해 주는 것.

</details>

의존관계 주입(DI)을 사용하여 동적인 인스턴스를 주입하면, 클라이언트의 변경 없이 호출 인스턴스를 변경할 수 있다는 장점이 있다. 
즉, 정적인 클래스 다이어그램, 클래스 의존관계의 변경 없이 동적 인스턴스를 변경할 수 있다.

즉, DI는 Spring에서 새롭게 지원하는 IoC의 한 형태로써 각 계층 사이, 각 Class 사이에 필요로 하는 의존관계가 있다면 
이를 컨테이너가 자동적으로 연결시켜 주는 것으로 각 Class 사이의 의존관계를 Bean 설정 정보를 바탕으로 컨테이너가 자동적으로 연결해 주는 것이다.


### DI 유형

(1) Constructor Injection(생성자 주입)
현재 가장 권장되는 의존 관계 주입 방식, Spring 공식 문서에서도 생성자 주입을 권장한다.

```
public class Injection {
 
    private InjectionService injectionService;
    
    // 생성자 DI
    // @Autowired -> Spring4.3부터는 @Autowired 생략 가능
    public Injection(InjectionService injectionService) {
    	this.injectionService = injectionService;
    }
}
```

생성자 주입이 가장 좋은 방법이지만, 이렇게 하면 매번 생성자를 만들어야 해서 귀찮고, 코드가 길어질 수 있는데 여기서 롬복(Lombok) 라이브러리를 사용하면 생성자 또한 어노테이션으로 생략할 수 있다.

```
@RequiredArgsConstructor
public class Injection {
 
    private InjectionService injectionService;
    
}
```

위의 코드를 보면 @RequiredArgsConstructor 은 롬복(Lombok)의 어노테이션 중 하나로 해당 어노테이션은 final 키워드가 붙은 주입에만 생성자를 만들어준다. 
만약 final 키워드를 사용하지 않으면 @AllArgsConstructor 어노테이션을 사용하면 된다.


(2) Field Injection(필드 주입)
어찌 보면 3가지 방법 중 가장 간단한 방법으로 Bean으로 등록된 객체를 사용하고자 하는 클래스에 Field로 선언한 뒤 @Autowired를 붙여주면 자동으로 의존 관계가 주입된다.

```
public class Injection {
	@Autowired
    private InjectionService injectionService;
}
```

> - 필드 주입의 장점 : 간결한 코드
> - 필드 주입의 단점 : 참조 관계를 눈으로 확인하기 어렵고, 순환 참조를 막을 수 없음


(3) Setter Injection(Setter 주입)
Spring에서 @Autowired 어노테이션을 사용해서 Setter 메서드를 통해 주입하는 방법으로
@Autowired는 Field, Setter Method, Constructor에 사용 가능하다.

```
public class Injection {
	
    private InjectionService injectionService;
    
    @Autowired // 생략가능
    public void setInjectionService( InjectionService injectionService) {
    	this.injectionService = injectionService;
    }
}
```

[출처]
[1]https://devmoony.tistory.com/100 <br>
[2]https://velog.io/@outstandingboy/Spring-%EC%99%9C-%EC%8A%A4%ED%94%84%EB%A7%81-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%A0%EA%B9%8C-Spring-vs-EJB-JavaEE <br>
[3]https://belklog.tistory.com/entry/Spring-FrameworkIoC%EC%99%80-DI-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EA%B0%9C%EB%85%90%EC%A0%95%EB%A6%AC#google_vignette <br>
[4]https://www.nowwatersblog.com/springboot/springstudy/IOC%20&%20DI <br>
[5]https://backendcode.tistory.com/249#google_vignette <br>
