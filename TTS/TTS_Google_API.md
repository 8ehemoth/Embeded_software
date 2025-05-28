좋습니다! 아래는 \*\*Windows CMD (명령 프롬프트)\*\*에서 Google Cloud의 **Text-to-Speech API**를 이용해 TTS (텍스트를 음성으로 변환)하는 전체 과정을 단계별로 정리한 가이드입니다.

---

## ✅ 1단계: Google Cloud 설정

### 1. Google Cloud 프로젝트 생성 및 TTS API 활성화

* [https://console.cloud.google.com](https://console.cloud.google.com) 에서 새 프로젝트 생성
* "Text-to-Speech API"를 검색 → **활성화**

### 2. 서비스 계정 키(JSON) 생성

1. IAM & Admin → 서비스 계정 → 서비스 계정 생성
2. 권한: `Text-to-Speech Admin` 또는 `Editor`
3. 키 → 키 추가 → JSON 선택 → 다운로드 (예: `ambient-topic-xxxxx.json`)

---

## ✅ 2단계: Windows 환경 준비

### 1. Python 설치 (없다면)

[https://www.python.org/downloads/](https://www.python.org/downloads/) 에서 Python 설치

설치 후 CMD에서 버전 확인:

```bash
python --version
```

---

### 2. 필요한 Python 패키지 설치

```bash
pip install google-cloud-texttospeech
```

---

### 3. 환경 변수 설정 (cmd에서 한 번만 하면 됨)

```bash
set GOOGLE_APPLICATION_CREDENTIALS="C:\경로\다운받은키.json"
```

> 예시:

```bash
set GOOGLE_APPLICATION_CREDENTIALS="C:\Users\Kim\Downloads\ambient-topic-461211-s1-90ff790bef2f.json"
```

---

## ✅ 3단계: Python 코드로 TTS 실행

파일 이름: `tts_test.py`

```python
from google.cloud import texttospeech
import os

# 인증 키 환경 변수 설정 (코드 안에서도 가능)
os.environ["GOOGLE_APPLICATION_CREDENTIALS"] = r"C:\Users\Kim\Downloads\ambient-topic-461211-s1-90ff790bef2f.json"

client = texttospeech.TextToSpeechClient()

synthesis_input = texttospeech.SynthesisInput(text="안녕하세요. 구글 클라우드 텍스트 투 스피치입니다.")

voice = texttospeech.VoiceSelectionParams(
    language_code="ko-KR",  # 한국어
    ssml_gender=texttospeech.SsmlVoiceGender.NEUTRAL
)

audio_config = texttospeech.AudioConfig(
    audio_encoding=texttospeech.AudioEncoding.MP3
)

response = client.synthesize_speech(
    input=synthesis_input, voice=voice, audio_config=audio_config
)

# 결과 저장
with open("output.mp3", "wb") as out:
    out.write(response.audio_content)
    print("output.mp3 파일로 저장 완료")
```

---

## ✅ 4단계: CMD에서 실행

CMD에서 해당 `.py` 파일이 있는 폴더로 이동 후 실행:

```bash
python tts_test.py
```

---

## 🔊 출력 결과

* 실행하면 현재 폴더에 `output.mp3` 파일이 생성됩니다.
* 더블클릭하면 바로 들을 수 있습니다.

---

## ✅ 오류 피하기 팁

| 문제              | 해결                               |
| --------------- | -------------------------------- |
| PermissionError | `output.mp3`가 열려있는 경우 종료하고 다시 실행 |
| SyntaxError     | 경로에 `\` 대신 `\\` 또는 `r""` 사용      |
| 인증 실패           | JSON 경로 확인 & 환경 변수 정확히 설정        |

---

필요하시면 라즈베리파이용 버전이나 영어/일어/남성 목소리로 바꾸는 방법도 알려드릴게요.
