####dense layer

- Dense는 딥러닝에서 가장 기본적인 뉴런 구성 요소 중 하나인 fully connected layer를 구현한 클래스입니다. 
- Dense Layer는 입력 뉴런과 출력 뉴런이 모두 연결되어 있는 밀집(dense)한 구조를 가지고 있습니다.
- Dense Layer는 입력 벡터와 가중치 행렬의 곱셈에 편향을 더하여, 활성화 함수를 거친 출력 값을 계산합니다.
- 일반적으로 활성화 함수로는 ReLU, sigmoid, tanh 등이 사용됩니다.
- Dense Layer는 다른 Layer와 결합하여 딥러닝 모델을 구성할 때 사용됩니다.
예를 들어, 이미지 분류 문제에서는 Flatten Layer로 이미지를 일차원 벡터로 변환한 후에 Dense Layer를 추가하여 출력 클래스에 대한 확률값을 계산합니다.



ex) 예시
from keras.layers import Dense
model = Sequential()
model.add(Dense(units=64, activation='relu', input_dim=100))
model.output_shape#(None, 64)

model.add(Dense(units=10, activation='softmax'))
model.output_shape#(None, 10)


출처 : https://wikidocs.net/192928, https://wikidocs.net/126060
