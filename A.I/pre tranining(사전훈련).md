####pre tranining(사전훈련)


```Pre-training(사전학습)이란 모델을 바로 주어진 데이터에 학습시키기 이전에 다른 데이터에 먼저 학습을 시키는 것을 말합니다. 이러한 pre-train된 모델의 parameter를 이용해서 모델을 초기화한 뒤 데이터에 fine-tuning하게 되면 임의로 초기화된 parameter를 가진 모델을 처음부터 학습시키는 것 보다 더 높은 성능을 보여줍니다. 예를 들어서, Computer vision에서는 엄청난 크기의 이미지 데이터인 ImageNet에 pre-train된 모델의 parameter를 가져와서 fine-tuning하는 방법이 있습니다.
```
