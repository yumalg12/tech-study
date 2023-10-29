## MyBatis

### 마이바티스의 정의

마이바티스 (MyBatis)는 자바 퍼시스턴트 프레임워크\*에 속하는 프레임워크 중 하나로, 객체 지향 언어인 자바의 관계형 데이터베이스 프로그래밍\*\*을 좀더 쉽게 할 수 있게 도와주는 개발 프레임워크이다.

```
* 자바 퍼시스턴트 프레임워크: 퍼시스턴트 프레임워크는 (Persistence Framework) 지속성 프레임워크라고도 불리며, 데이터의 저장, 조회, 변경, 삭제 (CRUD) 를 다루는 클래스 및 설정 파일들의 집합이다. 지속성 프레임워크를 사용하면 JDBC 프로그래밍의 복잡함이나 번거로움 없이 간단한 작업만으로 데이터베이스와 연동되는 시스템을 빠르게 개발할 수 있으며 안정적인 구동도 보장한다.[2]<br>
** 관계형 데이터베이스: 키(key)와 값(value)의 관계를 나타내는 테이블(table)로 이루어진 데이터베이스. 데이터의 종속성을 관계(relationship)로 표현하는 것이 관계형 데이터베이스의 특징이다. 현재 가장 많이 사용되는 데이터베이스의 한 종류이다. 구성된 테이블이 다른 테이블들과 관계를 맺고 모여있는 집합체로 이해할 수 있다.[4]
```

마이바티스는 프로그램 코드와 SQL을 분리할 수 있어서 유지보수의 용이성과 가독성을 향상시킬 수 있다는 장점을 가지고 있다. 코드 내에 SQL문을 직접 포함시켰던 서블릿 환경에서와는 달리, 마이바티스 환경에서는 SQL문을 별도의 파일 (매퍼, mapper)에 저장한다. 매퍼에 저장된 객체는 'SQL문을 실행해 직접 DB를 다룰 수 있는 객체' 이며, 필요 시 호출해 사용한다.

따라서 마이바티스를 사용하면 JDBC를 통해 데이터베이스에 접근하는 작업을 캡슐화\*\*\*하고 JDBC 코드와 매개 변수의 중복 작업을 제거할 수 있다.[1,3]

```
*** 캡슐화: 클래스 안에서 서로 관련 있는 데이터와 이를 처리할 수 있는 기능들을 하나의 캡슐(capsule)로 만들어 데이터를 외부로부터 보호하는 것을 말한다. 캡슐화를 통해 클래스 내부의 속성과 기능들을 보호하고 필요한 부분만 외부에 노출시켜 객체의 독립성과 책임 영역을 안전하게 유지할 수 있다.[5]
```

<br>

마이바티스 매퍼는  XML 형식 또는 애너테이션 (annotation)을 사용하는 두 가지 방식으로 구성할 수 있다.[1]

<br>

### 애너테이션 방식

다음은 애너테이션을 사용해 생성한 마이바티스 매퍼 클래스의 예시이다.

```
package com.multi.shoes4jo.mapper;

import (...)

@Mapper
public interface BoardMapper {
package org.mybatis.example;

	// 게시물 번호에 해당하는 게시물 조회
	@Select("SELECT * FROM board WHERE bno = #{bno}")
	BoardVO select(@Param("bno") int bno);

	// 새 게시물 추가
	@Insert("INSERT INTO board (bno, category, title, content, writer, file_name, file_path, link) VALUES (#{bno}, #{category}, #{title}, #{content}, #{writer}, #{file_name}, #{file_path}, #{link})")
	int insert(BoardVO vo);

	// 기존 게시물 업데이트
	@Update("UPDATE board SET category = #{category}, title = #{title}, content = #{content}, file_name = #{file_name}, file_path = #{file_path}, link = #{link} WHERE bno = #{bno}")
	int update(BoardVO vo);

}
```

<br>

위 마이바티스 객체는 서비스 클래스에서 다음과 같이 호출된다.

```
package com.multi.shoes4jo.board;

import (...)

@Service("boardService")
public class BoardServiceImpl implements BoardService {

	@Autowired
	private BoardMapper mapper;

(...)

	@Override
	public BoardVO selectOne(int bno) {
		return mapper.select(bno);
	}

	@Override
	public void insertOne(BoardVO vo) {
		Integer maxBno = mapper.maxBno();
		vo.setBno((maxBno == null) ? 1 : maxBno + 1);
		mapper.insert(vo);
	}

	@Override
	public void updateOne(BoardVO vo) {
		mapper.update(vo);
	}

(...)

}
```

<br>

### XML 방식

매퍼 클래스를 생성하는 대신 XML 파일을 생성하여 따로 관리할 수도 있다. 다음은 그 예시이다.

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="memberMapper">

	<resultMap id="memResult" type="MemberVO">
		<result column="member_id" property="member_id" />
		<result column="member_name" property="member_name" />
		<result column="member_pw" property="member_pw" />
		<result column="signup_date" property="signup_date" />
		<result column="member_email" property="member_email" />
		<result column="member_phone" property="member_phone" />
	</resultMap>

(...)

	<select id="showMember" resultMap="memResult">
		SELECT * FROM `shoes_4jo`.`member`
	</select>

	<insert id="insertMember" parameterType="com.multi.shoes4jo.member.MemberVO">

<![CDATA[
        insert into `shoes_4jo`.`member`(member_id, member_name, member_pw, signup_date,member_email, member_phone)
        values(#{member_id}, #{member_name}, #{member_pw}, NOW(), #{member_email}, #{member_phone})
    ]]>
	</insert>

	<update id="updateMember" parameterType="com.multi.shoes4jo.member.MemberVO">

<![CDATA[
	     update `shoes_4jo`.`member`
	     set member_name=#{member_name}, member_pw=#{member_pw}
	     , member_email=#{member_email},member_phone=#{member_phone}
	     where
	     member_id=#{member_id}
      ]]>
	</update>

(...)

</mapper>
```

<br>

XML 형태의 마이바티스 매핑은 마이바티스 API를 이용해 세션을 생성해서 실행하게 된다.

```
package com.multi.shoes4jo.member;

import (...)

@Service
public class MemberServiceImpl implements MemberService {

	@Autowired
	private SqlSession sqlSession;

	@Override
	public int insertMember(MemberVO vo) throws Exception {
		try {
			return sqlSession.insert("memberMapper.insertMember", vo);
		} catch (Exception e) {
			e.printStackTrace();
		}
		return 0;
	}

	(...)
}
```

<br>

### 마이바티스 환경 적용

마이바티스 사용을 위해서는 프로젝트에 별도의 설정 xml 파일을 생성해야 한다. 이에 대해서는 공식 문서를 참고하면 좋다.
- 국문: https://mybatis.org/mybatis-3/ko/getting-started.html
- 영문: https://mybatis.org/mybatis-3/getting-started.html

<br>

##

[1] https://ko.wikipedia.org/wiki/%EB%A7%88%EC%9D%B4%EB%B0%94%ED%8B%B0%EC%8A%A4<br>
[2] https://ko.wikipedia.org/wiki/%EC%A7%80%EC%86%8D%EC%84%B1_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC<br>
[3] https://khj93.tistory.com/entry/MyBatis-MyBatis%EB%9E%80-%EA%B0%9C%EB%85%90-%EB%B0%8F-%ED%95%B5%EC%8B%AC-%EC%A0%95%EB%A6%AC<br>
[4] https://www.tcpschool.com/mysql/mysql_intro_relationalDB<br>
[5] https://www.codestates.com/blog/content/%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%ED%8A%B9%EC%A7%95

