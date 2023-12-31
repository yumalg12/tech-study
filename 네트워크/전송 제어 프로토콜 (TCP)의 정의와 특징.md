## TCP의 정의와 특징

TCP란 전송 제어 프로토콜 (Transmission Control Protocol)으로, IP 프로토콜이 갖는 비연결성, 비신뢰성, 프로그램 구분 문제를 해결할 수 있는 기술이다. 그렇기 때문에 TCP는 IP의 상위 계층으로 구현되어 동작하며, IP의 단점들을 보완하게 된다.[1]

>#### 인터넷 프로토콜 스택의 4계층
>애플리케이션 계층 - HTTP, FTP<br>
>전송 계층 - TCP, UDP<br>
>인터넷 계층 - IP<br>
>네트워크 인터페이스 계층 - 랜카드, 랜 드라이버 등 물리적 장비

전송은 다음과 같은 단계로 이루어진다.

1. 애플리케이션 계층 (프로그램) 이 전송할 메시지를 생성
2. SOCKET 라이브러리를 통해 OS 계층 (TCPIP 부분) 에 메시지를 전달
3. 메시지 데이터를 포함하는 TCP 정보를 생성
4. TCP 정보와 메시지 데이터를 포함하는 IP 패킷을 생성
5. 네트워크 인터페이스 (랜 카드) 를 통해 외부로 전송

TCP 세그먼트에는 다음 정보가 포함된다.

- 출발지와 목적지의 Port 번호 -> 프로그램 구분 문제 해결
- 전송 제어 / 순서검증 정보 -> 비신뢰성 해결

TCP는 다음과 같은 특성을 갖는 신뢰할 수 있는 프로토콜이기 때문에 현재는 대부분 TCP를 사용한다.

- 연결 지향 TCP 3 way handshake (가상 연결)
- 데이터 전달 보증
- 순서 보장

##
[1] 모든 개발자를 위한 HTTP 웹 기본 지식, 김영한, 인프런
