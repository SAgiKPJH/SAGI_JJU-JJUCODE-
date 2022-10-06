문서정보 : 2022.09.20.~ 작성, 작성자 [@SAgiKPJH](https://github.com/SAgiKPJH)

<br>

# [프로젝트 1] 영상편집 도우미 in python

## 동작 과정

<img src="https://user-images.githubusercontent.com/66783849/193836128-56ef19bd-c711-46f6-99ee-5255ed431100.png" width="80%">

<br>

## 목적
- 영상편집을 할 때, 핵심부분만 따로 추출하는 프로그램을 만드는 목적

```mermaid
flowchart LR
Z["프로그램 시작"]--1. 입력--> A["동영상"] --->B_1["영상 부분"]--->C
A --2. 소리 분해--> B_2["소리 부분"]
B_2 --3. 소리 영역 감지-->B_2 --4. 영역 자르기--> C["추출된 영상"]
C --5. 영상 추출 <br>및 내보내기-->D["저장된<br> 추출된 영상"] --6. 영상 병합-->E["편집영상"]
```

## 목표

- [x] 0. 환경 구성
  - [x] Python 환경 기본 구성
  - [x] 설치된 Python, pip VScode에 연결하기
  - [x] VLC 미디어 재생기
  - [x] Test 영상 선정
- [x] 1. 영상 입력
  - [x] 영상 정보 획득
  - [x] Python-VLC로 영상 실행 제어
  - [x] Python-VLC 영상 재생 표준
  - [x] Python-VLC 소리 정보 시각화
- [ ] 2. 소리부분 추출
  - [ ] Python으로 소리 실시간 이미지화
- [ ] 3. 소리영역 감지
  - [ ] Python으로 소리 크기 획득
  - [ ] 소리 일정부분 이상 감지
- [ ] 4. 영역 자르기
  - [ ] 영상 자르기
- [ ] 5. 영상 추출 및 내보내기
  - [ ] 영상 내보내기
- [ ] 6. 영상 병합 작업 및 내보내기
  - [ ] 영상 내보내기
  - [ ] 최적화

### 제작 기간
- 09/20 (화) ~

### 제작자
[@SAgiKPJH](https://github.com/SAgiKPJH)


---

<br><br><br>

## 0. 환경 구성

### Python 환경 기본 구성

- Python 설치
  - Python 사이트를 통해 최신 버전을 설치한다.
- VScode
  - Python은 VScode를 통해 구현한다.
  - VScode에 Python을 설치한다.
- Jupyter Nodebook
  - Jupyter Nodebook을 통해 단계별 과정을 실험한다.
  - Python으로 영상을 다루는 방법을 알기 위해 VScode에 jupyter를 설치하고 실행한다.
  - 설치 후 [View] > [Command Palette...(명령 팔레트...)] > ">create" 입력 > [Python: Create New Black Jupyter Notebook] 클릭 > Jupyter Notebook을 생성한다.

<br>

### 설치된 Python, pip VScode에 연결하기

- VScode에 설치된 pip와 python을 연결한다.
  - python 위치 획득
    - 설치된 Python 프로그램 위치에 이동한다.
    - 윈도우 > python 검색 > python 3.10 파일의 위치 열기 > python 위치 획득
    - 파일 위치 예) C:\Users\UserName\AppData\Local\Programs\Python\Python310\
  - pip 위치 획득
    - python 폴더 > Scripts 폴더 > pip 및 pip3가 존재함을 확인
    - 파일 위치 예) C:\Users\UserName\AppData\Local\Programs\Python\Python310\Scripts\
  - 윈도우 > 고급 시스템 설정 보기 검색 후 실행 > 시스템 속성 창 > 환경 변수 > [UserName에 대한 사용자 변수]와 [시스템 변수]에 존재하는 path > Python 폴더위치 및 pip 폴더 위치를 등록한다.  
  <img src="https://user-images.githubusercontent.com/66783849/191776092-86e1c0a4-2aab-4ccb-b85b-73366a0541cc.png" width="70%">
- pip가 정삭작동함을 확인한다.
  - Terminal에 pip 명령어의 동작 여부를 확인한다.
<br>

### VLC 미디어 재생기
<img src="https://user-images.githubusercontent.com/66783849/192570998-90b017d4-ac4f-4bb1-8250-8cb800fbcacf.png" width="19%">

- VLC 미디어 플레이어(VLC media player)는 비디오랜(VideoLAN) 프로젝트가 개발한 자유-오픈 소스 미디어 플레이어 소프트웨어이다.
- VLC는 데스크톱 운영 체제, 그리고 안드로이드, iOS, iPadOS, 타이젠, 윈도우 10 모바일, 윈도우 폰 등 모바일 플랫폼용으로 내려받을 수 있다.
- 비디오랜 소프트웨어는 1996년 학술 프로젝트의 하나로서 기원하였다.
- [VLC 미디어 플레이어 사이트](https://www.videolan.org/vlc/)를 통해 VLC 미디어 플레이어를 다운 받는다.
- "pip3 install python-vlc"를 통해 파이썬에 설치한다.
- 다음 코드를 실행하여 문제가 없음을 확인한다.
  ```python
  import vlc
  ```
<br>

### Test 영상 선정

<img src="https://user-images.githubusercontent.com/66783849/193837616-6d2d25f6-a184-4b93-90ed-3a73054d6106.png">

- 영상 3개 선정
  - 영상 1 : 8초짜리 영상
  - 영상 2 : 1분 17초짜리
  - 영상 3 : 8초 짜리


<br><br><br>

## 1. 영상 입력

- Python으로 영상을 제어할 수 있다.

### 영상 정보 획득

- Python으로 영상을 받아서 실행한다.
- 코드를 다음과 같이 작성한다.
  ```python
  import vlc
  import time
  
  # vlc 미디어 플레이어 객체 생성하기
  media_player = vlc.MediaPlayer()
  
  # 재생할 뮤직비디오 파일을 vlc 모듈의 미디어로 변환.
  media = vlc.Media("영상1.mp4")
  
  # 읽어드린 미디어를 재생할 수 있도록 
  # 미디어 플레이어 객체에 세팅 (재생 준비 상태)
  media_player.set_media(media)
  
  # start playing video
  media_player.play()
  
  # wait so the video can be played for 5 seconds
  # irrespective for length of video
  time.sleep(0.05)
    
  # 비디오 정보 출력
  print("Frame Rate per Second(fps) : ")
  print(media_player.get_fps())
  print("Video Width x Height : ")
  print(str(media_player.video_get_width())
   + " x " +
   str(media_player.video_get_height()) )
  print("Audio Volume : ")
  print(media_player.audio_get_volume())
  print("Video_Length : ")
  print(media_player.get_length()/1000)
  
  media_player.stop()
  media_player.release()
  ```
- 결과는 다음과 같다.
  ```bash
  Frame Rate per Second(fps) : 
  29.87755012512207
  Video Width x Height : 
  1920 x 1080
  Audio Volume : 
  100
  Video_Length : 
  8.197
  ```

<br>

### Python-VLC로 영상 실행 제어
  
- VLC를 이용햐여 영상을 재생하고 정지 및 종료한다.
  ```python
  media_player = vlc.MediaPlayer()
  media = vlc.Media("영상2.mp4")
  media_player.set_media(media)
  
  # 영상 스케일 조정
  media_player.video_set_scale(0.4)
  time.sleep(1)
  print(f"영상 스케일 : {media_player.video_get_scale}이다.")
  
  # 볼륨 조정
  media_player.audio_set_volume(80)
  time.sleep(1)
  print(f"영상 볼륨 : {media_player.audio_get_volume}이다.")
  
  # 영상 1초 일지중지
  media_player.pause()
  time.sleep(1)
  
  # 영상 1초 재생
  media_player.play()
  time.sleep(1)
  
  # 영상 1초 중지
  media_player.stop()
  time.sleep(1)
  
  # 영상 다시 재생
  media_player.play()
  time.sleep(1)
  
  # 영상 위치 지정
  media_player.set_position(0.3) # 30%
  time.sleep(3)
  print(f"  - 영상 재생시간: {media_player.get_time()}")
  print(f"  - 영상 재생위치: {media_player.get_position()}")
  print("\n")
  
  # 영상 배속
  media_player.set_rate(1.5) # 1.5배
  time.sleep(3)
  print(f"  - 현재 재생 속도: {media_player.get_rate()}")
  print("\n")
  media_player.set_rate(1) # 1배
  
  
  # 음소거
  media_player.audio_toggle_mute()
  time.sleep(1)
  value = media_player.audio_get_mute()
  print(f"  - 현재 음소거 상태: {value}")
  print("\n")
   
  # 음소거 해제
  media_player.audio_toggle_mute()
  time.sleep(1)
  value = media_player.audio_get_mute()
  print(f"  - 현재 음소거 상태: {value}")
  print("\n")
   
  # 전체화면 - 영상비율도 같이 바꿔줘야 합니다.
  media_player.video_set_scale(2)
  media_player.set_fullscreen(True)
  time.sleep(1)
  print("  - 현재 Full screen 상태(get_fullscreen): ", media_player.get_fullscreen())
  print("\n")
   
  # 전체화면 해제 - 영상비율도 같이 바꿔줘야 합니다.
  media_player.video_set_scale(0.4)
  media_player.toggle_fullscreen()
  time.sleep(1)
  print("  - 현재 Full screen 상태(get_fullscreen): ", media_player.get_fullscreen())
  print("\n")
  
  # 영상 해제
  media_player.release()
  ```
  <img src="https://user-images.githubusercontent.com/66783849/193841897-9c13b143-3933-4d29-8a1a-23e95ae8494b.png" width="60%">

<br>

### Python-VLC 영상 재생 표준

- 영상이 종료되면 Release()되도록 구성한다.
  ```python
  # 영상 끝까지 재생 후 종료
  media_player = vlc.MediaPlayer()
  
  # Event
  def my_call_back(event):
      print("콜백함수호출: 종료호출")
      global status 
      status = 1 
  media_player.event_manager().event_attach(
      vlc.EventType.MediaPlayerStopped, my_call_back)
  
  # Setting
  media_player.set_media(vlc.Media("영상1.mp4"))
  media_player.video_set_scale(0.2)
  media_player.play()
  
  # 자동 종료
  status = 0
  while True:
      time.sleep(0.3)
      if status == 1:
          media_player.release()
      else:
          pass
  ```

### Python-VLC 소리 정보 시각화

- 소리 정보 시각화를 위해서는 다음 코드를 수정하여 진행한다.
- 옵션 중 `--effect-list=<string>`의 문자열값은 dummy, scope, spectrum, spectrometer, vuMeter 중에 하나의 값을 선택한다.
- `--effect-fft-window` 옵션의 값은 hann, flattop, blackmanharris, kaiser 이 리스트 중 하나의 값을 선택한다.
  ```python
  # media_player = vlc.MediaPlayer()

  instance = vlc.Instance(
      "--audio-visual=visual",
      "--effect-list=spectrum",
      "--effect-fft-window=flattop")
  
  media_player = instance.media_player_new()
  ```
- 다음과 같이 소리 시각화 코드를 구성한다.
  ```python
  # 소리의 시각화
  instance = vlc.Instance(
      "--audio-visual=visual",
      "--effect-list=spectrum",
      "--effect-fft-window=flattop")
  media_player = instance.media_player_new()
  
  # 이벤트
  def my_call_back(event):
      print("콜백함수호출: 종료호출")
      media_player.release()
  media_player.event_manager().event_attach(
      vlc.EventType.MediaPlayerStopped, my_call_back)
  
  # 영상 설정
  media_player.set_media(vlc.Media("영상1.mp4"))
  media_player.video_set_scale(0.2)
  media_player.play()
  ```
- 결과  
  <img src="https://user-images.githubusercontent.com/66783849/192597600-bde11ec7-a014-4339-b488-e5ae3b714edb.png" width="70%">

<br>

## 2. 소리부분 추출 

- 소리 추출을 위해서, 소리 관련 python 라이브러리인 librosa를 사용한다.  
  `pip install librosa`
- librosa를 사용하기 위해서 기본적으로 ffmepg를 설치해야 한다.  
  `pip install ffmpeg-python`

### Python으로 소리부분 추출

### Python으로 소리 실시간 이미지화

### Python-VLC 으로 소리 크기 획득

  

### 참조

- [VScode Jupyter NoteBooks 실행 방법](https://junglow9.tistory.com/10)
- [OpenCV install](https://hello-bryan.tistory.com/124)
- [Python, VScode 연결](https://joy-notes.com/vscode-%ED%8C%8C%EC%9D%B4%EC%8D%AC-pip-%EC%84%A4%EC%B9%98-%EC%9C%88%EB%8F%84%EC%9A%B0%EC%9A%A92022%EB%85%84-%EA%B8%B0%EC%A4%80/)
- [OpenCV VideoCapture, VideoProperty](https://wikidocs.net/28)
- [Python OpenCV VideoCapture](https://scribblinganything.tistory.com/491)
- [Python OpenCV And Audio Player ffpyplayer](https://dreamfuture.tistory.com/10)
- [ffpyplayer](https://pypi.org/project/ffpyplayer/)
- [python-VLC](https://scv-life.tistory.com/111?category=982165)
- 소리 시각화
  - [파이썬 오디오 라이브러리 Top 5종 (Python Audio Library )](https://richwind.co.kr/174)
  - [librosa](https://hyunlee103.tistory.com/36)
  - [librosa Update Error](https://develop247.tistory.com/35)