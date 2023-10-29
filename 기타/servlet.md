## 서블릿
동적 웹 페이지를 만들 때 사용되는 자바 기반의 웹 애플리케이션 프로그래밍 기술

<br>

**서블릿 동작 과정**
![servlet](https://github.com/yumalg12/tech-study/assets/134472265/e4da7915-d9e6-46f5-a357-76c42c47b071)

<br>

> **Servlet Life-Sycle**
> - Init() : 서블릿이 메모리에 로드될 때 한번만 호출 (코드 수정 시 다시 호출)
> - doGet() : GET방식으로 data전송 시 호출
> - doPost() : POST방식으로 data전송 시 호출
> - service() : 모든 요청은 service()를 통해 doXXX()메소드로 이동
> - destroy() : 서블릿이 기능을 수행하고 메모리에서 소멸될 때 호출


<br>

[출처]<br>
[링크](https://java-is-happy-things.tistory.com/23) <br>
사진 출처 - [링크](https://velog.io/@blueskyi/%EC%84%9C%EB%B8%94%EB%A6%BFServlet%EC%9D%B4%EB%9E%80-%EB%8F%99%EC%9E%91%EB%B0%A9%EC%8B%9Dfeat.-Dispatcher-Servlet)
