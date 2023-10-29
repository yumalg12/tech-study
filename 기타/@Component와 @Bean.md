## 빈 등록 방법
1. @Component
2. @Bean

<br>

| | @Component | @Bean |
|---|---|---|
|| 모든 자바 클래스에서 사용가능 | 특정 메소드 위에만 사용 가능 |
| 사용 용이성 | 어노테이션만 추가하면 됨 | 빈 생성을 위해 코드 전체 작성 |
| Autowiring | 생성자 주입 방식, setter 주입 방식, 필드 주입 방식 | 특정 메소드 호출, 메소드 파라미터 사용 |
| 빈 생성 | Spring Framework | 코드 작성 |
|| 개발자가 직접 컨트롤이 가능한 클래스들의 경우 | 컨트롤 불가능한 외부 라이브러리들을 등록하고 싶은 경우 |

<br>
<hr>

[출처]
- Udemy 강의 - Spring Boot 3 & Spring Framework 6 마스터 (2023 Java 최신)<br>
- [링크](https://velog.io/@albaneo0724/Spring-%EC%8A%A4%ED%94%84%EB%A7%81-Bean%EA%B3%BC-Component%EC%9D%98-%EC%B0%A8%EC%9D%B4)
