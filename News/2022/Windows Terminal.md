문서정보 : 2022.10.07.-09. 작성, 작성자 [@SAgiKPJH](https://github.com/SAgiKPJH)


# Windows Terminal

[![image](https://user-images.githubusercontent.com/66783849/194581819-164fa1df-8ff2-4855-8022-50fbc90818e9.png)](https://devblogs.microsoft.com/commandline/windows-terminal-1-0/)

[![image](https://user-images.githubusercontent.com/66783849/194581986-414d091c-fe18-4fd3-adc2-6d7eb20a8c39.png)](https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3D8gw0rXPMMPE&psig=AOvVaw10-tSFlEybX7Cv3Rx4x7ml&ust=1665240404781000&source=images&cd=vfe&ved=0CA0QjhxqFwoTCLjY7IiuzvoCFQAAAAAdAAAAABAN)


- 2019년 5월 3일, Windows에서 Terminal에 대한 새로운 애플리캐이션을 공개했다. (2020년 5월 19일에 정식으로 릴리즈)
- 비주얼 스튜디오와 C++로 개발되었다.

<br>

## Windows Terminal 설치하기

<details> 
<summary>▶Windows Terminal 설치하기</summary> 

<img src="https://user-images.githubusercontent.com/66783849/194584196-4ef1a700-44d9-4a38-84cb-b84e44bc51d1.png" width="100">

- Google에 "Windows Terminal" 검색 -> [Microsoft store 사이트](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701?hl=ko-kr&gl=kr) 접속 -> 스토어 앱에서 다운로드
  <img src="https://user-images.githubusercontent.com/66783849/194582731-8ac036cf-9ef2-4733-801c-09576995b677.png" width="300">
- 다운로드 후 애플리케이션을 실행한다.  
  <img src="https://user-images.githubusercontent.com/66783849/194583072-d0bb1d09-44d3-4d03-9378-3e4688823051.png" width="300">

</details> 

<br>

## Windows Terminal 유용한 팁

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + `마우스 스크롤` : Terminal 창의 배경 alpha 값을 조정한다. (투명도 조정)
- <kbd>Ctrl</kbd> + `마우스 스크롤` : 폰트크기를 설정한다.

<br>

## Windows Terminal 꾸미기

<details> 
<summary>▶Windows Terminal 꾸미기</summary> 


<img src="https://user-images.githubusercontent.com/66783849/194593015-6a5ca30c-fd36-4cfb-8268-08251190adfd.png" width="70%">

- Windows Terminal은 각 터미널 별로 Theme를 지정할 수 있다.
- 색, 폰트종류 및 크기, 여백크기, 투명한 배경 모두 가능하다.
- 이들을 쉽게 관리할 수있도록 Windows Terminal에서는 json 형식으로 theme를 저장한다.

<br>

### Windows Terminal json Setting

<img src="https://user-images.githubusercontent.com/66783849/194714772-cfc98e3e-ca35-4aa9-aa72-baffc5a6f982.png" width="70%">

- json에 가종 속성에 Theme를 첨가함으로써 다양한 터미널 디자인을 이용해 본다.
- Windows Terminal 설정 > 가장 아래 "json 파일 열기" 버튼 -> "setting.json"파일 을 통해 현재 파일 Theme를 관리한다.
- [Windows PowerShell](https://learn.microsoft.com/en-us/windows/terminal/custom-terminal-gallery/powerline-in-powershell)  
  <img src="https://user-images.githubusercontent.com/66783849/194590569-f14ad7af-a7a0-4620-8fb2-f4515cbc04f1.png" width="200">
  - 이 powershell 테마에 대한 json파일을 다음과 같다.
  ```json
  {
      "theme": "dark",
      "profiles": [
          {
              "name" : "Powershell",
              "source" : "Windows.Terminal.PowershellCore",
              "acrylicOpacity" : 0.5,
              "colorScheme" : "One Half Dark",
              "cursorColor" : "#FFFFFF",
              "font": 
              {
                  "face": "CaskaydiaCove Nerd Font"
              },
              "useAcrylic" : true
          }
      ]
  }
  ```
  - 파일에 존재하는 키워드 (예- "Profiles") 내용을 settings.json에 첨가한다.
- [Developer Raspberry Ubuntu](https://learn.microsoft.com/en-us/windows/terminal/custom-terminal-gallery/raspberry-ubuntu?source=recommendations)
  ```json
  {
      "theme": "dark",
      "profiles": [
          {
              "name" : "Ubuntu",
              "source" : "Windows.Terminal.Wsl",
              "colorScheme" : "Raspberry",
              "cursorColor" : "#FFFFFF",
              "fontFace" : "Cascadia Code",
              "padding" : "5, 5, 5, 5",
              "suppressApplicationTitle": true,
              "tabTitle": "Ubuntu"
          }
      ],
      "schemes": [
          {
              "name" : "Raspberry",
              "background" : "#3C0315",
              "black" : "#282A2E",
              "blue" : "#0170C5",
              "brightBlack" : "#676E7A",
              "brightBlue" : "#80c8ff",
              "brightCyan" : "#8ABEB7",
              "brightGreen" : "#B5D680",
              "brightPurple" : "#AC79BB",
              "brightRed" : "#BD6D85",
              "brightWhite" : "#FFFFFD",
              "brightYellow" : "#FFFD76",
              "cyan" : "#3F8D83",
              "foreground" : "#FFFFFD",
              "green" : "#76AB23",
              "purple" : "#7D498F",
              "red" : "#BD0940",
              "white" : "#FFFFFD",
              "yellow" : "#E0DE48"
          }
      ]
  }
  ```

<br>

### Windows Terminal json Key Setting

- terminal 내의 json 파일을 중심삼고 각종 단축키를 제작할 수 있다.
- 예) <kbd>Alt</kbd>+<kbd>K</kbd> : "clear"
  ```json
  { "command": {"action": "sendInput", "input": "clear\r"}, "keys": "alt+k", "name": "clear terminal" }
  ```
- 다음과 같이 Theme가 추가됨을 확인할 수 있다.  
<img src="https://user-images.githubusercontent.com/66783849/194714929-64612ddf-bf23-4daf-9ff3-72a08e0ed8b4.png" width="70%">

    
</details> 

<br>

## Windows Terminal 보조 기능

- 터미널을 사용하는 데 있어서 다양한 시각적 효과를 얻을 수 있는 보조기능을 설치하여 활용해본다.

<br>

<details> 
<summary>▶Windows Terminal 보조 기능</summary> 

### Nerd Font

- [Nerd Font 설치, Oh My Posh 설치](https://learn.microsoft.com/ko-kr/windows/terminal/tutorials/custom-prompt-setup)
- Nerd Font : 터미널에서 모든 문자 모양을 볼 수 있다.
  - [Nerd Font](https://www.nerdfonts.com/font-downloads) 다운로드한다.
  - Font 파일을 "C:\Windows\Fonts"에 붙여 넣는다.

<br>

### On My Posh

- Oh My Posh 설치 : powershell를 통해 설치한다.
  - PowerShell에 다음과 같이 입력하여 설치한다.
  ```bash
  winget install oh-my-posh
  ```
  - 최신 업데이트가 있는지 여부는 다음 코드를 통해서 확인한다.
  ```bash
  winget upgrade oh-my-posh
  ```
- [‼ 입력 조건과 일치하는 패키지가 여러 개 있습니다. 입력을 구체화하십시오.] : 여러 패키지가 있을 때 발생하며, 이름대신 "장치 ID"에 있는 문자열을 사용하면 됩니다.
  - 예) 다음과 같은 오류가 나타날 때
  ```bash
  > winget install oh-my-posh

  입력 조건과 일치하는 패키지가 여러 개 있습니다. 입력을 구체화하십시오.
  이름       장치 ID                 원본
  ------------------------------------------
  oh-my-posh XP8K0HKJFRXGCK          msstore
  Oh My Posh JanDeDobbeleer.OhMyPosh winget
  ```
  - 다음과 같이 입력한다.
  ```bash
  winget install JanDeDobbeleer.OhMyPosh
  ```
  <img src="https://user-images.githubusercontent.com/66783849/194716248-6f47af03-580d-409f-bf57-77f19978b5af.png" width="90%">
- 다음과 같이 결과가 나왔다.
  ```bash
  > winget install oh-my-posh

  입력 조건과 일치하는 패키지가 여러 개 있습니다. 입력을 구체화하십시오.
  이름       장치 ID                 원본
  ------------------------------------------
  oh-my-posh XP8K0HKJFRXGCK          msstore
  Oh My Posh JanDeDobbeleer.OhMyPosh winget
  
  > winget install JanDeDobbeleer.OhMyPosh

  찾음 Oh My Posh [JanDeDobbeleer.OhMyPosh] 버전 12.0.1
  이 응용 프로그램의 라이선스는 그 소유자가 사용자에게 부여했습니다.
  Microsoft는 타사 패키지에 대한 책임을 지지 않고 라이선스를 부여하지도 않습니다.
  Downloading https://github.com/JanDeDobbeleer/oh-my-posh/releases/download/v12.0.1/install-amd64.exe
    ██████████████████████████████  6.72 MB / 6.72 MB
  설치 관리자 해시를 확인했습니다.
  패키지 설치를 시작하는 중...
  설치 성공
  ```
- 다음 [사이트](https://ohmyposh.dev/docs/themes)를 통해 원하는 OhMyPush 테마를 선택한다.
- 선택한 테마의 json 파일을 별도로 저장한다.
- 다음 명령어를 통해 json 파일을 적용한다.
  ```bash
  oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\paradox.omp.json" | Invoke-Expression
  ```
  ```bahs
  oh-my-posh init pwsh --config "D:\Sagi_JJU D\코딩 프로젝트\2022\oh-my-posh-main\themes\quick-term.omp.json" | Invoke-Expression
  ```
  <img src="https://user-images.githubusercontent.com/66783849/194718853-7db148d9-e774-4336-8e22-7f2faa1d417a.png" >

  </details> 
<br>


<br>

### 참조

- [Oh My Posh를 사용하여 PowerShell 또는 WSL에 대한 사용자 지정 프롬프트 설정](https://learn.microsoft.com/ko-kr/windows/terminal/tutorials/custom-prompt-setup)
- [The new Windows Terminal | YouTube](https://www.youtube.com/watch?v=8gw0rXPMMPE)
- [프롬프트 연결](https://ohmyposh.dev/docs/installation/prompt)
