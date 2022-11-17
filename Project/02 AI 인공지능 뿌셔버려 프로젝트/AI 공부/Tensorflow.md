문서정보 : 2022.11.04.~ . 작성, 작성자 [@SAgiKPJH](https://github.com/SAgiKPJH)

<br>

# TensorFlow 공부 (초고속)

<br>

## 목적

- 초고속으로 TensorFlow를 공부하자.

<br>

## 목표

- [x] 개요
- [x] [초급 과정](https://www.tensorflow.org/tutorials/quickstart/beginner?hl=ko)
- [x] [전문과 과정](https://www.tensorflow.org/tutorials/quickstart/advanced?hl=ko)
- [ ] Keras ML
  - [x] [기본 이미지 분류](https://www.tensorflow.org/tutorials/keras/classification?hl=ko)
  - [ ] [기본 텍스트 분류](https://www.tensorflow.org/tutorials/keras/text_classification?hl=ko)
  - [ ] TF Hub 텍스트 분류
  - [ ] 회귀
  - [ ] 과적합 및 과소적합
  - [ ] 저장 및 로드
  - [ ] Keras Tuner로 초매개변수 미세조정
  - [ ] keras.io에 관한 추가예

<br>

### 참고 사이트

- [TensorFlow Colab](https://colab.research.google.com/drive/17LOf94j3qGqdEiRWh-lGQRhmerkQ100L?usp=sharing)

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
- 요약하면 다음과 같다.
  - 학습 데이터 다운
  - 모델 생성
  - optimizer, loss유형 정의, 모델평가(metrics)
  - 모델 학습
  - 모델 결과 (가능하면 확률분포)

<br><br><br>

# 전문가 과정

- 초급 과정에서 조금더 세부적으로 제어할 수 있다.
  ```bash
  pip install tensorflow
  ```
  ```python
  # import
  import tensorflow as tf
  print("TensorFlow version:", tf.__version__)
  
  from tensorflow.keras.layers import Dense, Flatten, Conv2D
  from tensorflow.keras import Model

  # 모델 다운
  mnist = tf.keras.datasets.mnist
  
  # array([[~~]])
  (x_train, y_train), (x_test, y_test) = mnist.load_data()
  x_train, x_test = x_train / 255.0, x_test / 255.0
  
  # 채널 추가 array([ [[~~]] ], dtype=float32)
  x_train = x_train[..., tf.newaxis].astype("float32")
  x_test = x_test[..., tf.newaxis].astype("float32")

  # 데이터 섞기 + 묶음(batch)
  # 섞고 묶고
  train_ds = tf.data.Dataset.from_tensor_slices(
      (x_train, y_train)).shuffle(10000).batch(32)
  # 묶기만 하고
  test_ds = tf.data.Dataset.from_tensor_slices((x_test, y_test)).batch(32)
  
  # 모델 생성
  class MyModel(Model):
    def __init__(self):
      super(MyModel, self).__init__()
      self.conv1 = Conv2D(32, 3, activation='relu')
      self.flatten = Flatten()
      self.d1 = Dense(128, activation='relu')
      self.d2 = Dense(10)
    # 모델 사용할 시
    def call(self, x):
      x = self.conv1(x)
      x = self.flatten(x)
      x = self.d1(x)
      return self.d2(x)
  
  # Create an instance of the model
  model = MyModel()

  # optimizer, loss유형 정의
  loss_object = tf.keras.losses.SparseCategoricalCrossentropy(from_logits=True)
  optimizer = tf.keras.optimizers.Adam()
  
  # 모델평가(metrics) 정의
  train_loss = tf.keras.metrics.Mean(name='train_loss')
  train_accuracy = tf.keras.metrics.SparseCategoricalAccuracy(name='train_accuracy')
  
  test_loss = tf.keras.metrics.Mean(name='test_loss')
  test_accuracy = tf.keras.metrics.SparseCategoricalAccuracy(name='test_accuracy')

  # 모델 훈련 함수 생성
  # 배치수만큼(?) [이미지 모델 넣어보기 > loss 획득] > optimizer(최적화) > loss값 저장, 평가값 저장 
  @tf.function
  def train_step(images, labels):
    with tf.GradientTape() as tape:
      # training=True is only needed if there are layers with different
      # behavior during training versus inference (e.g. Dropout).
      predictions = model(images, training=True)
      loss = loss_object(labels, predictions)
    gradients = tape.gradient(loss, model.trainable_variables)
    optimizer.apply_gradients(zip(gradients, model.trainable_variables))

    train_loss(loss)
    train_accuracy(labels, predictions)
  
  # 모델 테스트 함수 생성
  # 모델 이미지 투하 > 로스 획득 > 로스 저장, 평가값 저장
  @tf.function
  def test_step(images, labels):
    # training=False is only needed if there are layers with different
    # behavior during training versus inference (e.g. Dropout).
    predictions = model(images, training=False)
    t_loss = loss_object(labels, predictions)
  
    test_loss(t_loss)
    test_accuracy(labels, predictions)

  # 학습 및 테스트
  EPOCHS = 5
  
  # 총 5회 반복
  # 각종 정보 초기화 > 이미지 수만큼 (6만/32번) 학습 돌리기 > 테스트 1만/32번 돌리기 > 결과값 보여주기
  for epoch in range(EPOCHS):
    # Reset the metrics at the start of the next epoch
    train_loss.reset_states()
    train_accuracy.reset_states()
    test_loss.reset_states()
    test_accuracy.reset_states()
  
    for images, labels in train_ds:
      train_step(images, labels)
  
    for test_images, test_labels in test_ds:
      test_step(test_images, test_labels)
  
    print(
      f'Epoch {epoch + 1}, '
      f'Loss: {train_loss.result()}, '
      f'Accuracy: {train_accuracy.result() * 100}, '
      f'Test Loss: {test_loss.result()}, '
      f'Test Accuracy: {test_accuracy.result() * 100}'
    )
  ```

<br><br><br>

# Keras ML

## 3.1 기본 이미지 분류

- 손글씨와 같은 28*28 > 128 > 10 모델로, 패션 용품을 분류하는 모델을 생성한다.
- 28*28의 흑백 이미지 7만장을 갖고 있다.
- 모델 키워드에 대한 정보는 다음과 같다.
  레이블 | 클래스
  -- | --
  0 | T-shirt/top
  1 | Trouser
  2 | Pullover
  3 | Dress
  4 | Coat
  5 | Sandal
  6 | Shirt
  7 | Sneaker
  8 | Bag
  9 | Ankle boot
- 이미지는 다음과 같다.  
  <img src="https://user-images.githubusercontent.com/66783849/200587223-ebea76a9-c20b-49b7-8e3f-19fb26008b63.png" width="150">
- 기본 코드는 다음과 같다.
  ```python
  # import
  import tensorflow as tf
  
  import numpy as np
  import matplotlib.pyplot as plt
  
  print(tf.__version__)
  
  # 모델 다운 (패션:키워드 모델 다운), train 6만개, test 1만개
  fashion_mnist = tf.keras.datasets.fashion_mnist
  (train_images, train_labels), (test_images, test_labels) = fashion_mnist.load_data()
  
  # 학습에 대한 배열 정의
  class_names = ['T-shirt/top', 'Trouser', 'Pullover', 'Dress', 'Coat', 'Sandal', 'Shirt', 'Sneaker', 'Bag', 'Ankle boot']
  
  # 이미지 0 ~ 255 -> 0 ~ 1
  train_images = train_images / 255.0
  test_images = test_images / 255.0
  
  # 각 이미지 보기
  plt.figure(figsize=(10,10))
  for i in range(25):
      plt.subplot(5,5,i+1)
      plt.xticks([])
      plt.yticks([])
      plt.grid(False)
      plt.imshow(train_images[i], cmap=plt.cm.binary)
      plt.xlabel(class_names[train_labels[i]])
  plt.show()
  
  # 모델 설정
  model = tf.keras.Sequential([
      tf.keras.layers.Flatten(input_shape=(28, 28)),
      tf.keras.layers.Dense(128, activation='relu'),
      tf.keras.layers.Dense(10)
  ])
  model.compile(optimizer='adam',
                loss=tf.keras.losses.SparseCategoricalCrossentropy(from_logits=True),
                metrics=['accuracy'])
  
  # 모델 학습
  model.fit(train_images, train_labels, epochs=10)
  
  # 학습 결과
  test_loss, test_acc = model.evaluate(test_images,  test_labels, verbose=2)
  print('\nTest accuracy:', test_acc)
  ```
- 모델 변형 및 예측
  ```python
  # 모델 변형 및 예측
  probability_model = tf.keras.Sequential([model, tf.keras.layers.Softmax()])
  
  # 1회 학습
  predictions = probability_model.predict(test_images)
  
  # 예측값 확인
  predictions[0]
  
  # 예측값 클래스 추출
  np.argmax(predictions[0])
  
  # 레이블 값과 비교
  test_labels[0]
  ```
- 결과 이미지화
  ```python
  # 결과 이미지화
  
  def plot_image(i, predictions_array, true_label, img):
    true_label, img = true_label[i], img[i]
    plt.grid(False)
    plt.xticks([])
    plt.yticks([])
  
    plt.imshow(img, cmap=plt.cm.binary)
  
    predicted_label = np.argmax(predictions_array)
    if predicted_label == true_label:
      color = 'blue'
    else:
      color = 'red'
  
    plt.xlabel("{} {:2.0f}% ({})".format(class_names[predicted_label],
                                  100*np.max(predictions_array),
                                  class_names[true_label]),
                                  color=color)
  
  def plot_value_array(i, predictions_array, true_label):
    true_label = true_label[i]
    plt.grid(False)
    plt.xticks(range(10))
    plt.yticks([])
    thisplot = plt.bar(range(10), predictions_array, color="#777777")
    plt.ylim([0, 1])
    predicted_label = np.argmax(predictions_array)
  
    thisplot[predicted_label].set_color('red')
    thisplot[true_label].set_color('blue')
  
  # Plot the first X test images, their predicted labels, and the true labels.
  # Color correct predictions in blue and incorrect predictions in red.
  num_rows = 5
  num_cols = 3
  num_images = num_rows*num_cols
  plt.figure(figsize=(2*2*num_cols, 2*num_rows))
  for i in range(num_images):
    plt.subplot(num_rows, 2*num_cols, 2*i+1)
    plot_image(i, predictions[i], test_labels, test_images)
    plt.subplot(num_rows, 2*num_cols, 2*i+2)
    plot_value_array(i, predictions[i], test_labels)
  plt.tight_layout()
  plt.show()
  ```
- 이미지 직접 넣어보기
  ```python
  # 모델 직접 적용 튜토리얼
  # 이미지 부여
  img = test_images[1]
  print(img.shape)
  
  # 배치 파일 부여 이미지
  img = (np.expand_dims(img,0))
  print(img.shape)
  
  # 이미지의 예측값 획득
  predictions_single = probability_model.predict(img)
  print(predictions_single)
  
  # 이미지의 예측값 시각화
  plot_value_array(1, predictions_single[0], test_labels)
  _ = plt.xticks(range(10), class_names, rotation=45)
  plt.show()
  
  # 이미지의 결과값
  print("Result : " + str(np.argmax(predictions_single[0])))
  ```
- 다음과 같은 결과 이미지를 획득할 수 있다.  
  <img src="https://user-images.githubusercontent.com/66783849/200592486-21cdf52e-0490-4148-a956-a5d021ef4b70.png" width="250">

<br><br>

## 3.2 기본 텍스트 분류

 인터넷 영화 데이터베이스(Internet Movie Database)에서 수집한 50,000개의 영화 리뷰 텍스트를 담은 IMDB 데이터셋을 사용하여, 영화 리뷰(review) 텍스트를 긍정(positive) 또는 부정(negative)으로 분류해본다.  
- 기본 코드는 다음과 같다.
```python
import tensorflow as tf
from tensorflow import keras
import numpy as np
print(tf.__version__)

imdb = keras.datasets.imdb
(train_data, train_labels), (test_data, test_labels) = imdb.load_data(num_words=10000)
# 훈련 데이터에서 가장 많이 등장하는 상위 10,000개의 단어를 선택
# 학습용 25,000, 훈련용 25,000
```

<br><br>

##

<br><br><br>


#