
## POJO 기반의 구성



POJO란 Plain Old Java Object의 약자로 다른 클래스나 인터페이스를 상속/implements 받아 메서드가 추가된 클래스가 아닌 일반적으로 우리가 알고 있는 getter, setter 같이 기본적인 기능만 가진 자바 객체를 말한다.


POJO 프로그래밍이 필요한 이유

- 특정 환경이나 기술에 종속적이지 않으면 재사용이 가능하고, 확장 가능한 유연한 코드를 작성할 수 있다.
- 저수준 레벨의 기술과 환경에 종속적인 코드를 제거하여 코드를 간결해지며 디버깅하기에도 상대적으로 쉬워진다.
- 특정 기술이나 환경에 종속적이지 않기 때문에 테스트가 단순해진다.
- 객체지향적인 설계를 제한 없이 적용할 수 있다. (가장 중요한 이유)



public class CaregiverVO {
	private String g_id;
	private String g_pw;
	private String g_name;
	private String g_gender;

	public String getG_id() {
		return g_id;
	}

	public void setG_id(String g_id) {
		this.g_id = g_id;
	}

	public String getG_pw() {
		return g_pw;
	}

	public void setG_pw(String g_pw) {
		this.g_pw = g_pw;
	}

	public String getG_name() {
		return g_name;
	}

	public void setG_name(String g_name) {
		this.g_name = g_name;
	}

	public String getG_gender() {
		return g_gender;
	}

	public void setG_gender(String g_gender) {
		this.g_gender = g_gender;


POJO의 개념을 사용하지 않은 예시

```
public class ExampleListener implements MessageListener {

  public void onMessage(Message message) {
    if (message instanceof TextMessage) {
      try {
        System.out.println(((TextMessage) message).getText());
      }
      catch (JMSException ex) {
        throw new RuntimeException(ex);
      }
    }
    else {
      throw new IllegalArgumentException("Message must be of type TextMessage");
    }
  }

}
```

POJO의 개념을 사용한 예시

```
@Component
public class ExampleListener {

  @JmsListener(destination = "myDestination")
  public void processOrder(String message) {
    System.out.println(message);
  }
}
```



출처 https://velog.io/@galaxy/Spring%EC%9D%98-%EA%B8%B0%EB%B3%B8-%ED%8A%B9%EC%A7%95-POJO,https://ittrue.tistory.com/211
