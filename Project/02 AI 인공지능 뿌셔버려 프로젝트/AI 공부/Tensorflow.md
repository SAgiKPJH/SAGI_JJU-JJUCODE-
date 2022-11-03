문서정보 : 2022.11.04.~ . 작성, 작성자 [@SAgiKPJH](https://github.com/SAgiKPJH)

<br>

# TensorFlow 공부 (초고속)

<br>

## 목적

- 초고속으로 TensorFlow를 공부하자.

<br>

## 목표

- [x] 개요
- [x] 초급 과정

<br>

### 제작 기간
- 10/04(금)부터

<br>

### 제작자
[@SAgiKPJH](https://github.com/SAgiKPJH)

---

<br>

# 개요

- 인공지능을 위해 여러 알고리즘이 있지만, 신경망을 중점으로 공부한다.
- 이를 위해 신경망을 다양하게 활용하는 TensorFlow를 공부해본다.
- 그것도 매우매우매우 빠르고 핵심만 바로!

<br><br><br>

# 초급 과정

### 손글씨 정보 학습

<img src="https://user-images.githubusercontent.com/66783849/199782040-157a850b-d580-4db7-8262-9492cf6eaa6b.png" width="250">

- 다음과 같이 요약
- 이미 튜토리얼 자체가 잘 만들어져 있기 때문에, 직접 배워보는 것도 좋다.
  ```bash
  # TensorFlow 설치
  pip install tensorflow
  ```
  ```python
  # TensorFlow 버전 확인
  import tensorflow as tf
  print("TensorFlow version:", tf.__version__)

  # 손글씨 정보 데이터 세트 (x:손글씨 이미지(28*28), y:숫자)
  # Train 6만개, Test 1만개
  mnist = tf.keras.datasets.mnist 
  (x_train, y_train), (x_test, y_test) = mnist.load_data() # x:0~255 이미지
  x_train, x_test = x_train / 255.0, x_test / 255.0 # x:0~1 이미지 변환

  # 신경망 구축
  model = tf.keras.models.Sequential([
    tf.keras.layers.Flatten(input_shape=(28, 28)),
    tf.keras.layers.Dense(128, activation='relu'),
    tf.keras.layers.Dropout(0.2),
    tf.keras.layers.Dense(10, activation='softmax')
  ])
  # 784 > 128 (relu) > Dropout(0.2) > 10 (확률분포)
  # Dropout(0.2) : 노드 20% 무작위로 0 (과적합 방지) 
  # softmax : 0~9 각 확률들을 나타냄
  
  # 모델 설정
  # optimizer adam : 최적화 'adam' 알고리즘
  # loss 형 유형을 선택, 훈련데이터의 label 값이 정수일 때
  # metrics : 모델 평가, accuracy: 빈도계산
  model.compile(optimizer='adam',
                loss='sparse_categorical_crossentropy',
                metrics=['accuracy'])

  # 모델 훈련, train으로 훈련, 5회
  model.fit(x_train, y_train, epochs=5)

  # 모델 평가, 몇 % 정확도인지 보여준다.
  model.evaluate(x_test,  y_test, verbose=2)
  ```
- model 대입 및 활용
  ```python
  # 모델에 대해서 직접 넣어 결과(10가지)를 확인할 수 있다.
  # x_train[:1] = array[ x_train[0] ]
  predictions = model(x_train[:1]).numpy()
  predictions
  
  # 결과 값(10가지)을 확률분포로 변환
  tf.nn.softmax(predictions).numpy()
  ```
- loss에 대해서 다음과 같이 확장 가능
  ```python
  # loss 유형 정의
  loss_fn = tf.keras.losses.SparseCategoricalCrossentropy(from_logits=True)
  
  # y_train[:1](정답)에 대한 predictions 에 대응되는 손실정도는?
  loss_fn(y_train[:1], predictions).numpy()
  # 무작위일 경우, -tf.math.log(1/10) ~= 2.3 이어야 한다.

  # 다음과 같이 활용 가능
  model.compile(optimizer='adam',
              loss=loss_fn,
              metrics=['accuracy'])
  ```
- 모델 확장 및 결과에 대해 확률분포로 표현
  ```python
  # 새 모델 정의 > model + 확률분포 레이어 추가
  probability_model = tf.keras.Sequential([
                 model,
                 tf.keras.layers.Softmax()
                 ])
  
  # 5가지 이미지에 대한 확률분포 확인
  probability_model(x_test[:5])
  ```

<br><br><br>

#

#

#