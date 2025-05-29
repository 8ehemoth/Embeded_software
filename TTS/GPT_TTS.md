좋습니다! 아래는 **OpenAI API 키와 Google Cloud 서비스 계정 키 JSON 파일을 사용한 TTS 프로젝트**를 디렉토리 구성까지 포함해 **VSCode 환경 기준 Git 프로젝트 형식**으로 정리해 드립니다.

---

## ✅ 1. 디렉토리 구조 예시

```
My_project/
├── .env                   ← OpenAI API 키 저장
├── .gitignore             ← 민감 정보 무시 설정
├── README.md              ← 프로젝트 설명 문서
├── test_gpt_voice.py      ← 메인 실행 코드
└── requirements.txt       ← 필요한 패키지 명시
```

---

## ✅ 2. `.gitignore`

```gitignore
.env
*.json
__pycache__/
*.pyc
*.mp3
.venv/
```

> `.env` 파일과 Google Cloud JSON 키 파일은 **절대 Git에 올리지 마세요**. 위처럼 `.gitignore`에 추가해야 안전합니다.

---

## ✅ 3. `.env` 파일 (업로드 금지)

```env
OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

---

## ✅ 4. `requirements.txt` 파일

```txt
openai>=1.0.0
google-cloud-texttospeech
python-dotenv
```

> 아래 명령어로 자동 생성 가능:

```bash
pip freeze > requirements.txt
```

---

## ✅ 5. `test_gpt_voice.py`

```python
import os
from openai import OpenAI
from google.cloud import texttospeech
from dotenv import load_dotenv

# .env 파일 로드
load_dotenv()

# OpenAI 클라이언트 초기화
client = OpenAI()

# ChatGPT 응답 받기
def get_chatgpt_response(prompt: str) -> str:
    response = client.chat.completions.create(
        model="gpt-3.5-turbo",
        messages=[{"role": "user", "content": prompt}],
        temperature=0.7
    )
    return response.choices[0].message.content.strip()

# 한국어 음성으로 MP3 변환
def text_to_korean_speech(text: str, filename: str = "output_korean.mp3"):
    tts_client = texttospeech.TextToSpeechClient()

    synthesis_input = texttospeech.SynthesisInput(text=text)

    voice = texttospeech.VoiceSelectionParams(
        language_code="ko-KR",
        name="ko-KR-Wavenet-C",
        ssml_gender=texttospeech.SsmlVoiceGender.FEMALE
    )

    audio_config = texttospeech.AudioConfig(
        audio_encoding=texttospeech.AudioEncoding.MP3,
        speaking_rate=1.0
    )

    response = tts_client.synthesize_speech(
        input=synthesis_input,
        voice=voice,
        audio_config=audio_config
    )

    with open(filename, "wb") as out:
        out.write(response.audio_content)
        print(f"✅ 한국어 음성 MP3 저장 완료: {filename}")

if __name__ == "__main__":
    # Google 서비스 키 경로 수동 설정
    os.environ["GOOGLE_APPLICATION_CREDENTIALS"] = "경로\your-key.json"

    user_prompt = input("💬 ChatGPT에게 질문하세요 (한글): ")
    answer = get_chatgpt_response(user_prompt)
    print("🧠 ChatGPT 응답:", answer)

    text_to_korean_speech(answer)
```



## 🔐 환경 변수 설정

1. `.env` 파일 생성:

```
OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxx
```

2. Google Cloud Console에서 서비스 계정 키(JSON)를 생성하여 로컬에 저장하고,
   `test_gpt_voice.py`의 경로를 아래처럼 수정:

```python
os.environ["GOOGLE_APPLICATION_CREDENTIALS"] = "경로\your-key.json"
```

## ▶️ 실행

```bash
python test_gpt_voice.py
```

---

## ❗주의

* `.env`와 JSON 키 파일은 `.gitignore`에 추가되어 있어야 합니다!
* API 키를 절대 공개하지 마세요.

---

## 🎯 목표 기능 (필요 시 추가)

* 한국어/영어 자동 감지 및 음성 선택
* 다회 입력 지원
* 음성 재생 기능 추가 (playsound 등)


실행결과
![image](https://github.com/user-attachments/assets/67ece3b9-b01e-4b76-9078-e63c03b1c7df)

https://github.com/user-attachments/assets/9616ca02-8b29-4889-9825-8f660aea728e



