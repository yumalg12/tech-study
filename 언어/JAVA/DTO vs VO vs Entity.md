# DTO (Data Transfer Object)

**계층 간 데이터 교환을 하기 위해 사용하는 객체**로, 로직을 가지지 않는 순수한 데이터 객체

- 순수한 데이터 객체로써 속성과 그 속성에 접근하기 위한 getter, setter 메소드만 가진 클래스
- 주로 view와 controller 사이에서 데이터를 주고 받을 때 사용한다.

<br>

# VO (Vaule Object)

값 오브젝트로써 값 자체를 표현하는 객체

- **Read-Only** 특징을 가진다.
- 불변의 객체로 특정한 값을 나타내는 객체
- 값의 비교를 위해 equals()와 hashcode() 메소드를 오버라이딩 해야한다

<br>

# Entity

실재 DB의 테이블과 1:1로 매핑되는 클래스

- DB의 테이블 내에 존재하는 컬럼만을 속성으로 가져야한다
- Entityl 클래스는 상속을 받거나 구현체여서는 안된다.
- 요청이나 응답 값을 전달하는 클래스로 사용하면 안되며 id를 통해 구분

<br>
<br>

## DTO와 VO의 차이점

DTO는 데이터를 계층간 교환하는데 의미가 있고<br>
VO는 읽기만 가능한 read-only 속성을 가진 객체로서 데이터 그 자체에 의미를 두고 있다.(setter가 없다)

<br>

## Entityl와 DTO를 분리하는 이유

DB와 view 사이의 역할을 분리하기 위함이다.

Entity 클래스는 실제 테이블과 매핑되어 변경된다면 다른 클래스에 영향을 끼치고<br>
DTO 클래스는 view와 통신하며 자주 변경되므로 분리해줘야한다.(Entity 클래스 보호)

<br>
<br>

||DTO|VO|Entity|
|---|:---:|:---:|:---:|
|정의|레이어간 데이터 전송용 객체|값 표현용 객체|DB 테이블 매핑용 객체|
|상태 변경 여부|가변 또는 불변 객체|불변 객체|가변 또는 불변 객체|
|로직 포함 여부|로직 포함 X|로직 포함 O|로직 포함 O|

##

[출처]
- [링크](https://devmoony.tistory.com/180)
- [링크](https://tecoble.techcourse.co.kr/post/2021-05-16-dto-vs-vo-vs-entity/)
