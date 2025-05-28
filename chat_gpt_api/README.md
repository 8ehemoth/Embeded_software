# 핵심 개념 정리 — ChatGPT API · Prompt Caching · Embeddings  
> 임베디드 졸음운전 방지 프로젝트용 메모  
> (작성 2025-05-28)

---

## 1. ChatGPT API (Chat Completions)

| 항목 | 내용 |
|------|------|
| **엔드포인트** | `POST https://api.openai.com/v1/chat/completions` |
| **요청 본문** | `model`, `messages[]`, 선택 파라미터(`stream`, `temperature`, `tools` 등) |
| **역할(role)** | `system → assistant ↔ user` 순으로 대화 맥락 전달 |
| **응답** | JSON → `choices[0].message.content` 에 모델 답변, `usage` 필드에 토큰 통계 |
| **과금** | *입력 토큰 × 단가* + *출력 토큰 × 단가*<br>(GPT-4o mini 기준 : 입력 $0.40/M, 출력 $1.60/M) |
| **지연 ↓ 방법** | • `stream:true` 로 토큰 스트리밍   • Prompt Caching(아래) 적용 |

> 자세한 파라미터는 OpenAI 공식 문서 *API Reference → Chat Completions* 참조. :contentReference[oaicite:0]{index=0}

### 1-1. 최소 호출 예시 (Python SDK)

```python
from openai import OpenAI
client = OpenAI(api_key="sk-…")

resp = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[
        {"role":"system","content":"You are an upbeat co-driver."},
        {"role":"user",  "content":"내가 졸려, 말 좀 걸어줘!"}
    ],
    stream=False
)
print(resp.choices[0].message.content)
