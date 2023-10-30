## EJB(Enterprise Java Bean)


EJB(Enterprise Java Bean)란 기업환경의 시스템을 구현하기 위한 서버 측 컴포넌트 모델이다. 일반적으로 업무 로직을 가지고 있는 서버 어플리케이션을 EJB라고 한다.


하지만 EJB에는 치명적인 단점이 있었는데, 바로 코드들이 EJB 기술에 지나치게 종속되어야 한다는 것이다. 
아래의 코드는 EJB 기반으로 작성된 것으로, 특정 서비스 계층에 EJB라는 기술이 마구 침투하는 모습을 확인할 수 있다. 
import 선언문부터 implenets, 인스턴스 변수까지 코드가 EJB에 완전히 종속된다.

마틴 파울러는 당시 인기를 끌던 EJB처럼 복잡하고 제한적인 기술보다는 자바의 단순 오브젝트를 이용해 비즈니스 로직을 구현하는 편이 낫다고 생각했다. 
그래서 만든것이 POJO이다.



■ EJB 장점

- 인스턴스 풀링: 객체를 미리 생성하여 메모리에 저장하여 사용준비 상태에 들어가도록 함, 많은 동시접속자에 대한 안정성 지원
- 트랜잭션 처리: 자동으로 컨테이너가 모든 처리메소드에 대하여 트랜잭션을 처리해줌, 안정적인 데이터 조작
- 퍼시스턴스 관리: 빈즈의 상태를 메모리에서 사용여부에 따라 자동으로 활성화/비활성화를 실행해 관리해줌
- FAT Client를 Thin Client로, n-tier 시스템을 구축할 수 있다.
- Weblogic, Webspere주로 사용, 국산은 제우스(jeus) 사용
- EJB 컴포넌트들이 Loading되어 활동하는 서버 쪽 프로그램, 컴포넌트의 생성, 소멸, 라이프 사이클, 보안, Threading 등의 서비스를 제공
 

■  EJB단점

- 객체지향적이지 않음
- 복잡한 프로그래밍 모델
- 특정 환경, 기술에 종속적인 코드
- 컨테이너에 안에서만 동작할 수 있는 객체구조
- 자동화된 테스트가 매우 어렵거나 불가능
- 부족한 개발생산성, 이동성(portablity)


종속적인 코드(Dependent Code)의 문제:

- 종속성: 초기 EJB 스펙은 EJB 컨테이너 환경에 강하게 종속됩니다. 이는 EJB 구성 요소가 특정 API와 클래스에 강하게 결합되어 독립적으로 실행되거나 테스트하기 어렵다는 의미입니다. 이로 인해 EJB 기반 소프트웨어의 이식성과 유지 관리가 어려워집니다.

- 단위 테스트의 복잡성: EJB의 이러한 종속성으로 인해, EJB 컴포넌트를 단위 테스트하기 위해서는 종종 전체 EJB 컨테이너를 실행해야 합니다. 이는 단위 테스트의 복잡성을 증가시키며, 빠른 피드백 사이클을 방해하고 개발 시간을 증가시킵니다.

- 개발 및 배포의 복잡성: EJB 컴포넌트를 개발하고 배포하기 위해서는 EJB 명세에 따라 많은 XML 구성이 필요합니다. 또한, EJB를 사용하는 클라이언트 코드 또한 EJB 환경에 강하게 종속되어 있어, 코드의 복잡성과 개발자의 부담을 증가시킵니다.

이러한 문제점들은 EJB3와 같은 후속 버전에서 개선되었으며, 의존성 주입(Dependency Injection)과 같은 기술이 도입되어 컴포넌트의 결합도를 줄이고 단위 테스트의 용이성을 증가시켰습니다. 그러나 초기 EJB 모델의 이러한 한계는 많은 개발자들이 경량 프레임워크(e.g., Spring)로 전환하는 원인 중 하나였습니다.


import javax.ejb.EJBException;
import javax.ejb.SessionBean;
import javax.ejb.SessionContext;

public class OrdersService implements SessionBean {

    private SessionContext ctx;

    public Orders placeOrder(String menuName) {
        Orders orders = new Orders(menuName);
        orders.init()
        return orders;
    }

    @Override
    public void setSessionContext(SessionContext ctx) throws EJBException {
        this.ctx = ctx;
    }

    @Override
    public void ejbRemove() throws EJBException {

    }

    @Override
    public void ejbActivate() throws EJBException {

    }

    @Override
    public void ejbPassivate() throws EJBException {

    }
}
