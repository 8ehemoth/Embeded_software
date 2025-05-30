## 🔧 졸음운전이 감지되지 않았을 경우 음성으로 액추에이터를 제어하는 아이디어

- 졸음운전이 감지되지 않은 상태에서도 운전자의 음성 명령을 통해 차량 내 액추에이터를 제어할 수 있는 기능을 추가하는 아이디어 제시
- 예: “창문 열어줘”, “에어컨 꺼줘” 등의 명령을 통해 실습용 모형에서 기능 제어

---

## 🚗 차량 액추에이터 제어 관련 기술적 논의

### 1. 제어 방식

- **GPIO 방식**  
  - 간단한 실습용 액추에이터 제어에 적합 (LED, 부저, 서보모터 등)
  - Raspberry Pi의 GPIO 핀으로 제어 가능

- **CAN 방식**
  - 실제 차량에서는 대부분의 액추에이터가 CAN 통신을 통해 제어됨
  - 구현이 복잡하고 고가의 하드웨어 필요

### 2. 실차 모델링의 필요성

- 완전한 차량 액추에이터 구현은 **CAN 통신 기반 실차 모형** 필요
- 현실적인 구현 방식: **모형 자동차 + 간단한 액추에이터 (창문, 히터 등)** 만 제어
- **기능 구현이 핵심**이며, 외형은 최소한으로 구성

---

## 🧰 모형 구현 관련 의견

- **3D 프린터를 활용한 외관 제작 가능**
  - 간단한 CAD 모델링을 통해 출력
- 프로젝트 목적상, **외형보다는 기능 동작 중심으로 구성**하는 것이 효율적

---

## 🗣️ 음성 제어 처리 로직

1. 운전자 음성을 수신
2. **STT(Speech to Text)** 처리로 텍스트 변환
3. 변환된 텍스트 분석
4. 명령어에 따라 특정 **액추에이터(GPIO 제어 등)** 실행

---

## 🔌 차량 직접 통신(CAN) 여부

- 실제 차량과의 통신은 **고급 기술 및 인증 필요**
- 실습 프로젝트 수준에서는 GPIO 기반 제어로 충분
- 필요 시, **CAN 통신을 시뮬레이션**하는 방식으로도 가능

---
