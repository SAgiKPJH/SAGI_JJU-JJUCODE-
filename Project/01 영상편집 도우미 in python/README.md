문서정보 : 2022.09.20.~ 작성, 작성자 [@SAgiKPJH](https://github.com/SAgiKPJH)

<br>

# [프로젝트 1] 영상편집 도우미 in python

## 목적

- 영상편집을 할 때, 핵심부분만 따로 추출하는 프로그램을 만드는 목적

```mermaid
flowchart LR
A["영상"]--1. 입력-->B["프로그램<br>Python"]--3. 출력-->C["출력 영상"]
B--2. 소리부분 추출-->B
```

### 목표
- [ ] : 1. 환경 구성
- [ ] : 2. 영상 받기
  - [ ] Test 영상 선정
  - [ ] Test 영상 Python으로 출력
  - [ ] Python으로 영상 제어
  - [ ] Python으로 영상 중간에서 틀기
  - [ ] Python으로 소리 출력
  - [ ] Python으로 소리 이미지화
  - [ ] Python으로 소리 실시간 이미지화
  - [ ] 최적화
- [ ] : 3. 영상 편집
  - [ ] 소리 일정부분 이상 감지
  - [ ] 영상 자르기
  - [ ] 최적화
- [ ] : 4. 영상 출력
  - [ ] 영상 내보내기

### 제작 기간
- 09/20 (화) ~

### 제작자
[@SAgiKPJH](https://github.com/SAgiKPJH)


---

<br><br><br>

## 1. 환경 구성

### Python 환경 기본 구성

- Python 설치
  - Python 사이트를 통해 최신 버전을 설치한다.

<br>

### 설치된 Python, pip VScode에 연결하기

- VScode
  - Python은 VScode를 통해 구현한다.
  - VScode에 Python을 설치한다.
- Jupyter Nodebook
  - Jupyter Nodebook을 통해 단계별 과정을 실험한다.
  - Python으로 영상을 다루는 방법을 알기 위해 VScode에 jupyter를 설치하고 실행한다.
  - 설치 후 [View] > [Command Palette...(명령 팔레트...)] > ">create" 입력 > [Python: Create New Black Jupyter Notebook] 클릭 > Jupyter Notebook을 생성한다.
- VScode에 설치된 pip와 python을 연결한다.
  - python 위치 획득
    - 설치된 Python 프로그램 위치에 이동한다.
    - 윈도우 > python 검색 > python 3.10 파일의 위치 열기 > python 위치 획득
    - 파일 위치 예) C:\Users\UserName\AppData\Local\Programs\Python\Python310\
  - pip 위치 획득
    - python 폴더 > Scripts 폴더 > pip 및 pip3가 존재함을 확인
    - 파일 위치 예) C:\Users\UserName\AppData\Local\Programs\Python\Python310\Scripts\
  - <img src="https://user-images.githubusercontent.com/66783849/191776092-86e1c0a4-2aab-4ccb-b85b-73366a0541cc.png" width="70%"><br> 윈도우 > 고급 시스템 설정 보기 검색 후 실행 > 시스템 속성 창 > 환경 변수 > [UserName에 대한 사용자 변수]와 [시스템 변수]에 존재하는 path > Python 폴더위치 및 pip 폴더 위치를 등록한다.

<br>

## OpenCV
<img src="https://user-images.githubusercontent.com/66783849/186481810-4badd25d-bb67-4d26-b6ef-c74ecba02e5c.png" width="19%">

- OpenCV(Open Source Computer Vision)은 실시간 컴퓨터 비전을 목적으로한 프로그래밍 라이브러리이다.
- C++와 Python에서 연동 사용 가능하다.
- pip3 install opencv-python를 통해 install 한다.
- VScode 터미널을 통해 pip3 install opencv-pyhon을 진행한다.

<br>



<br><br><br>

# 2. 영상 받기

- Python으로 영상을 받고 가공할 수 있다.

<br><br>

## Test 영상 선정

- 영상 3개 선정
  - 영상 1 : 8초짜리 영상
  - 영상 2 : 1분 17초짜리
  - 영상 3 : 8초 짜리

<br><br>

## Test 영상 Python으로 출력


















### Python으로 영상 제어

<br>

### Python으로 영상 중간에서 틀기

<br>

### Python으로 소리 출력

<br>

### Python으로 소리 이미지화

<br>

### Python으로 소리 실시간 이미지화

<br>

### 최적화

<br>

## 2. 영상 편집

<br>

### 소리 일정부분 이상 감지

<br>

### 영상 자르기

<br>

### 최적화

<br>

## 3. 영상 출력

<br>

### 영상 내보내기


### 참조

- [VScode Jupyter NoteBooks 실행 방법](https://junglow9.tistory.com/10)
- [OpenCV install](https://hello-bryan.tistory.com/124)