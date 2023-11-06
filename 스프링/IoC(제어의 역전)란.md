## Spring IOC

### Spring Framework는 IOC기반이다. IOC란?

객체의 생성에서부터 생명주기의 관리까지 모든 객체에 대한 제어권이 바뀐것을 의미하는 것이 제어의 역전(IOC)이다.
스프링에서는 프로그램의 흐름을 프레임워크가 주도하고 객체의 생성부터 생명주기 관리를 컨테이너가 도맡아서 한다.
즉 제어권을 프로그램이 가지고 있는 게 아니고, 프레임워크 가지고 있으므로 제어가 역전된 상태인 것이다.



<details>
<summary>더보기</summary>

IOC는 Inversion of Control의 약자로 말 그대로 제어의 역전입니다. 그럼 제어의 역전이란 무엇일까요?     

자바가 등장하고 자바 기반으로 애플리케이션을 개발하기 시작하던 최초의 시기에는 개발자가 프로그램의 흐름(애플리케이션 코드)을 제어하는 주체였습니다.
자바 객체를 생성하고 객체간의 의존관계를 연결시키는 등의 제어권을 개발자가 직접 가지고 있었습니다. 

그러나 서블릿, EJB가 등장하면서 개발자들의 독점적으로 가지고 있던 제어권이 서블릿과 EJB를 관리하는 컨테이너에게 넘어가 버렸고
객체에 대한 제어권이 컨테이너에게 넘어가면서 객체의 생명주기를 관리하는 권한 또한 컨테이너들이 전담할 수 밖에 없게 되었습니다. 

이처럼 객체의 생성에서부터 생명주기의 관리까지 모든 객체에 대한 제어권이 바뀐것을 의미하는 것이 제어권의 역전, 즉 IoC라는 개념입니다.

스프링에서는 프로그램의 흐름을 프레임워크가 주도하고 객체의 생성부터 생명주기 관리를 컨테이너가 도맡아서 합니다.
즉, 제어권이 컨테이너로 넘어가게 되고, 이것을 제어권의 흐름이 바뀌었다고 해서 IoC(Inversion of Control: 제어의 역전) 이라고 합니다.

제어권이 컨테이너로 넘어옴으로써 DI(의존성 주입), AOP(관점 지향 프로그래밍) 등이 가능해졌으며,
의존성을 역전시켜 객채 간에 결합도를 줄이고, 유연한 코드를 작성할 수 있게 됨에 따라 가독성 및 코드 중복, 유지 보수를 편하게 할 수 있게 해줍니다. 

IoC의 대표적인 사례가 바로 프레임워크입니다. 우리가 프레임워크을 이용해 프로그램을 구현하면, 프레임워크 위에서 프로그램이 실행됩니다. 
이 말이 구현한 프레그램의 설정과 실행 등의 제어를 프레임워크가 해준다는 의미입니다. 
제어권을 프로그램이 가지고 있는 게 아니고, 프레임워크 가지고 있습니다. 제어가 역전된 상태인 것입니다. 그래서 IoC의 대표적인 예가 프레임워크가 되는 것입니다.

** EJB? Enterprise Java Bean

Java Bean이란 자바 객체를 재사용 가능하도록, 즉 컴포넌트화시킬 수 있는 코딩 방침을 정의한 것을 의미합니다.
EJB란 엔터프라이즈급 어플리케이션 개발을 단순화하기 위해 발표한 스펙으로 개발을 하다보면 많은 객체들을 만들게 되는데, 이러한 비지니스 객체들을 관리하는 컨테이너를 만들어서
필요할때 컨테이너로부터 객체를 받는 식으로 관리하면 효율적이겠다. 라는 것에서 탄생합니다.

엔터프라이즈 자바빈즈(Enterprise JavaBeans; EJB): 기업환경의 시스템을 구현하기 위한 서버측 컴포넌트 모델

EJB 사양은 Java EE의 자바 API 중 하나로, 주로 웹 시스템에서 JSP는 화면 로직을 처리하고, EJB는 업무 로직을 처리하는 역할을 합니다.
EJB는 비즈니스 객체들을 관리하는 컨테이너 기술, 설정에 의한 트랜잭션 기술 등이 담겨 있었습니다.
2000년대 초반에는 EJB라는 개념이 획기적이었고, Java 진영에서 표준으로 인정한 기술이기 때문에 많이 사용되었습니다.

EJB의 다양한 기술들을 사용하기 위해서는 EJB 스펙을 사용해야 했고, 그로 인하여 서비스가 구현해야 하는 비즈니스 로직보다 EJB 컨테이너 설정을 위해 더 많은 시간을 투자해야 했습니다.

개발자들은 오히려 평범한 자바 클래스 (POJO, Plain Old Java Object)를 사용 하려는 조짐을 보였다.
이런 복잡한 EJB의 컨테이너를 대체하기 위해서 등장한 것이 바로 Spring 컨테이너입니다.

Spring 컨테이너는 특정 클래스를 상속하거나 인터페이스를 구현하지 않는 POJO를 사용하여 많은 복잡성을 제거하였습니다.

</details>


### 출처
[1]https://khj93.tistory.com/entry/Spring-Spring-Framework%EB%9E%80-%EA%B8%B0%EB%B3%B8-%EA%B0%9C%EB%85%90-%ED%95%B5%EC%8B%AC-%EC%A0%95%EB%A6%AC <br>
[2]https://devscb.tistory.com/111 <br>
[3]https://www.nowwatersblog.com/springboot/springstudy/IOC%20&%20DI <br>
[4]https://belklog.tistory.com/entry/Spring-FrameworkIoC%EC%99%80-DI-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EA%B0%9C%EB%85%90%EC%A0%95%EB%A6%AC#google_vignette <br>
[5]https://madnix.tistory.com/entry/Spring-Framework%EC%99%80-IOC-DL-DI-%EC%A0%95%EC%9D%98 <br>
[6]https://velog.io/@outstandingboy/Spring-%EC%99%9C-%EC%8A%A4%ED%94%84%EB%A7%81-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%A0%EA%B9%8C-Spring-vs-EJB-JavaEE <br>
[7]https://velog.io/@outstandingboy/Spring-%EC%99%9C-%EC%8A%A4%ED%94%84%EB%A7%81-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%A0%EA%B9%8C-Spring-vs-EJB-JavaEE <br>
[8]https://hoon93.tistory.com/56 <br>
[9]https://velog.io/@corone_hi/%EC%97%94%ED%84%B0%ED%94%84%EB%9D%BC%EC%9D%B4%EC%A6%88-%EC%9E%90%EB%B0%94%EB%B9%88%EC%A6%88-EJB-Enterprise-Java-Beans<br>
