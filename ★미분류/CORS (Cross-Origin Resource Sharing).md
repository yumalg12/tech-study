## CORS (Cross-Origin Resource Sharing)

### 1. 교차 출처 리소스 공유 정책과 동일 출처 정책
CORS (Cross-Origin Resource Sharing, 교차 출처 리소스 공유)는 웹페이지가 다른 도메인의 리소스를 요청할 수 있게 하는 체제이다. 

<br>

웹 애플리케이션은 리소스가 자신의 출처 (도메인, 프로토콜, 포트)와 다를 때 교차 출처 HTTP 요청을 실행하게 된다.
CORS 요청은, 트랜잭션 메시지의 추가 HTTP 헤더를 통해 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 것이다.[1]

기본적으로 웹 브라우저는 보안 상의 이유로 클라이언트가 클라이언트의 URL과 동일한 오리진의 리소스로만 요청을 보낼 수 있는 '동일 출처 정책 (Same-Origin Policy)' 을 사용한다.
클라이언트 URL의 프로토콜, 포트 및 호스트 이름은 모두 클라이언트에서 요청하는 서버와 일치해야 하는 것이다.

클라이언트 URL이 http://store.aws.com/dir/page.html일 때 각 URL은 다음과 같이 인식된다.
|URL                                      |판정  |이유                      |
|-----------------------------------------|-------|----------------------------|
|http://store.aws.com/dir2/new.html       |동일한 오리진|경로만 다름                      |
|http://store.aws.com/dir/inner/other.html|동일한 오리진|경로만 다름                      |
|https://store.aws.com/page.html          |다른 오리진 |다른 프로토콜 (http와 https)            |
|http://store.aws.com:81/dir/page.html    |다른 오리진 |다른 포트 (http://는 기본적으로 포트 80)|
|http://news.aws.com/dir/page.html        |다른 오리진 |다른 호스트(=도메인)                      |


동일 출처 정책은 '크로스 사이트 요청 위조 (CSRF) 문제*' 를 방지하기 위해 도입되었다. 
```
*CSRF는 피해자의 브라우저에서 다른 애플리케이션으로 피해자가 의도하지 않은 가짜 클라이언트 요청을 전송하는 해킹 방식이다.
이 공격은 피해자가 로그인한 상태에서 발생한다. 공격자는 피해자를 속여 새 브라우저 탭에서 외부 웹 사이트를 로드한다.
이 외부 웹 사이트는 피해자의 보안 인증 정보를 사용해 피해자인 것처럼 가장해 데이터를 요청한다.
이렇게 되면 서버는 공격자의 요청을 피해자의 정상적인 요청으로 인식하게 되어 권한이 없는 사용자에게 애플리케이션에 대한 액세스 권한이 부여되어 버린다.
```
동일 출처 정책은 보안 상으로는 안전하지만, 웹 애플리케이션에서 다른 출처의 리소스 이용이 제한되므로 유연하지 못하다는 문제가 있다.[2]

위와 같은 문제를 해결하기 위해, 동일 오리진 정책을 확장한 CORS가 도입되었다. CORS는 웹 애플리케이션에서 다른 출처의 리소스를 안전하게 요청할 수 있게 하는 메커니즘이다.
CORS 정책을 통해 웹 애플리케이션이 다른 출처의 리소스를 불러오려면 그 출처에서 올바른 CORS 헤더를 포함한 응답을 반환해야 한다.[1,2]
다시 말해, CORS는 보안을 유지하면서 웹 애플리케이션의 유연성을 높이는 중요한 역할을 한다.

<br>

정리하자면, 동일 출처 정책과 CORS는 웹의 보안 모델에서 핵심적인 부분을 차지하며 서로 보완적인 관계에 있다.
동일 출처 정책은 기본적인 보안 메커니즘이며, CORS는 이를 확장하여 웹 애플리케이션에서 필요에 따라 다른 출처의 리소스에 안전하게 접근할 수 있게 된다.

<br>

### 2. CORS 동작 원리

표준 인터넷 통신에서 브라우저는 애플리케이션 서버에 HTTP 요청을 보내고 HTTP 응답으로 데이터를 수신하여 표시한다.
이때 현재 브라우저 URL을 '현재 오리진', 서드 파티 URL을 '크로스 오리진' 이라고 한다.

크로스 오리진 요청 시 요청-응답 프로세스는 다음과 같다.[2]

1. 브라우저는 현재 오리진의 프로토콜, 호스트 및 포트에 대한 정보가 포함된 오리진 헤더를 요청에 추가한다.
```
https://news.example.com 이라는 사이트가 partner-api.com 의 API 리소스에 액세스를 시도하면,
```
2. 서버는 현재 오리진 헤더를 확인하고 요청된 데이터와 Access-Control-Allow-Origin 헤더로 응답한다.
```
https://partner-api.com의 개발자는 먼저 new.example.com을 허용된 오리진 목록에 추가하여 크로스 오리진 리소스 공유(CORS) 헤더를 구성한다.
이를 위해 서버 구성 파일에 아래 줄을 추가한다. 여러 오리진에 대한 액세스 권한을 부여하려면 쉼표로 구분된 목록이나 *와 같은 와일드카드 문자를 사용한다.
Access-Control-Allow-Origin: https://news.example.com
```
3. 브라우저는 액세스 제어 요청 헤더를 확인한 후, 반환된 데이터를 클라이언트 애플리케이션과 공유한다.
```
CORS 액세스가 구성되었기 때문에 news.example.com에서 partner-api.com의 리소스를 요청할 수 있다.
모든 요청에서 partner-api.com은 Access-Control-Allow-Credentials : "true"로 응답한다.
브라우저에서는 이 응답을 통해 통신이 승인되었음을 인지하고 크로스 오리진 액세스를 허용한다.
```
4. 서버에서 크로스 오리진 액세스를 허용하지 않는 경우에는 오류 메시지로 응답한다.

<br>

HTTP 요청 유형에 따라 CORS 동작은 다소 달라질 수 있다.[1-3]

![image](https://github.com/yumalg12/tech-study/assets/134472216/712ca5e3-25b9-47bd-803b-b5c35e6d2c38)

#### 단순 요청 (Simple Request)

'단순 요청 (Simple requests)' 이란, 특정 조건을 충족하는 HTTP 요청은 위험이 낮은 것으로 간주해 추가적인 확인 없이 바로 본 요청을 보내는 것이다.
브라우저가 자동으로 CORS를 처리하므로 사전 요청 (Preflight Request) 없이 바로 서버에 전송된다.

서버의 응답이 왔을 때 브라우저가 요청한 Origin과 응답한 헤더 Access-Control-Request-Headers의 값을 비교하여 유효한 요청이라면 리소스를 응답한다.
반면 유효하지 않은 요청이라면 브라우저에서 이를 막고 오류 메시지를 발생시킨다.

'단순 요청' 은 다음 조건을 모두 충족하는 요청을 말한다.

- HTTP 메소드가 'GET', 'HEAD', 'POST' 중 하나일 것. 이 세 가지 메소드는 서버의 상태를 변경하지 않는 요청에 주로 사용되는 것이다.
- 요청 헤더 중 수동으로 설정한 헤더는 'Accept', 'Accept-Language', 'Content-Language', 'Content-Type' 만일 것. 이는 보안을 위한 제한으로, 다른 헤더를 더 사용하려면 사전 요청이 필요하다.
- 'Content-Type' 헤더의 값이 'application/x-www-form-urlencoded', 'multipart/form-data', 'text/plain' 중 하나일 것. 이 세 가지 타입은 서버가 해석할 수 있는 일반적인 데이터 형식이다.
- XMLHttpRequest 객체를 사용하여 요청을 보낼 때, 이 요청의 업로드 과정을 모니터링하기 위해 XMLHttpRequest.upload 객체에 이벤트 리스너를 등록하지 않은 상태일 것. 즉, xhr.upload.addEventListener() 함수를 호출하여 업로드 과정을 추적하는 이벤트 리스너를 추가하지 않은 상태여야 한다.
- 요청에 ReadableStream 객체를 사용하지 않았을 것

![image](https://github.com/yumalg12/tech-study/assets/134472216/4054875c-e677-45b5-ba31-f4c02d260652)

<br>

#### 사전 요청 (Preflight)

단순 요청의 조건을 하나라도 위배하는 요청은 복잡한 크로스 오리진 요청으로 간주되어 '사전 요청' 단계가 추가된다.

실제 요청이 전송하기에 안전한지 확인하기 위해 먼저 해당 메서드를 사용하여 다른 원본의 리소스에 HTTP 요청을 보낸다.
예를 들어 기존 데이터를 삭제하거나 수정하라는 요청은 복잡한 것으로 간주되며, 이러한 원본 간 요청은 사용자 데이터에 영향을 미칠 수 있으므로 사전 요청이 수행된다.

사전 요청이 필요한 경우 브라우저에서 사전 요청이 생성되며, 이 사전 요청은 OPTIONS 요청 형태로 보내진다.

```
OPTIONS /data HTTP/1.1

Origin: https://example.com

Access-Control-Request-Method: DELETE
```

브라우저는 실제 요청 메시지가 전달되기 전에 사전 요청을 보낸다.
이때 서버는 서버가 클라이언트 URL에서 수락할 의향이 있는 크로스 오리진 요청에 대한 정보를 사용하여 사전 요청에 응답해야 한다.
서버 응답 헤더에는 다음이 포함되어야 한다.

- Access-Control-Allow-Methods
- Access-Control-Allow-Headers
- Access-Control-Allow-Origin

서버 응답의 예시는 다음과 같다.

```
HTTP/1.1 200 OK

Access-Control-Allow-Headers: Content-Type

Access-Control-Allow-Origin: https://news.example.com

Access-Control-Allow-Methods: GET, DELETE, HEAD, OPTIONS
```

사전 요청 응답에는 Access-Control-Max-Age 헤더가 추가로 포함될 수 있다.
이 헤더는 브라우저에서 브라우저의 사전 요청 결과를 캐시하는 기간을 초 단위로 지정하기 위해 사용된다.
캐싱을 사용하면 브라우저에서 사전 요청 사이에 여러 복잡한 요청을 전송할 수 있다.
max-age로 지정된 시간이 경과하기 전까지는 다른 사전 요청을 보내지 않아도 된다.

![image](https://github.com/yumalg12/tech-study/assets/134472216/45e6c5f4-6088-40ac-b5b6-5271c45961bf)

<br>

### 3. CORS 요청/응답 헤더 목록

#### 요청 헤더 목록
- Origin
- Access-Control-Request-Method: preflight 요청을 할 때 실제 요청에서 어떤 메서드를 사용할 것인지 서버에게 알리기 위해 사용
- Access-Control-Request-Headers: preflight 요청을 할 때 실제 요청에서 어떤 header를 사용할 것인지 서버에게 알리기 위해 사용
 
#### 응답 헤더 목록
- Access-Control-Allow-Origin: 브라우저가 해당 origin이 자원에 접근할 수 있도록 허용합니다. 혹은 *은 credentials이 없는 요청에 한해서 모든 origin에서 접근이 가능하도록 허용합니다.
- Access-Control-Expose-Headers: 브라우저가 액세스할 수 있는 서버 화이트리스트 헤더를 허용합니다.
- Access-Control-Max-Age: 얼마나 오랫동안 preflight요청이 캐싱 될 수 있는지를 나타낸다.
- Access-Control-Allow-Credentials
  - Credentials가 true 일 때 요청에 대한 응답이 노출될 수 있는지를 나타냅니다.
  - preflight 요청에 대한 응답의 일부로 사용되는 경우 실제 자격 증명을 사용하여 실제 요청을 수행할 수 있는지를 나타냅니다.
  - 간단한 GET 요청은 preflight되지 않으므로 자격 증명이 있는 리소스를 요청하면 헤더가 리소스와 함께 반환되지 않으면 브라우저에서 응답을 무시하고 웹 콘텐츠로 반환하지 않습니다.
- Access-Control-Allow-Methods: preflight 요청에 대한 대한 응답으로 허용되는 메서드들을 나타냅니다.
- Access-Control-Allow-Headers: preflight요청에 대한 대한 응답으로 실제 요청 시 사용할 수 있는 HTTP 헤더를 나타냅니다.

<br>

<br>

##
[1] https://developer.mozilla.org/ko/docs/Web/HTTP/CORS<br>
[2] https://aws.amazon.com/ko/what-is/cross-origin-resource-sharing/<br>
[3] https://hannut91.github.io/blogs/infra/cors<br>

<br>
