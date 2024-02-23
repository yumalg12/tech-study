Word2vec 

```
딥러닝 기반의 word embedding 방법으로 단어간 유사도를 반영할 수 있도록 단어의 의미를 벡터화할 수 있는 방법이다.
```



Word2vec 모델은 Continous Bag of Words(CBoW)와 Skip-Gram 두 가지 방식이 있다.

![word2vec](https://github.com/yumalg12/tech-study/assets/74216748/91ea1623-2e44-4e3f-81d3-eb3e0f655d01)


 Continous Bag of Words(CBoW)

- CBoW란? 주변에 있는 단어들을 가지고 중간에 있는 단어들을 예측하는 방법
- 즉, "The fat cat sat on the mat"라는 문장이 있을때 sat을 예측하는것 
![sat](https://github.com/yumalg12/tech-study/assets/74216748/e2f38d82-67ce-49d3-bac8-7d334f8e2252)


- 문장의 n개의 토큰이 있을 때 예측대상의 단어 인덱스는 int(n/2)이며 이를 중심단어(center word)라고 합니다.
- 예측에 사용되는 단어들을 주변 단어(context word) 락 합니다.
- 중심단어를 예측하기 위해서 주변 단어의 수, 앞 뒤로 몇 개의 단어를 볼지 범위를 정하게 되는데 이범위를 원도우(window)라고 합니다.
- 즉, window=k일때, 예측에 사용되는 주변단어의 개수는 2k입니다.

아래는 "The fat cat sat on the mat" 문장에서원도우의 크기를 2로 설정했을때 CBow가 학습되는 과정입니다.

![그림 3](https://github.com/yumalg12/tech-study/assets/74216748/a15eed33-bd67-42c0-b6d3-a6f55425ea6b)


Input layer : fat,cat,on,the 주변단어가 one-hot vector로 input 
Output layer: sat 중심단어가 one-hot vector로 output 

Skip-Gram

CBoW와 반대로 중간에 있는 단어로 주변 단어들을 예측하는 방법입니다. 중심단어에서 주변단어를 예측하므로 input에는 중심단어가 output은 주변단어가 됩니다. 또한 중심단어에서 주변 단어를 예측하므로 투사층에서 벡터들의 평균을 구하는 과정은 없습니다. 성능인 skip-gram이 CBoW보다 성능이 좋다고 알려져있습니다.



출처
https://codingsmu.tistory.com/100
<br>
https://www.goldenplanet.co.kr/our_contents/blog?number=859&pn=1
<br>
https://terms.naver.com/entry.naver?docId=6717082&cid=40942&categoryId=32845
<br>
https://wikidocs.net/22660
