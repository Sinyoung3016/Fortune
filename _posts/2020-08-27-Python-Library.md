---
layout: post
title: "[PYTHON] Library"
date: 2020-08-27 00:00:00
categories: [STUDY]
tags: [PYTHON]
last_modified_at: 2021-01-11
---

From w3schools
<br>From [keras.io](https://keras.io/ko/)

---

### NumPy

<p>
Numerical Python
<br>: python library used for working with array
<br> + linear algebra, fourier transform and matrices
</p>

<p>
* 배열은 속도와 자원이 중요한 데이터과학에서 쓰임.
<br>* numPy Array = ndarray, N-dimensional array
<br>* 같은 데이터타입의 데이터만 배열에 넣을 수 있음.
<br>* 일반적인 파이썬 배열 객체보다 더 빠르게 기능함.
</p>

__NumPy ufuncs__

<p> : Universal Functions, ndarray객체에서 작동하는 Numpy함수로 벡터화를 통해 속도를 줄임.
<br>* 사칙연산, 반올림내림, 로그, 최소공배수, 최대공약수, 삼각합수, 쌍곡선, 집합 등의 연산이 가능.
</p>

```{.python}
#ufunc 만들기 : frompyfunc(함수이름, 인수(배열)의 수, 출력배열의 수)
def myadd(x, y):
  return x+y

myadd = np.frompyfunc(myadd, 2, 1)
print(myadd([1,2], [3,5]))

#함수가 ufunc인지 확인
print(type(myadd))
```

<figure>
  <center><img src="/Fortune/assets/Python/Numpy/15.png" alt="Midnight" style="width:100%"></center>
</figure>

---


### Keras
<p>
: deep learning API, running on TensorFlow
<br>* 빠르고 간편하게 실험 가능.
<br>* 사용자 친화성. 모듈성. 확장성이 장점.
<br>* model(데이터 구조)로 레이어를 조직하는 방식으로 대표적으로 Sequential
</p>

```{.python}
import tensorflow as tf
import numpy as np

#dataSet 설정
x_train = [1,2,3,4]
y_train = [1,2,3,4]

#Model 구성
model = tf.keras.models.Sequential()
  #units == output shape, input_dim = input shape
model.add(tf.keras.layers.Dense(units=1, input_dim=1)) #add로 layer쌓기

#Model의 학습과정 설정
  #mse = mean square error
  #sgd = stadard gradient descent
sgd = tf.keras.optimizers.SGD(lr=0.1)
model.compile(loss='mse', optimizer=sgd, metrics=['accuracy'])

#Model 학습
train = model.fit(x_train, y_train, epochs=100)

#Model 학습 과정 보기
print("##training loss and acc##")
print(train.history['loss'])
print(train.history['accuracy'])

#Model평가
print("##evaluation##")
eva = model.evaluate(x_train, y_train)
print(eva)

#Model 예측
print("##y_test##")
y_test = model.predict(np.array([4,6,7]))
print(y_test)

```

<figure>
<center><img src="/Fortune/assets/Python/keras/01.png" alt="Midnight" style="width:100%"></center>
</figure>

---

<br>
<br>



