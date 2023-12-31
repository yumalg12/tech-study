#### Hyper Parameters

```
머신러닝에서 하이퍼파라미터는 최적의 훈련 모델을 구현하기 위해 모델에 설정하는 변수로 학습률(Learning Rate), 에포크 수(훈련 반복 횟수), 가중치 초기화 등을 결정할 수 있습니다.
또한 하이퍼파라미터 튜닝 기법을 적용하여 훈련 모델의 최적값들을 찾을 수 있습니다.
```

하이퍼파라미터의 특징
- 모델의 매개 변수를 추정하는 데 도움이 되는 프로세스에서 사용된다.
- 하이퍼파라미터는 개발자에 의해 수동으로 설정할 수 있다.(임의 조정 가능)
- 학습 알고리즘의 샘플에 대한 일반화를 위해 조절된다.
하이퍼파라미터의 예
-학습률
-손실 함수
-일반화 파라미터
-미니배치 크기
-에포크 수
-가중치 초기화
-은닉층의 개수
-k-NN의 k값

1. 모델 파라미터는 새로운 샘플이 주어지면 무엇을 예측할지 결정하기 위해 사용하는 것이며 학습 모델에 의해 결정\
2. 하이퍼파라미터는 학습 알고리즘 자체의 파라미터로 모델이 새로운 샘플에 잘 일반화 되도록 하이퍼파라미터들의 최적값을 찾으나, 데이터 분석 결과로 얻어지는 값이 아니므로 절대적인 최적값은 존재하지 않고, 사용자가 직접 설정


출처:https://ittrue.tistory.com/42,  https://aws.amazon.com/ko/what-is/hyperparameter-tuning/, https://nanunzoey.tistory.com/entry/%ED%95%98%EC%9D%B4%ED%8D%BC%ED%8C%8C%EB%9D%BC%EB%AF%B8%ED%84%B0Hyperparmeter%EC%99%80-%EC%B5%9C%EC%A0%81%ED%99%94Optimization, https://aws.amazon.com/ko/what-is/hyperparameter-tuning/
