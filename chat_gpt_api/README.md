# 핵심 개념 정리 — ChatGPT API · Prompt Caching · Embeddings  
> 임베디드 졸음운전 방지 프로젝트용 메모  
> (작성 2025-05-28)

---

## 1. ChatGPT API (*Chat Completions*)

| 항목 | 내용 |
|------|------|
| **엔드포인트** | `POST https://api.openai.com/v1/chat/completions` |
| **요청 본문** | `model`, `messages[]`, 선택 파라미터 (`stream`, `temperature`, `tools` 등) |
| **역할(role)** | `system → assistant ↔ user` 순으로 대화 맥락 전달 |
| **응답** | JSON → `choices[0].message.content` 에 모델 답변, `usage` 필드에 토큰 통계 |
| **과금** | *입력 토큰 × 단가* + *출력 토큰 × 단가*<br>(예: **GPT-4o mini** 기준 — 입력 $0.40 / M, 출력 $1.60 / M) |
| **지연 ↓ 방법** | ① `stream:true` 로 토큰 스트리밍<br>② Prompt Caching(아래) 활용 |

### 1-1. 최소 호출 예시 (Python SDK)

```python
from openai import OpenAI
client = OpenAI(api_key="sk-...")

resp = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[
        {"role": "system", "content": "You are an upbeat co-driver."},
        {"role": "user",   "content": "내가 졸려, 말 좀 걸어줘!"}
    ],
    stream=False           # True로 하면 토큰 단위 스트리밍
)
print(resp.choices[0].message.content)
```

---

## 2. Prompt Caching

> **같은 조직**에서 **최근 1 시간** 이내 제출된 프롬프트의 **앞 1 024 token 이상**이 일치하면 **입력 토큰 비용 50 % 할인** + 전처리 지연 감소.

| 체크포인트 | 이유 / 효과 |
|------------|-------------|
| 공통 시스템 프롬프트·예시는 **맨 앞**에 고정 | 캐시 적중률 ↑ |
| 1 024 token 이상 되도록 컨텍스트 묶기 | 캐시 임계값 충족 |
| 캐시 의도 O + `stream:true` | 실측 지연 30 %↓ |

캐시 적중 여부는 응답 JSON의  
`usage.prompt_tokens_details.cached_tokens` 필드로 확인할 수 있다.

---

## 3. Embeddings API

| 항목 | 내용 |
|------|------|
| **엔드포인트** | `POST https://api.openai.com/v1/embeddings` |
| **대표 모델** | `text-embedding-3-small` (1 536‑dim, 저가형) |
| **출력** | 입력 텍스트 → 부동소수 벡터<br>예: `[0.018, -0.012, …]` |
| **주요 용도** | • 벡터 DB(FAISS/Chroma) 검색<br>• RAG(Retrieval‑Augmented Generation)<br>• 유사도 기반 문서 요약·압축 |

### 3-1. 간단 호출 예

```python
vec = client.embeddings.create(
    model="text-embedding-3-small",
    input="졸음운전 방지 프로젝트 개요"
).data[0].embedding   # 길이 1 536
```

### 3-2. 긴 텍스트 요약 워크플로

1. GPT가 반환한 **긴 답변** → 문단 단위 **벡터화** 후 로컬 DB 저장  
2. “핵심 정보만” 요청 시, **질의 벡터**와 **CosSim Top‑k** 문단 검색  
3. 추출 문단만 GPT에게 보내 **재요약** → 출력 토큰·지연 ↓

---

## 4. 용어 한눈에 보기

| 용어 | 정의 |
|------|------|
| **API** | 기능을 외부에 노출하는 **계약(명세)** |
| **엔드포인트** | “주소 + HTTP 메서드” 한 쌍으로 정의된 API 호출 지점 |
| **토큰** | LLM이 처리하는 최소 단위 (영어 ≈ 0.75 단어, 한글 ≈ 1 글자) |
| **Prompt Caching** | 동일 프롬프트 prefix 재사용 시 입력 토큰 50 % 할인 |
| **Embedding** | 텍스트 의미를 보존하는 고차원 벡터 표현 |

