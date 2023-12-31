####pre tranining(사전훈련)


```
Pre-training(사전학습)이란 모델을 바로 주어진 데이터에 학습시키기 이전에 다른 데이터에 먼저 학습을 시키는 것을 말합니다.
이러한 pre-train된 모델의 parameter를 이용해서 모델을 초기화한 뒤 데이터에 fine-tuning하게 되면 임의로 초기화된 parameter를 가진 모델을 처음부터 학습시키는 것 보다 더 높은 성능을 보여줍니다.
예를 들어서, Computer vision에서는 엄청난 크기의 이미지 데이터인 ImageNet에 pre-train된 모델의 parameter를 가져와서 fine-tuning하는 방법이 있습니다.
```


출처 :https://medium.com/riiid-teamblog-kr/%EB%AC%B8%EC%A0%9C-%EC%9E%84%EB%B2%A0%EB%94%A9%EC%9D%98-%EC%82%AC%EC%A0%84-%ED%95%99%EC%8A%B5%EC%9D%84-%ED%86%B5%ED%95%9C-knowledge-tracing-%EC%84%B1%EB%8A%A5%EC%9D%98-%ED%96%A5%EC%83%81-c5b3c645f8cd
