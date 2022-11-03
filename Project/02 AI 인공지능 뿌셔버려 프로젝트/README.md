문서정보 : 2022.11.03.~ . 작성, 작성자 [@SAgiKPJH](https://github.com/SAgiKPJH)

<br>

# [프로젝트 2] AI 인공지능 뿌셔버려

<br>

## 목적

- 인공지능으로 직접 다양한 개발을 할 수 있다.
- 인공지능으로 다양한 과제를 수행할 수 있다.
- 누구나 쉽게 공부해서 인공지능에 대해서 깊게 다룰 수 있다.

<br>

## 목표

- [ ] 0. 인공지능에 대한 개요
- [ ] 기초 공부
  - [ ] 뉴럴
- [ ] 도구 공부
  - [ ] TensorFlow
  - [ ] Hands-On Machine Learning
    - [ ] 1부 : 알고리즘
    - [ ] 2부 : 신경망 활용
  - [ ] Pytorch
  - [ ] Keras

<br>

### 제작 기간
- 10/03(목)부터

<br>

### 제작자
[@SAgiKPJH](https://github.com/SAgiKPJH)

---

<br>


# 0. 인공지능에 대한 개요

인공지능은 Nural NetWork를 어떻게 구성하느냐에 따라 종류가 달라진다.  
즉, NuralNetwork를 아이디어 + 수학모델 + 알고리즘을 합하여 구성한다.  
NuralNetwork를 만들자!  
\+ 빠르게!

<br>

### 인공지능 공부 방향
- 공부 방향
  - 뉴런(기본단위)
  - 뉴럴 네트워크 구축
  - 다양한 인공지능 구현
- 공부 요소
  - C++ CUDA cuDNN
  - Python TensorFlow
  - Pyrhon Pytorch
  - Python Keras
  - 툴 분석 + 활용
    - Darknet Yolo
    - ...
- 기타 요소
  - Apache MXNet
  - Deeplearning4j
  - OpnMP
  - TBB
  - MPI
  - CUDA
  - TensorRT
  - OpenVINO
- 도전과제
  - CNN설계 및 최적화
  - &|Network 구축해보기
- 무엇을 만들것인가?

<br>

### 각각 공부 방법 (해야할 것 + 할 수 있는 것)
- 순수 네트워크 구축해보기
  - [신경망이란?](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi)
- cuDNN
  - [cuDNN 라이브러리의 Convolution 사용하기](https://m.blog.naver.com/sogangori/220965933190)
  - [cuDNN 으로 컨볼루션 뉴럴 넷 구성하기](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=sogangori&logNo=220976878680)
- tensorflow (*.ckpt)
  - [TensorFlow Core 튜토리얼](https://www.tensorflow.org/tutorials?hl=ko)
    - [텐서플로 2.0 시작하기: 초보자를 위한 빠른 시작](https://www.tensorflow.org/tutorials/quickstart/beginner?hl=ko)
    - [텐서플로 2.0 시작하기: 전문가를 위한 빠른 시작](https://www.tensorflow.org/tutorials/quickstart/advanced?hl=ko)
    - [Keras를 사용한 ML 기본사항](https://www.tensorflow.org/tutorials/keras/classification?hl=ko)
    - [데이터 로드](https://www.tensorflow.org/tutorials/load_data/csv?hl=ko)
    - [맞춤 설정](https://www.tensorflow.org/tutorials/customization/basics?hl=ko)
    - [분산형 학습](https://www.tensorflow.org/tutorials/distribute/keras?hl=ko)
    - [이미지]
    - [텍스트]
    - [오디오]
    - [구조화된 데이터]
    - [생성]
      - Neural Style Transfer
      - DeepDream
      - 심층 합성곱 생성적 적대 신경망 (DCGANs)
      - Pix2Pix
      - CycleGAN
      - FGSM
      - Autoencoder
      - Variational Autoencoder
    - [모델 이해]
    - [강화학습]
    - [tf.estimator]
    - [어텐션을 사용한 인공 신경망 기계 번역](https://www.tensorflow.org/tutorials/text/nmt_with_attention?hl=ko)
  - [Probability](https://www.tensorflow.org/probability/examples/A_Tour_of_TensorFlow_Probability?hl=ko)
  - [Tendorflow PlayGround](https://playground.tensorflow.org/?hl=ko#activation=tanh&batchSize=10&dataset=circle%C2%AEDataset=reg-plane&learningRate=0.03%C2%AEularizationRate=0&noise=0&networkShape=4,2&seed=0.04620&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false)
  - [tensorflow App](https://www.tensorflow.org/lite?hl=ko)
  - [TFX](https://www.tensorflow.org/tfx?hl=ko)
- [pytorch](https://tutorials.pytorch.kr/)
  - [TORCHVISION 객체 검출 미세조정(FINETUNING) 튜토리얼](https://tutorials.pytorch.kr/intermediate/torchvision_tutorial.html)
  - [컴퓨터 비전(VISION)을 위한 전이학습(TRANSFER LEARNING)](https://tutorials.pytorch.kr/beginner/transfer_learning_tutorial.html)
- [Keras](https://keras.io/about/)
- yolo darknet 분석 (cuDNN 기반, *.data, *.cfg, *.weights)
- webui 분석 (PyTorch 기반, *.pt)
- c++에서 할 것이냐, python에서 할 것이냐 그것이 문제로다.
- [Apache MXNet](https://mxnet.apache.org/versions/1.4.1/tutorials/index.html)
- [Deeplearning4j]
  - [간단 가이드](https://recordsoflife.tistory.com/219)