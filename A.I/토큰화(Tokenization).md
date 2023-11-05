토큰화(Tokenization)


```
주어진 텍스트에서 토큰(token)이라 불리는 단위로 나누는 작업을 토큰화(tokenization)라고 한다. 토큰의 단위는 상황에 따라 달라지지만 보통 의미있는 단위로 정의 한다.
```

하는 이유

자연어 처리에서 코퍼스 데이터가 필요에 맞게 전처리되지 않은 상태에서 해당 데이터를 사용하고자하는 용도에 맞게 토큰화(Tokenization)&정제(cleaning)&정규화(normalization)하는 일


단어 토큰화(Word Tokenization)

토큰의 기준을 단어로 하는 경우이다.이때 마침표(.), 컴마(,), 세미콜론(;), 느낌표(!)같은 기호는 제외시킨다.

       입력 : Time is an illusion. Lunchtime double so!
       출력 : 'Time', 'is', 'an', 'illusion', 'Lunchtime', 'double', 'so'

![image](https://github.com/yumalg12/tech-study/assets/74216748/945f0d90-ddac-438c-9438-b646868db925)


문장 토큰화(Sentence Tokenization)

문장 단위로 나누는 것 토큰의 기준을 문장으로 하는 경우이다.

![image](https://github.com/yumalg12/tech-study/assets/74216748/0ef0e0be-2031-4dab-9096-607de5b4925e)


출처 
https://katenam32.tistory.com/40
https://wikidocs.net/21698
