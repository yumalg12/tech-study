# Database Scan

## Full Scan
> 테이블에 포함된 모든 레코드에 접근하는 방식

## Range Scan
> 테이블의 일부 레코드에만 접근하는 방식 <br/>
> ex) where 조건절 사용 <br/>
> Index 를 사용하면 Full Scan 을 사용하지 않고 Range Scan 을 사용

## Index 생성 시 주의할 점
> 읽기 (Select) 를 하는 경우 성능 상의 이점이 생기나, <br/> 
> 생성 (create), 수정 (update), 삭제 (delete) 작업 시에는 <br/>
> 원본 테이블의 수정과 함께 Index의 수정도 같이 이루어지기 때문에 <br/>
> 데이터의 수정보다 데이터의 읽기가 자주 사용되는 테이블에 생성하는 것이 좋다.