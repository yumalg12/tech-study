## Spring MVC

스프링 프레임워크는 웹 애플리케이션 개발에 필요한 여러 가지 기능들을 미리 만들어서 제공한다.

- Core: 다른 기능과 설정을 분리하기 위한 IoC 기능
- Context: 스프링의 기본 기능. 애플리케이션의 각 기능을 하는 빈 (Bean)에 대한 접근 방법 제공
- DAO: JDBC 기능을 좀 더 편리하게 사용할 수 있게 함
- ORM: 하이버네이트나 마이바티스와 같은 영속성 관련 프레임워크와 연동된 기능 제공
- AOP: 관점 지향 기능 제공
- Web: Web 애플리케이션 개발에 필요한 기능 제공
- <b>WebMVC: 스프링에서 MVC 구현에 관련된 기능 제공</b>

여기서 MVC 기능의 특징은 다음과 같다.

1. 모델2 아키텍처를 지원
2. 스프링과 다른 모듈과의 쉬운 연계
3. 타일즈 같은 View 기술과의 쉬운 연계
4. 태그 라이브러리를 통해 메시지 출력, 테마 적용, 입력 폼 구현을 쉽게 수행

스프링 프레임워크의 MVC 구성 요소는 다음과 같다.

- DispatcherServlet: 클라이언트의 요청을 전달받아 해당 요청에 대한 컨트롤러를 선택하여 클라이언트의 요청을 전달한다. 또한 컨트롤러가 반환한 값을 View에 전달하여 알맞은 응답을 생성한다.
- HandlerMapping: 클라이언트가 요청한 URL을 처리할 컨트롤러를 지정한다.
- Controller: 클라이언트의 요청을 처리한 후 그 결과를 DispatcherServlet에 전달한다.
- ModelAndView: 컨트롤러가 처리한 결과및 뷰 선택에 필요한 정보를 저장한다.
- ViewResolver: 컨트롤러의 처리결과를 전달할 뷰를 지정한다.
- View: 컨트롤러의 처리 결과 화면을 생성한다.

이 구성 요소들은 다음과 같이 상호작용한다.

![image](https://github.com/yumalg12/tech-study/assets/134472216/49f5b012-cd6c-4f21-88e2-74c4be61bf27)

1. 브라우저가 DispatcherServlet에 URL로 접근하여 필요한 정보를 요청한다.
2. 핸들러 매핑에서 해당 요청에 대해 매핑된 컨트롤러가 있는지 요청한다.
3. 매핑된 컨트롤러에 대해 처리를 요청한다.
4. 컨트롤러가 클라이언트의 요청을 처리한 결과와 View 이름을 ModelAndView에 저장해서 DispatcherServlet으로 반환한다.
5. DispatcherServlet에서는 컨트롤러에서 보내온 View 이름을 ViewResolver로 보내 해당 View를 요청한다.
6. ViewResolver는 요청한 View를 보낸다.
7. View의 처리 결과를 DispatcherServlet으로 보낸다.
8. DispatcherServlet은 최종 결과를 브라우저로 전송한다.
