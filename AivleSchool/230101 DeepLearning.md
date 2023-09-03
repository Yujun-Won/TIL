# Aivle School Deep Learning 베스트 질문

- [1. TensorFlow vs. PyTorch](#1-tensorflow-vs-pytorch)
- [2. 스케일링](#2-스케일링)
- [3. Loss와 Accuracy](#3-mysql에서-select-문-조회-결과를-테이블로-생성하기)
- [4. 쿼리문 작성할 때 대문자와 소문자](#4-쿼리문-작성할-때-대문자와-소문자)
- [5. metrics의 표기 차이](#5-metrics의-표기-차이)


## 1. TensorFlow vs. PyTorch
```plain text
연구는 PyTorch, 실무에서는 TensorFlow를 주로 사용한다.
프레임워크의 우열은 없고, 그냥 개인 취향이다.
```

## 2. 스케일링
```plain text
스케일링이 항상 성능에 좋은 영향을 주는 것은 아니다.

모델을 학습시킬 때 사용되는 데이터들은 각 특성마다 데이터가 가질 수 있는 값의 범위가 다르다.
예를 들어, 나이와 재산이라는 특성이 있을 때, 두 특성의 단위가 다르다.
따라서 이 경우 재산에 치중된 학습을 하게 된다.

스케일링 기법도 여러가지가 있다.
```

## 3. Loss와 Accuracy
```plain text
Loss와 Accuracy 사이의 연관관계가 존재하는 것은 아니다.

Accuracy는 전체 데이터에 대한 예측 오류의 수로 볼 수 있다.
100개 중 97개를 맞췄다면 accuracy는 97%이다.

Loss는 실제 정답과 모델이 예측한 값 사이의 차이이다.
즉, 손실이 클수록 데이터에 대한 오류도 커진다.
더 쉽게 말하면, 틀리게 예측한 경우 얼마나 오류를 범했는가로 볼 수 있다.
2개의 모델이 100개 중 97개를 똑같이 맞춰도 둘의 오차는 다를 수 있다.

A모델(정확도: 0.9786, 손실: 0.089612)
B모델(정확도: 0.9802, 손실: 0.105635)

B모델의 정확도가 더 높지만(더 많이 맞췄지만) 몇몇의 데이터에서 큰 오류를 범했다고 볼 수 있다.

A모델은 정확도가 B모델보다 낮지만 손실이 적다.
즉, 많은 데이터에서 오류가 거의 발생하지 않음을 알 수 있다.
```

## 4. 레이어 개수나 노드의 개수를 정하는 기준
```plain
테스트 에러가 기준이 된다.

테스트 에러가 증가하지 않을 때까지 레이어를 추가하면 된다.
즉, 테스트 에러가 감소한다면 레이어를 계속 추가할 수 있다.
```

## 5. metrics의 표기 차이
- `metrics=[keras.metrics.Accuracy()]`
- `metrics=['accuracy']`
```plain text
두 코드는 의미가 다르다.

1. metrics=['accuracy']
loss='binary_crossentropy'에 맞는 매트릭스를 자동으로 불러 와서 BinaryAccuracy()를 사용

2. metrics=[keras.metrics.Accuracy()]
Accuracy()를 사용
```