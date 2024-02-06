# Java Stream 연산의 종류

## Java Stream 연산의 종류

- 중간 연산
> - Stream 을 연결할 수 있는 연산을 지칭한다. <br>
> - filter, sorted 와 같은 연산이 있다. <br>
> - 중간 연산은 다른 Stream 을 반환하기 때문에 여러 중간 연산을 나열하여 질의를 만들 수 있다. (메서드 체이닝) <br>
> ex)  
    members.stream(). <br>
    .filter(...) // 중간 연산 <br>
    .map(...) // 중간 연산 <br>
    .limit(...) // 중간 연산 <br>
    .collect(toList()); // 최종 연산 <br>
> 위와 같은 경우 filter(), map(), limit()을 순차적으로 수행하는 것이 아니라 이를 모두 합친 하나의 연산으로 수행된다. (루프 퓨전)

- 최종 연산 
> Stream 을 닫는 연산을 지칭한다. <br>
> 최종 연산에 의해 반환형이 지정된다. <br>
> forEach(), collect() 와 같은 연산이 있다. <br> 

### 출처
https://yoo-dev.tistory.com/38