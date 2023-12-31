## REACT

### Routing이란?
라우팅 이란 간단하게 말하면 사용자가 요청한 URL에 따라 해당 URL에 맞는 페이지를 보여주는 것이라고 생각할 수 있다.

### Client Side Routing이란?
Single Page Application이라는 용어 그대로 SPA는 하나의 페이지를 가지고 있지만 한 종류의 화면만 사용하는 것은 아니다. 화면이 변경되기 위해선 주소 또한 달라져야 할 필요가 있는데 이렇게 다른 주소에 따라 다른 화면을 보여주는 과정을 '경로에 따라 변경한다'라는 의미로 라우팅(Routing)이라고 한다. React는 View에 중점을 둔 프론트엔드 라이브러리이기 때문에 React 자체만으로는 라우팅 기능을 사용할 수 없다. 별도의 라이브러리를 설치해야지만 라우팅 기능을 사용할 수 있는데 통상적으로 React Router라는 라이브러리가 가장 많이 사용된다. React Router를 통한 SPA 내 화면 전환 및 주소 값 변경은 서버가 아니라 클라이언트(브라우저) 측에서 일어나기 때문에 Client-Side Routing이라고 한다.

### 서버 사이드 vs 클라이언트 사이드
Server-side (서버 측): 서버에서 라우팅을 처리하기 때문에 사용자가 해당 페이지에 직접 접근하는 방식. 즉, 웹 페이지 요청이 서버에 도달하면 서버에서 해당 페이지를 렌더링하고 클라이언트에게 반환한다.

Client-side (클라이언트 측): 클라이언트 내부에서 라우팅을 처리하기 때문에 해당 페이지를 호출할 때 루트(root)에서 시작하여 해당 페이지까지 차례로 로딩. 즉, 웹 애플리케이션이 로드된 후에 클라이언트 측에서 라우팅을 담당한다.

### 클라이언트 사이드 라우팅의 장점

1.  주소가 변경될때마다 매번 서버에서 페이지를 받아오지 않아도 되기 때문에 서버와 클라이언트 간의 데이터 트래픽이 감소한다는 이점이 있다. 즉, 페이지 이동이 빠르다.
2. 페이지 전환 시 새로고침을 방지할 수 있기 때문에 보다 자연스러운 페이지 이동과 사용자 경험을 제공하는 것이 가능해진다.

### 클라이언트 사이드 라우팅의 단점

1. 초기 로딩 시간이 길 수 있다. 모든 라우트와 컴포넌트 그리고 HTML이 한번에 로딩되기 때문에 모든 웹사이트가 첫 요청에 로딩되어야 한다.
2. 검색엔진 최적화(SEO)에 불리하다. 라우팅 시 콘텐츠 구성이 완료된 HTML을 서버에서 받아오는 것이 아니라 화면 구성에 필요한 모든 HTML을 클라이언트 측에서 처리하기 때문에 검색엔진에서 페이지 파악이 불리해진다. 이 때문에 검색 결과에서 더 높은 순위를 점하는 것이 어렵다. 
3. 보안 관련해서는 Client-Side Routing에서 사용자 정보 저장이 기존 서버 기반 세션이 아닌 상대적으로 보안에 취약한 클라이언트 기반의 쿠키에서 이루어지기 때문에 위험 요소가 될 수 있다.
4. 외부 라이브러리 사용이 필요하다. 서버 사이드 라우팅과 다르게 이는 더 많은 코드 작성과 외부 패키지에 대한 의존성을 높힐 수 있다.


### 출처
[1]  https://mari-mo.tistory.com/217<br>
[2] https://velog.io/@ye-ji/React-%EC%98%88%EC%83%81-%EB%A9%B4%EC%A0%91-%EC%A7%88%EB%AC%B8-%EB%A6%AC%EC%8A%A4%ED%8A%B8 <br>
[3] https://tturbo0824.tistory.com/131 <br>
[4] https://ksrae.github.io/angular/client-routing/ <br>
