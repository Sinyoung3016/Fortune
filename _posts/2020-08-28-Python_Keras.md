---
layout: post
title: "[PYTHON] Keras 정리(ing)"
date: 2020-08-28 00:00:00
categories: [SOPHOMORE]
tags: [PYTHON]
last_modified_at: 2020-08-28
---

From [keras.io](https://keras.io/ko/)

---

__Keras__
<p> : deep learning API, running on TensorFlow
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

## Model
<p> Keras 제공 모델 = 1.Sequential Model 2.Model class
</p>

#### 공통된 메소드와 속성들

|model.layers|모델을 구성하는 레이어들이 저장된 1차원 리스트|
|model.inputs|모델의 입력 텐서들이 저장된 1차원 리스트|
|model.outputs|모델의 출력 텐서들이 저장된 1차원 리스트|
|model.summary()|모델의 구조 출력, utils.print_summary(model)|
|model.get_config()|모델의 설정이 저장된 딕셔너리를 반환|
|model.get_weights()|모델의 가중치 텐서들이 NumPy 배열로 저장된 1차원 리스트|
|model.set_weights(weights)|모델의 가중치 값을 NumPy 배열의 리스트로부터 설정|

---

__Sequential Model__
### compile
<p>: 학습을 위해 모델을 구성.</p>

```{.python}
compile(optimizer, loss=None, metrics=None, loss_weights=None, sample_weight_mode=None, weighted_metrics=None, target_tensors=None)
```
###### arguments

|optimizer|최적화 알고리즘 이름(string)|
|loss|손실 함수 이름(string)|
|metrics|학습 과정에서 평가할 측정학목의 리스트|
|loss_weights||
|sample_weight_mode||
|weighted_metrics||
|target_tensors||

---

### fit
<p>: 정해진 수의 세대에 걸쳐 모델을 학습시킴.(dataSet에 대한 반복)</p>

```{.python}
fit(x=None, y=None, batch_size=None, epochs=1, verbose=1, callbacks=None, validation_split=0.0, validation_data=None, shuffle=True, class_weight=None, sample_weight=None, initial_epoch=0, steps_per_epoch=None, validation_steps=None)
```
###### arguments

|x|Input data. 데이터의 Numpy배열 또는 Numpy배열의 리스트|
|y|Target data. 데이터의 Numpy배열 또는 Numpy배열의 리스트|
|batch_size||
|epochs|모델을 학습시킬 세대의 수, 한 세대는 제공된 모든 x와 y에 대한 반복.|
|verbose||
|callbacks||
|validation_split||
|validation_data||
|shuffle||
|class_weight||
|sample_weight||
|initial_epoch||
|steps_per_epoch||
|validation_steps||

###### returns
<p>
: History Object
<br> * History.history : 연속된 epoch동안, record of training loss values and metrics values
</p>

---

### evaluate
<p>: 테스트 모드에서의 모델의 손실값과 측정항목값을 반환.
<br> 계산은 batch단위로 이루어짐.
</p>

```{.python}
evaluate(x=None, y=None, batch_size=None, verbose=1, sample_weight=None, steps=None, callbacks=None)
```
###### arguments

|x|Input data|
|y|Target data|
|batch_size||
|verbose||
|sample_weight||
|steps||
|callbacks||

###### returns
<p>
: scalar test loss(if the model has a single output and no metrics)
<br> or list of scalars(if the model has multiple outputs and/or metrics)
</p>

---

### predict
<p>: input sample에 대한 ouput 예측을 생성
<br> 계산은 batch단위로 이루어짐.
</p>

```{.python}
predict(x, batch_size=None, verbose=0, steps=None, callbacks=None)
```
###### arguments

|x|Input data|
|batch_size||
|verbose||
|steps||
|callbacks||

###### returns
<p>
: 예측 값의 Numpy 배열
</p>

---

## Layers
<p> : 하나 이상의 텐서를 입출력으로 사용하는 호출가능한 객체,
</p>

__Dense__

```{.python}
keras.layers.Dense(units, activation=None, use_bias=True, kernel_initializer='glorot_uniform', bias_initializer='zeros', kernel_regularizer=None, bias_regularizer=None, activity_regularizer=None, kernel_constraint=None, bias_constraint=None)
```
###### arguments

|units|출력 노드의 수|
|activation|사용할 활성화 함수|
|use_bias||
|kernel_initializer||
|bias_initializer||
|kernel_regularizer||
|bias_regularizer||
|activity_regularizer||
|kernel_constraint||
|bias_constraint||

```{.python}
model = Sequential()
model.add(Dense(32, input_shape=(1,)))#shape tuple

model.add(Dense(32, input_dim=1))
```
<p>
* 첫번째 레이어에서 입력형태에 대한 정보를 입력해줌
</p>


<br>
<br>



