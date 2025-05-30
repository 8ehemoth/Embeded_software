2025년 5월 기준으로, Google Cloud Text-to-Speech API에서 한국어(ko-KR)로 사용할 수 있는 음성 목록은 다음과 같습니다:

---

### ✅ 한국어(ko-KR) 지원 음성 목록

| 음성 이름                    | 성별 | 음성 유형     | 설명              |                                                                         |
| ------------------------ | -- | --------- | --------------- | ----------------------------------------------------------------------- |
| `ko-KR-Standard-A`       | 여성 | Standard  | 기본 여성 음성        |                                                                         |
| `ko-KR-Standard-B`       | 여성 | Standard  | 기본 여성 음성        |                                                                         |
| `ko-KR-Standard-C`       | 남성 | Standard  | 기본 남성 음성        |                                                                         |
| `ko-KR-Standard-D`       | 남성 | Standard  | 기본 남성 음성        |                                                                         |
| `ko-KR-Wavenet-A`        | 여성 | WaveNet   | 자연스러운 여성 음성     |                                                                         |
| `ko-KR-Wavenet-B`        | 여성 | WaveNet   | 자연스러운 여성 음성     |                                                                         |
| `ko-KR-Wavenet-C`        | 남성 | WaveNet   | 자연스러운 남성 음성     |                                                                         |
| `ko-KR-Wavenet-D`        | 남성 | WaveNet   | 자연스러운 남성 음성     |                                                                         |
| `ko-KR-Neural2-A`        | 여성 | Neural2   | 향상된 자연스러운 여성 음성 |                                                                         |
| `ko-KR-Neural2-B`        | 여성 | Neural2   | 향상된 자연스러운 여성 음성 |                                                                         |
| `ko-KR-Neural2-C`        | 남성 | Neural2   | 향상된 자연스러운 남성 음성 |                                                                         |
| `ko-KR-Chirp3-HD-Aoede`  | 여성 | Chirp3-HD | 고품질 여성 음성       |                                                                         |
| `ko-KR-Chirp3-HD-Kore`   | 여성 | Chirp3-HD | 고품질 여성 음성       |                                                                         |
| `ko-KR-Chirp3-HD-Leda`   | 여성 | Chirp3-HD | 고품질 여성 음성       |                                                                         |
| `ko-KR-Chirp3-HD-Zephyr` | 여성 | Chirp3-HD | 고품질 여성 음성       |                                                                         |
| `ko-KR-Chirp3-HD-Charon` | 남성 | Chirp3-HD | 고품질 남성 음성       |                                                                         |
| `ko-KR-Chirp3-HD-Fenrir` | 남성 | Chirp3-HD | 고품질 남성 음성       |                                                                         |
| `ko-KR-Chirp3-HD-Orus`   | 남성 | Chirp3-HD | 고품질 남성 음성       |                                                                         |
| `ko-KR-Chirp3-HD-Puck`   | 남성 | Chirp3-HD | 고품질 남성 음성       | ([Stack Overflow][1], [VentureBeat][2], [Google Cloud][3], [Twilio][4]) |

---

### 🎧 음성 선택 가이드

* **자연스러운 여성 음성**: `ko-KR-Wavenet-A`, `ko-KR-Wavenet-B`
* **자연스러운 남성 음성**: `ko-KR-Wavenet-C`, `ko-KR-Wavenet-D`
* **향상된 자연스러움**: `ko-KR-Neural2-A`, `ko-KR-Neural2-B`, `ko-KR-Neural2-C`
* **고품질 음성**: `ko-KR-Chirp3-HD-*` 시리즈([Google Cloud Community][5], [Twilio][4])

---

### 🔧 예시 코드 (Python)

```python
from google.cloud import texttospeech

client = texttospeech.TextToSpeechClient()

synthesis_input = texttospeech.SynthesisInput(text="안녕하세요. 만나서 반가워요!")

voice = texttospeech.VoiceSelectionParams(
    language_code="ko-KR",
    name="ko-KR-Wavenet-B"  # 원하는 음성으로 변경
)

audio_config = texttospeech.AudioConfig(
    audio_encoding=texttospeech.AudioEncoding.MP3
)

response = client.synthesize_speech(
    input=synthesis_input,
    voice=voice,
    audio_config=audio_config
)

with open("output.mp3", "wb") as out:
    out.write(response.audio_content)
```

---

### 📌 참고

* 최신 음성 목록은 [Google Cloud 공식 문서](https://cloud.google.com/text-to-speech/docs/voices?hl=ko)에서 확인하실 수 있습니다.
* 특정 음성의 톤, 말속도, 감정 스타일 같은 고급 설정도 가능합니다.

필요하신 경우, 특정 음성의 데모나 추가 설정 방법에 대해 안내해 드릴 수 있습니다!

[1]: https://stackoverflow.com/questions/79392578/google-cloud-text-to-speech-remove-supported-voice-list-without-notify?utm_source=chatgpt.com "Google Cloud Text-To-Speech Remove Supported Voice List ..."
[2]: https://venturebeat.com/ai/google-cloud-text-to-speech-adds-31-wavenet-voices-7-languages-and-dialects/?utm_source=chatgpt.com "Google Cloud Text-to-Speech adds 31 WaveNet voices, 7 ..."
[3]: https://cloud.google.com/text-to-speech/docs/release-notes?utm_source=chatgpt.com "Text-to-Speech release notes - Google Cloud"
[4]: https://www.twilio.com/docs/voice/twiml/say/text-speech?utm_source=chatgpt.com "Text-to-Speech (TTS) - Twilio"
[5]: https://www.googlecloudcommunity.com/gc/AI-ML/Problems-with-using-ko-KR-Neural2-in-tts-API/m-p/602671/highlight/true?utm_source=chatgpt.com "Re: Problems with using ko-KR-Neural2 in tts API."




https://github.com/user-attachments/assets/d0372fb3-0185-41b7-ada3-d03368e9b8e4



https://github.com/user-attachments/assets/6877b65d-5c64-4458-bf04-c7b3d9b11299



https://github.com/user-attachments/assets/ab794432-9bd5-4ffb-973e-bbf16ae16284




