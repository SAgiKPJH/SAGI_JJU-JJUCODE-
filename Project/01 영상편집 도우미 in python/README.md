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
- [x] 2. 소리부분 추출
  - [x] 소리부분 추출 최종 목적
  - [x] 소리 파형 이미지화 방법
  - [x] librosa를 통한 wav 파일 파형 시각화
  - [x] moviepy를 통한 mp4 > mp3 파일 변환
  - [x] pydub를 통한 mp3 > wav 파일 변환
  - [x] Python으로 소리 이미지 출력
- [x] 3. 소리영역 획득
  - [x] Python으로 소리 이미지 그래프 제어
  - [x] Python 소리 이미지 그래프 가공
  - [x] Python 소리 영역 획득
- [x] 4. 영역 자르기
  - [x] 자르는 시간 영역 획득
  - [x] 시간 정보를 토대로 한 영상 자르기 및 내보내기
- [x] 5. 영상 추출 성능
  - [x] 영상 추출 성능 측정
  - [x] 영상 추출 성능 검증
  - [x] 영상 추출 기능 개선
- [x] 6. 영상 최종 출력
  - [x] VLC 활용한 영상 순서대로 출력
  - [x] VLC 영상 반복 및 삭제 기능 구현
  - ~~[ ] 영상 병합 및 내보내기~~
  

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
  <img src="https://user-images.githubusercontent.com/66783849/194721385-2f614025-e7b6-4c05-87c9-689d578b681d.png" width="70%">
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

### 소리부분 추출 최종 목적

[![image](https://user-images.githubusercontent.com/66783849/194329336-88881e70-e5e2-4ccd-9b13-fd0c962c4295.png)](https://nachwon.github.io/faster-waveform/) (이미지 출처 : https://nachwon.github.io/faster-waveform/)
- 최종적인 목적은, 소리의 크기를 시간대별로 획득 할 수 있어야 한다.
- 이는 소리를 이미지화를 이룸으로써 위 문제도 해결할 수 있는 준비를 갖출 수 있다.
- 이를 위해서 소리를 이미지화 할 수 있고, 제어를 할 수 있는 python 라이브러리를 찾아본다.

<br>

### 소리 파형 이미지화 방법

- 찾아본 결과 librosa 라이브러리를 통해 wav 파일의 파형을 시각화 할 수 있다.
- 이를 위해서 pydub를 통해 mp3를 wav 파일로 변환한다.
- mp4 파일을 mp3로 변환하기 위해 moviepy 라이브러리를 사용한다.
  ```mermaid
  flowchart LR
  A(("mp4"))--moviepy-->B(("mp3"))--pydub-->C(("wav"))--librosa-->D("파형 이미지 획득")
  ```

<br>

### librosa를 통한 wav 파일 파형 시각화

<img src="https://user-images.githubusercontent.com/66783849/194331548-49e7d65b-4b2c-4abd-872e-c57228ec1c15.png" width="250">  

- 소리 추출을 위해서, 소리 관련 python 라이브러리인 librosa를 사용한다.  
  `pip install librosa`
- librosa를 사용하기 위해서 기본적으로 ffmepg를 설치해야 한다.  
  `pip install ffmpeg-python`
- 이후 다음과 같이 코드를 작성하여, 문제가 없는지를 확인한다.
  ```python
  import numpy as np
  import librosa, librosa.display 
  import matplotlib.pyplot as plt
  ```
- 문제가 없으면 다음 코드를 통해 이미지화한다.
  ```python
  filepath = "D:/test/영상1.wav"
  
  sig, sr = librosa.load(filepath, sr=22050)
  
  plt.figure(filepath)
  librosa.display.waveshow(sig, sr, alpha=0.5)
  plt.xlabel("Time (s)")
  plt.ylabel("Amplitude")
  plt.title("Waveform")
  ```
- 결과는 다음과 같다.  
  <img src="https://user-images.githubusercontent.com/66783849/194332742-986e4352-1ad1-4797-a10e-f75ba8c56908.png" width="300">
- 시간대 별로 소리크기를 확인할 수 있다.

<br>

### moviepy를 통한 mp4 > mp3 파일 변환

- wav 파일을 통해 파형 이미지를 획득할 수 있다.
- mp4를 wav 파일로 변환하기 위한 라이브러리는 찾기 힘들다.
- mp3를 wav 파일로 변환하는 pydub라는 라이브러리가 존재하기에, mp4를 mp3로 변환하는 라이브러리를 찾았다.
- mp4를 mp3로 변환할땐, moviepy를 활용한다.
  ```mermaid
  flowchart LR
  A(("mp4"))--moviepy-->B(("mp3"))--pydub-->C(("wav"))--librosa-->D("파형 이미지 획득")
  ```
- mp4 to mp3 변환을 위해서, python 라이브러리인 moviepy를 사용한다.
- 다음 내용을 Terminal에 입력하여 moviepy를 설치한다.  
  `pip install moviepy`
- 이후 다음과 같이 코드를 작성하여, 문제가 없는지를 확인한다.
  ```python
  import moviepy.editor as mp
  ```
- 문제가 없으면 다음 코드를 통해 변환한다.
- [📌주의] 반드시 파일 이름은 영문으로 작성한다.
  ```python
  clip = mp.VideoFileClip("movie.mp4")
  clip.audio.write_audiofile("movie.mp3")
  ```
- 결과는 다음과 같다.  
  <img src="https://user-images.githubusercontent.com/66783849/194336277-5de6fae8-f592-436e-9c31-39903b9491dc.png" width="300">
- 직접 소리 파일을 재생하여, 문제가 없는지 확인한다.

<br>

### pydub를 통한 mp3 > wav 파일 변환

- mp3 to wav 변환을 위해서, python 라이브러리인 pydub를 사용한다.
- 다음 내용을 Terminal에 입력하여 pydub를 설치한다.  
  `pip install pydub`
- librosa를 사용하기 위해서 기본적으로 ffmepg를 설치해야 한다.  
  `pip install ffmpeg-python`
- 이후 다음과 같이 코드를 작성하여, 문제가 없는지를 확인한다.
  ```python
  import pydub                    # 생략 가능
  from pydub import AudioSegment
  import ffmpeg
  ```
- 문제가 없으면 다음 코드를 통해 변환한다.
- [📌주의] 반드시 파일 이름은 영문으로 작성한다.
  ```python
  clip = mp.VideoFileClip("movie.mp4")
  clip.audio.write_audiofile("movie.mp3")
  ```
- [‼FileNotFoundError 발생시]
  - 다른 환경에서 이상없이 작동하는지 확인한다.
  - [Colab에서는 무사히 작동한다]  
    <img src="https://user-images.githubusercontent.com/66783849/194721125-3980b0fc-7520-4a13-98c4-87e85e53642d.png" width="60%">  
  - ffmpeg를 설치하여 환경을 구성한다.
  - [ffmpeg 설치 참고 출처](https://digital-play.tistory.com/104#google_vignette)
    1. [ffmpeg](https://ffmpeg.org/) 사이트에서 Download를 진행한다.  
       <img src="https://user-images.githubusercontent.com/66783849/195105487-57d6f676-1c5d-4d14-acdf-1cdc758b66d5.png" width="400">  
       - ffmpeg 사이트 -> Download -> 아래 Window 마크 링크 -> Release 버전 압축파일(essentials 또는 Full버전)을 다운받는다.
    2. 다운로드 된 압축파일을 c드라이브(메인드라이브)에 "ffmpeg"라는 폴더명 안에 푼다.
    3. 윈도우의 "명령 프롬프트"를 관리자 권한으로실행한다.  
       <img src="https://user-images.githubusercontent.com/66783849/194721930-cb3f04c4-3dd5-4c36-99fb-3275dc7ff0a2.png"> 
    4. 다음 내용을 입력한다.
       ```bash
       setx /m PATH "C:\ffmpeg\bin;%PATH%"
       ```
    5. 컴퓨터 재시작 후 ffmpeg가 제대로 동작하는지 확인한다.
       ```bash
       ffmpeg -version
       ```
       <img src="https://user-images.githubusercontent.com/66783849/195109101-0ed837dc-5042-4d03-b768-60172c6802ac.png" width="300">
- 결과는 다음과 같다.  
  <img src="https://user-images.githubusercontent.com/66783849/195109974-14b06b4c-7d66-4136-a65d-8557c1ecadb9.png" width="300">  
- 직접 소리 파일을 재생하여, 문제가 없는지 확인한다.  
  <img src="https://user-images.githubusercontent.com/66783849/195110267-f02c8cf2-8ec6-485a-8729-0d2dfe7149a6.png" width="200">  

<br>

### Python으로 소리 이미지 출력

- moviepy, pydub, librosa를 활용하여 mp4 영상의 소리를 추출하여 크기를 시간대별 시각화한다.
  ```python
  InputFileName = "edit"

  print("Start Converting mp4 to mp3...")
  # mp4 to mp3
  import moviepy.editor as mp
  
  clip = mp.VideoFileClip(InputFileName+".mp4")
  clip.audio.write_audiofile(InputFileName+".mp3")
  
  print("Start Converting mp3 to wav...")
  # mp3 to wav
  import pydub
  from pydub import AudioSegment
  import ffmpeg
  
  audSeg = AudioSegment.from_mp3(InputFileName+".mp3")
  audSeg.export(InputFileName+".wav", format="wav", bitrate=16)
  
  print("Start making Visualization wav...")
  
  # wav to Visualization
  import numpy as np
  import librosa, librosa.display 
  import matplotlib.pyplot as plt
  
  filepath = InputFileName+".wav"
  
  sig, sr = librosa.load(filepath, sr=22050)
  
  plt.figure(filepath)
  librosa.display.waveshow(sig, sr, alpha=0.5)
  plt.xlabel("Time (s)")
  plt.ylabel("Amplitude")
  plt.title("Waveform")
  ```
- 결과는 다음과 같다.  
  <img src="https://user-images.githubusercontent.com/66783849/195115662-f753e7a6-9c5b-4bbc-8e72-b76dc971093e.png" width="190">  
- 8.2초 영상의 소리를 변환하는데, 7.5초가 경과하였다.
- 이를 토대로 함수화를 진행한다.
  ```python
  # mp4 to mp3
  import moviepy.editor as mp
  # mp3 to wav
  import pydub
  from pydub import AudioSegment
  import ffmpeg
  # wav to Visualization
  import numpy as np
  import librosa, librosa.display 
  import matplotlib.pyplot as plt
  
  def getSoundVolume(name, sr) : 
      # mp4 to mp3
      print("Start Converting mp4 to mp3...")
      clip = mp.VideoFileClip(name+".mp4")
      clip.audio.write_audiofile(name+".mp3")
      # mp3 to wav
      print("Start Converting mp3 to wav...")
      audSeg = AudioSegment.from_mp3(name+".mp3")
      audSeg.export(name+".wav", format="wav", bitrate=16)
      # wav to Visualization
      print("Start making Visualization wav...")
      filepath = name+".wav"
      sig, sr = librosa.load(filepath, sr)
      return sig, sr
  ```
- 다음과 같이 활용한다.
  ```python
  InputFileName = "edit"
  sig, sr = getSoundVolume(InputFileName, 2000)
  ```
- 8.2초 영상의 소리를 획득하는데, 1.3초가 경과하였다.
- 다음과 같이 이미지 출력을 함수화 한다.
  ```python
  def drawSoundImage(sig, sr) :
      librosa.display.waveshow(sig, sr, alpha=0.5)
      plt.xlabel("Time (s)")
      plt.ylabel("Amplitude")
      plt.title("Waveform")
  ```
- 다음과 같이 활용한다.
  ```python
  drawSoundImage(sig, sr)
  ```
  <img src="https://user-images.githubusercontent.com/66783849/195143712-88859f77-a431-44e7-bd61-8c1a8e8f3d6f.png" width="190">  


<br>

## 3. 소리영역 획득

- 원하는 소리 영역을 감지하기 위해 소리정보를 가공하여 다룬다.

<br>

### Python으로 소리 이미지 그래프 제어

- librosa 함수를 사용할 때 각 설정들은 다음과 같은 뜻을 갖고 있다.
  - param sr : 1초당 분해수이다.
  - sig : 분해단위당 볼륨크기 np 배열
  - sig.size : 총 분해단위 수
  - sig.size / sr : 총 분해단위수 / 1초 분해단위수 = 영상 길이(초)
  - 1/sr : 분해단위의 길이
- 다음 함수를 통해 일반 출력을 진행한다.
  ```python
  import numpy as np
  import librosa, librosa.display 
  import matplotlib.pyplot as plt
  
  filepath = InputFileName+".wav"
  dsecs = 2000
  
  sig, sr = librosa.load(filepath, sr=dsecs)
  
  plt.figure(filepath)
  librosa.display.waveshow(sig, sr, alpha=0.5)
  plt.xlabel("Time (s)")
  plt.ylabel("Amplitude")
  plt.title("Waveform")
  ```
  <img src="https://user-images.githubusercontent.com/66783849/195143712-88859f77-a431-44e7-bd61-8c1a8e8f3d6f.png" width="250">
- 다음 함수를 통해 절댓 값 출력을 진행한다.
  ```python
  import matplotlib.pyplot as plt

  plt.plot(np.arange(0., sig.size/dsecs, 1/dsecs), abs(sig))
  ```
  <img src="https://user-images.githubusercontent.com/66783849/195144477-91398340-8103-4803-bab9-69135c48e7f8.png" width="250">
- 다음 코드를 통해 적분 값을 가져온다.
  ```python
  import matplotlib.pyplot as plt
  import copy
  
  plt.plot(np.arange(0., sig.size/dsecs, 1/dsecs), abs(sig))
  
  sig1 = copy.deepcopy(sig)
  
  for i in range(1, sig.size) :
      sig1[i]=0
      sig1[i] = sig1[i-1] +  abs(sig[i])
  
  plt.plot(np.arange(0., sig.size/dsecs, 1/dsecs), sig1)
  plt.show()
  ```
  <img src="https://user-images.githubusercontent.com/66783849/195145067-6847f25f-379e-4ebc-a622-cd07957d4371.png" width="250">

<br>

### Python 소리 이미지 그래프 가공

- 다음 코드를 통해 일정한 범위의 적분을 가져온다.
  ```python
  import matplotlib.pyplot as plt

  plt.plot(np.arange(0., sig.size/dsecs, 1/dsecs), abs(sig))
  
  sig1 = copy.deepcopy(sig)
  n = 1 # 측정 범위 1초
  dd = dsecs * n
  
  for i in range(1, sig.size-1, dd) :
      sig1[i] = 0
      for j in range(0, int(dd)) :
          a = 0
          if i+(j-dd/2) < 0 or i+(j-dd/2) >= sig.size:
              a = 0
          else :
              a = sig[int(i+(j-dd/2))]
          sig1[i] += abs(a)
  
  plt.plot(np.arange(0., sig.size/dsecs, 1/dsecs), sig1/dd)
  
  plt.show()
  ```
  <img src="https://user-images.githubusercontent.com/66783849/195145500-f14e7c33-3fda-4dfa-a771-3ac00875899d.png" width="250">
- 8.2초의 소리를 가공하여 0.6초 안에 정보를 획득했다.
- 최종적으로 다음과 같은 코드로 작성한다.
  ```python
  import matplotlib.pyplot as plt
  import copy
  
  plt.plot(np.arange(0., sig.size/dsecs, 1/dsecs), abs(sig))
  
  sig1 = np.zeros(1)
  
  n = 0.7 # 측정 범위 1초
  dd = dsecs * n
  
  for i in range(1, sig.size-1, int(1000*n/4)) :
      k = 0
      for j in range(0, int(dd)) :
          a = i+(j-dd/2)
          if not(a < 0 or a >= sig.size):
              k += abs( sig[int(a)] )
      sig1 = np.insert(sig1, -1 , k )
          
  
  plt.plot(np.arange(0., (sig.size+200)/sr, 1*((sig.size+200)/sr/sig1.size)), sig1/dd)
  
  plt.show()
  ```
  <img src="https://user-images.githubusercontent.com/66783849/195611365-263a0e9c-1c28-4014-bee8-e04b86b9aecd.png" width="300">
- 8.2초의 소리를 가공하여 0.5초 안에 정보를 획득했다.
- 이 정보를 토대로 함수화를 진행한다.
  ```python
  def getSoundIntegral(sig, sr, dsec, n = 1) : 
      sig1 = np.zeros(1)
      dd = dsecs * n
  
      for i in range(1, sig.size-1, int(1000*n/4)) :
          k = 0
          for j in range(0, int(dd)) :
              a = i+(j-dd/2)
              if not(a < 0 or a >= sig.size):
                  k += abs( sig[int(a)] )
          sig1 = np.insert(sig1, -1 , k )
      
      return sig1, dd
  ```
- 다음과 같이 활용한다.
  ```python
  import matplotlib.pyplot as plt
  import copy
  
  sig1, dd = getSoundIntegral(sig, sr, dsec, 1)
  ```
- 다음과 같이 이미지화를 구성한다.
  ```python
  def drawGraphVolume(sig1, dd) :
      plt.plot(np.arange(0., sig1.size, 1), sig1/dd)
      plt.show()
  ```
- 다음과 같이 활용한다.
  ```python
  drawGraphVolume(sig1, dd)
  ```
  <img src="https://user-images.githubusercontent.com/66783849/195618099-1bd84a87-1c24-4a0e-a0a3-7600a196742a.png" width="250">


### Python 소리 영역 획득

- 소리의 범위를 구하기 위해서는, 소리 검출 영역의 시작점과 끝점을 획득할 수 있어야 한다.
- 소리 크기의 0.0025 부분을 기준으로 영역을 검출한다.
  <img src="https://user-images.githubusercontent.com/66783849/195636012-933259de-6e74-4e97-9dc3-4a6bcab98746.png" width="250">
- 우선 0.0025 이하인 영역을 검출한다.
  ```python
  for i in range(0, sig1.size) :
      if( sig1[i]/dd < 0.0025 ) :
          print(i)
  ```
- 결과는 다음과 같다.
  ```bash
  0 1 31 45 46 47 48 49 50 51 52 53 54 66
  ```
- 이러한 결과가 다음과 같이 출력 될 수 있도록 Python 코드를 구현한다.
  ```bash
  1 31
  31 45
  54 66
  ```
  ```python
  a = 0
  for i in range(0, sig1.size) :
      if( sig1[i]/dd < 0.0025 ) :
          if ( a + 1 == i ):
              a = i
          if ( i - a > 1 ) :
              print(a, ", ", i)
              a = i
  ```
- 결과는 다음과 같다.
  ```bash
  1 ,  31
  31 ,  45
  54 ,  66
  ```
- 이를 np.array 배열로 묶는다.
  ```python
  k = [np.zeros(2)]
  
  a = 0
  for i in range(0, sig1.size) :
      if( sig1[i]/dd < 0.0025 ) :
          if ( a + 1 == i ):
              a = i
          if ( i - a > 1 ) :
              k = np.append(k, [[a, i]], axis = 0)
              a = i
  k = np.delete(k, 0, axis=0)
  k
  ```
- 결과는 다음과 같다.
  ```bash
  array([[ 1., 31.],
         [31., 45.],
         [54., 66.]])
  ```
- 이러한 결과를 함수화 한다.
  ```python
  def getRangeVolume(sig1, v = 0.0025) :
      k = [np.zeros(2)]
  
      a = 0
      for i in range(0, sig1.size) :
          if( sig1[i]/dd < 0.0025 ) :
              if ( a + 1 == i ):
                  a = i
              if ( i - a > 1 ) :
                  k = np.append(k, [[a, i]], axis = 0)
                  a = i
      return np.delete(k, 0, axis=0)
  ```
- 코드를 다음과 같이 개선하였다.
  ```python
  def getRangeVolume(sig1, v = 0.0025) :
      k = [np.zeros(2)]
  
      a = 0
      b = False
      for i in range(0, sig1.size) :
          if( sig1[i]/dd < v ) :
              if ( b ):
                  k = np.append(k, [[a, i]], axis = 0)
                  b = False
          else : 
              if ( not(b) ) :
                  a = i
                  b = True
      return np.delete(k, 0, axis=0)
  ```
- 다음과 같이 활용한다.
  ```python
  k = getRangeVolume(sig1, 0.0025)
  ```

<br>



<br><br>

## 4. 영상 자르기

### 자르는 시간 영역 획득

- 소리 영역 획득을 토해 얻은 소리의 시작 위치와 끝 위치를 시간 단위로 변환한다.
  ```python
  print("추출 Volume 길이 : ", sig1.size)
  print("총 영상 길이", sig.size)
  print("원본 영상 시간", sig.size/sr, "s")
  print(sig.size/sr, "초 동안", sig1.size, "개의 정보가 존재")
  print("초당", sig1.size/(sig.size/sr), "개가 존재해야 한다")
  print(sig.size/sr, "x", sig1.size/(sig.size/sr), "=", (sig.size/sr)*(sig1.size/(sig.size/sr)) )
  print(sig.size/sr, "초 동안", sig1.size, "개의 정보")
  print("추출 Volume 길이 1당", (sig.size/sr)/sig1.size )
  print("추출 Volume 길이 1이",sig1.size, "개 있으면")
  print( (sig.size/sr)/sig1.size, "x", sig1.size, "=", sig1.size*(sig.size/sr)/sig1.size  )
  ```
- 결과는 다음과 같다.
  ```bash
  추출 Volume 길이 :  67
  총 영상 길이 16400
  원본 영상 시간 8.2 s
  8.2 초 동안 67 개의 정보가 존재
  초당 8.170731707317074 개가 존재해야 한다
  8.2 x 8.170731707317074 = 67.0
  8.2 초 동안 67 개의 정보
  추출 Volume 길이 1당 0.12238805970149252
  추출 Volume 길이 1이 67 개 있으면
  0.12238805970149252 x 67 = 8.2
  ```
- 소리 영역 획득을 토해 얻은 소리의 시작 위치와 끝 위치를 시간 단위로 변환한다.
  ```python
  k *= (sig.size/sr)/sig1.size
  k
  ```
- 결과는 다음과 같다.
  ```bash
  array([[0.12238806, 3.79402985],
         [3.79402985, 5.50746269],
         [6.60895522, 8.07761194]])
  ```

<br>

### 시간 정보를 토대로 한 영상 자르기 및 내보내기

- 영상을 자르기 위해서는 moviepy에서 제공하는 자르기 기능을 활용한다.
- 다음을 통해 영상을 시작초-끝초를 지정하여 영상을 자른다.
  ```python
  from moviepy.video.io import ffmpeg_tools
  
  # 0초 부터 1.5초 까지 자른다. 
  ffmpeg_tools.ffmpeg_extract_subclip(InputFileName+".mp4", 0, 1.5, targetname=InputFileName+"_Out.mp4")
  ```
- 다음을 통해 자르는 시간 영역 획득 결과를 대입하여 추출해본다.
  ```python
  from moviepy.video.io import ffmpeg_tools
  
  a = 0
  for i in k :
      a+=1
      ffmpeg_tools.ffmpeg_extract_subclip(InputFileName+".mp4", i[0], i[1], targetname=InputFileName+str(a)+"_Out.mp4")
  ```
- 함수화를 진행한다.
  ```python
  def exportVideo(InPath, InputFileName, OutPath, k) :
      a = 0
      for i in k :
          a+=1
          ffmpeg_tools.ffmpeg_extract_subclip(InPath+InputFileName+".mp4", i[0], i[1], targetname=OutPath+InputFileName+str(a)+"_Out.mp4")
  ```
- 다음과 같이 활용한다.
  ```python
  exportVideo("", "edit", "OutPut/", k)
  ```
  <img src="https://user-images.githubusercontent.com/66783849/195652992-239064f2-bfac-43b7-9daf-cceca43bc517.png" width="250">

## 5. 영상 추출 성능

### 영상 추출 성능 측정

#### 8.2초짜리 영상

- 제작한 코드의 성능을 측정한다.
1. import 과정 ------ (10.8s)
2. 함수 등록 -------- ( 0.8s)
3. 영상 wav 획득 ---- ( 3.8s) (8.2s 영상 input)
4. drawSoundImage --- ( 1.1s)
5. getSoundIntegral - ( 0.2s) (8.2s 영상 input)
6. drawGraphVolume -- ( 0.4s)
7. getRangeVolume --- ( 0.8s)
8. exportVideo ------ ( 0.5s) (8.2s 영상, 3 영역)
- 총 18.4s 소요
- input 영상의 2.24배 소요

#### 77s초짜리 영상

- 제작한 코드의 성능을 측정한다.
1. import 과정 ------ ( 7.2s)
2. 함수 등록 -------- ( 0.1s)
3. 영상 wav 획득 ---- ( 9.2s) (77s 영상 input)
4. drawSoundImage --- ( 0.8s)
5. getSoundIntegral - ( 1.1s) (77s 영상 input)
6. drawGraphVolume -- ( 0.5s)
7. getRangeVolume --- ( 0.8s)
8. exportVideo ------ ( 1.3s) (8.2s 영상, 3 영역)
- 총 21s 소요
- input 영상의 0.27배 소요

#### 14155s초짜리 영상

- 제작한 코드의 성능을 측정한다.
1. import 과정 ------ (    7.2s)
2. 함수 등록 -------- (    0.1s)
3. 영상 wav 획득 ---- ( 1044.4s) (14155s 영상 input) (17m24.4s)
4. drawSoundImage --- (   1.1s)
5. getSoundIntegral - ( 131.9s) (14155s 영상 input) (2m11.9s)
6. drawGraphVolume -- ( 0.2s)
7. getRangeVolume --- ( 0.5s)
8. exportVideo ------ ( 8.1s) (8.2s 영상, 3 영역)
- 총 1193.5s 소요
- input 영상의 0.084배 소요


### 영상 추출 성능 검증

- 검출 길이 1s, 3s 확인
- 다른 영상도 소리 추출 잘 됨을 확인

<br>

### 영상 추출 기능 개선

- 영상추출을 시도하면서 생기는 문제 또는 개선점을 해결한다.
- 이미 wav파일로 변환하여, mp4 -> wav 파일로 변환하는 작업을 생략할 때
  ```python
  def getWaveVolume(name, sr) :
      # wav to Visualization
      print("Start making Visualization wav...")
      filepath = name+".wav"
      sig, sr = librosa.load(filepath, sr)
      return sig, sr
  ```
  ```python
  # 이미 Wav 파일이 존재할 시
  InputFileName = "video_14155_"
  dsec = 2000
  sig, sr = getWaveVolume(InputFileName, dsec)
  ```
- getGraphVolume() 함수의 일부분만 확대하여 볼 때
  ```python
  print(sig1.size)
  cut = 42700  # sig1.size의 크기에 맞게끔 구성한다.
  plt.plot(np.arange(0., sig1.size-cut, 1), sig1[0:-cut]/dd)
  plt.show()
  ```
- getRangeVolume() 코드를 다음과 같이 개선하였다.
  ```python
  def getRangeVolume(sig1, v = 0.0025) :
      k = [np.zeros(2)]
  
      a = 0
      b = False
      for i in range(0, sig1.size) :
          if( sig1[i]/dd < v ) :
              if ( b ):
                  k = np.append(k, [[a, i]], axis = 0)
                  b = False
          else : 
              if ( not(b) ) :
                  a = i
                  b = True
      return np.delete(k, 0, axis=0)
  ```

<br><br>


## 6. 영상 최종 출력

- 최종 추출된 영상을 빠르게 순서대로 확인하고, 쉽게 삭제 저장여부를 선택할 수 있도록 한다.
- 필요하면 병합을 할 수 있도록 한다.

### VLC 활용한 영상 순서대로 출력

- 추출된 영상을 순서대로 출력하는 코드를 짜본다.
  ```python
  import vlc
  import time
  ```
  ```python
  InputPath = "OutPut/"
  InputFileName = "video_14155_"
  a = 1
  
  # 영상 끝까지 재생 후 종료
  media_player = vlc.MediaPlayer()
  
  media_player.event_manager().event_attach(
      vlc.EventType.MediaPlayerStopped, my_call_back)
  
  # Event
  def my_call_back(event):
      print("콜백함수호출: 종료호출")
      global status 
      status = 1 
  
  
  while(a<785) : 
  
      # Setting
      media_player.set_media(
          vlc.Media(
              InputPath+InputFileName+str(a)+"_Out.mp4"
          )
      )
      media_player.video_set_scale(0.8)
      media_player.play()
  
      # 자동 종료
      status = 0
      while (status == 0):
          time.sleep(0.3)
          if status == 1:
              media_player.stop()
              a+=1
              print(a)
          else:
              pass
  ```

<br>

### VLC 영상 반복 및 삭제 기능 구현

- 영상 반복 재생 또는 영상 삭제 기능을 키보드를 통해 쉽게 제어할 수 있도록 한다.
- 키보드 입력을 받기 위해서 다음 라이브러리를 활용한다.
  ```bash
  pip install keyboard
  ```
  ```python
  import keyboard

  while True:
      if keyboard.is_pressed("1"):
          print("hello")
          break
  ```
- R 버튼(다시 재생)과 D 버튼(삭제), N 버튼(다음 영상), P 버튼(이전 영상) 입력받을 수 있도록 구현한다.
  ```python
  while True:
      if keyboard.is_pressed("r"):
          print("replay")
          break
      if keyboard.is_pressed("d"):
          print("delete")
          break
      if keyboard.is_pressed("n"):
          print("next Video")
          break
      if keyboard.is_pressed("p"):
          print("prev Video")
          break
  ```
- 영상을 삭제하기 위해서 다음과 같이 활용한다.
  ```python
  InputPath = "OutPut/"
  InputFileName = "video_14155_"
  a = 784
  os.remove(InputPath+InputFileName+str(a)+"_Out_test.mp4")
  ```
- 이를 종합하여 VLC 영상 간편 추출 도우미를 구성한다.
  ```python
  InputPath = "OutPut/"
  InputFileName = "video_14155_"
  a = 1
  
  # 영상 끝까지 재생 후 종료
  media_player = vlc.MediaPlayer()
  
  # Event
  def my_call_back(event):
      print("콜백함수호출: 종료호출")
      global status 
      status = 1 
  
  media_player.event_manager().event_attach(
      vlc.EventType.MediaPlayerStopped, my_call_back)
  
  while(a<785) : 
  
      # Setting
      media_player.set_media(
          vlc.Media(
              InputPath+InputFileName+str(a)+"_Out.mp4"
          )
      )
      media_player.video_set_scale(0.8)
      media_player.play()
  
      # 자동 종료
      status = 0
      while (status == 0):
          time.sleep(0.3)
          if status == 1:
              media_player.stop()
              while True:
                  if keyboard.is_pressed("r"):
                      print("replay : ", a)
                      break
                  if keyboard.is_pressed("d"):
                      print("delete : ", a)
                      a += 1
                      media_player.set_media(
                          vlc.Media(
                              InputPath+InputFileName+str(a)+"_Out.mp4"
                          )
                      )
                      os.remove(InputPath+InputFileName+str(a-1)+"_Out.mp4")
                      print("next : ", a)
                      break
                  if keyboard.is_pressed("n"):
                      a += 1
                      print("next : ", a)
                      break
                  if keyboard.is_pressed("p"):
                      a -= 1
                      print("prev : ", a)
                      break
          else:
              pass
  ```


<br>

<br><br>



## 결과
- 8.2초 영상의 소리를 이미지 정보로 변환하는데, 7.5초가 경과하였다.
  - 8.2초 영상의 소리를 획득하는데, 1.3초가 경과하였다.
- 8.2초의 소리를 가공하여 0.6초 안에 정보를 획득했다.

  

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
- mp4 to mp3
  - [파이썬을 이용해 동영상에서 오디오 추출하기](https://codingnuri.com/extracting-audio-from-video-using-python/)
- ffmpeg
  - [[파이썬 활용] ffmpeg 설치하기](https://digital-play.tistory.com/104#google_vignette)
- ffmpeg
  - [ffmpeg 다운로드와 간단한 사용 방법](https://seogilang.tistory.com/1578)
- plt
  - https://wikidocs.net/92071
- matlab
  - https://wikidocs.net/92071
- python 문법
  - [조건문 if else](https://wikidocs.net/57)
  - [and or 연산](https://wikidocs.net/22211)
  - [얕은 복사, 깊은 복사](https://blockdmask.tistory.com/576)
- np
  - [넘파이(NumPy) 기초: 배열 및 벡터 계산](https://compmath.korea.ac.kr/appmath/NumpyBasics.html)
  - [넘파이 알고 쓰자 - 넘파이의 원소 제거 및 추가(delete, add)](https://everyday-image-processing.tistory.com/93)
- 파일 삭제
  - [Python 파일 및 디렉토리 삭제하는 방법](https://webisfree.com/2018-03-16/python-%ED%8C%8C%EC%9D%BC-%EB%B0%8F-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC-%EC%82%AD%EC%A0%9C%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95)