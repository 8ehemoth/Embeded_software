# OpenAI API Key 발급 & 사용 가이드
> 졸음운전 방지 프로젝트 — ChatGPT 모듈 준비용  
> (v 2025 ‑ 05 ‑ 28)

---

## 1. API Key 발급 절차

| 단계 | 화면 경로 | 설명 |
|------|-----------|------|
| 1 | **platform.openai.com** 로그인 | 회원 가입 또는 기존 계정 로그인 |
| 2 | **Billing ▸ Payment methods** | 무료 크레딧 이후 사용하려면 카드 등록 |
| 3 | **右上 사용자 아이콘 ▸ “API keys”** | 키 관리 페이지 진입 |
| 4 | **Create new secret key** 버튼 | 별칭 입력 → **Create key** |
| 5 | **키 복사(sk‑…) & 보관** | 한 번만 노출됨 – 바로 `.env` 등에 저장 |

---

## 2. 안전 보관 수칙 🔐
| 항목 | 권장 방법 |
|------|-----------|
| **저장** | 프로젝트 루트에 `.env` → `OPENAI_API_KEY=sk-…` |
| **코드 공개** | `.gitignore`에 `.env` 추가 – GitHub에 노출 금지 |
| **키 분리** | 개발 / 운영 / 테스트 환경별로 개별 키 발급 |
| **회수(Revoke)** | 사용 안 하면 “⋯ ▸ Revoke” 로 즉시 폐기 |

---

## 3. 환경 변수 로드 예시 (Python)

```python
import os
from openai import OpenAI

client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))

resp = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[{"role":"user","content":"키 설정 완료?"}]
)
print(resp.choices[0].message.content)
```

---

## 4. VS Code 실행 팁

1. **Python 확장** 설치 후, `.venv` 가상환경 활성화  
2. **dotenv** 확장으로 `.env` 하이라이트  
3. `Ctrl+Shift+D` ▶ “Run & Debug” → 환경 변수가 자동 주입되면 정상

---

## 5. 문제 해결 체크리스트

| 증상 | 원인·조치 |
|------|-----------|
| `401 Unauthorized` | 키 오타 / 만료 → 새로 발급 |
| `429 Rate limit` | 초당 요청 과다 → `asyncio.sleep` 백오프 |
| `Billing hard limit reached` | Usage > 설정 한도 → Billing ▸ Usage refresh |

> 이 가이드라인을 따라 **API Key 발급 → `.env` 저장 → 간단 호출 스크립트** 까지 완료되면 ChatGPT API 연동 준비가 끝납니다.
