# Jump-up-Labs-TEMPLATE
# 국립한밭대학교 인공지능 소프트웨어학과 이파이팀

**팀 구성**
- 20227005 진경은
- 20192390 김장환
- 20221055 신은호
- 20221063 이유진
- 20231045 김서연

## Project Background
- 최근 생성형 모델의 대중화와 함께 특정 도메인에서의 활용도 역시 커지고 있다. 이에 따라 교내 경진대회(생성형 AI 와 인간 텍스트 판별 챌린지)를 통해 특정 도메인에서 주어진 데이터 분포를 효과적으로 학습 할 수 있는 방법에 대해 탐구한다. 거기에 더해 특정 도메인에 특화된 모델을 저전력 디바이스에서도 효율적으로 동작 할 수 있도록 다양한 최적화 기법에 대해 탐구한다.

## System Model
### 1. 생성형 AI와 인간 텍스트 판별 챌린지
#### 1. 데이터
 - 이진 분류
 - Test dataset 이 Train 보다 크다는 특징이 있음
 - 영어, 한국어로 구성되어있으며 정치 시사 등 여러 뉴스기사로 구성됨

#### 2. 데이터 증강
 - 키워드 블라인딩 : 클래스와 상관성이 높은 단어를 랜덤하게 선택 이후 masking 하는 기법
 - 랜덤 단어 삽입 : 사전에 정의한 단어 뭉치에서 샘플링한 중립적인 의미를 가지는 단어를 무작위로 삽입하는 기법

#### 3. 파인튜닝 
 - 학습용 데이터가 검증용 데이터 보다 작다는 점을 감안해 비교적 크기가 작은 모델 인 Qwen3-8B(영어), KoBERT(한국어)를 활용
 - LoRA 어뎁터를 삽입해 PEFT 방식으로 학습, K-Fold 교차검증를 활용해 일반화 성능을 추정
   
  <img width="445" height="390" alt="image" src="https://github.com/user-attachments/assets/fb977123-9d57-459e-be8d-a6bdb1ffe83b" />

 <img width="812" height="254" alt="image" src="https://github.com/user-attachments/assets/83508d27-c219-492e-b100-c109b729e161" />

### 2. 모델 최적화 연구


본 연구에서는 **대규모 멀티모달 모델의 효율적 경량화**를 목표로,  
`X-Decoder` 구조를 대상으로 한 **PTQ (Post-Training Quantization)** 기반 최적화 기법을 적용하였다.  
대규모 생성형 모델은 연산량과 메모리 사용량이 커 **저전력 디바이스에서의 실시간 추론이 어렵다**는 한계가 있다.  
이에 따라 **추론 속도 향상과 정확도 유지의 균형**을 달성하기 위한 다양한 양자화 실험을 수행하였다.

---

#### 연구 개요

- **모델 대상:** `X-Decoder` (멀티모달 Semantic Segmentation 모델)  
- **연구 목표:** 추가 학습 없이 정수형 연산으로 변환하여 효율 개선  
- **사용 도구:** [AIMET (AI Model Efficiency Toolkit)](https://github.com/quic/aimet)  
- **데이터셋:** RefCOCO (이미지–텍스트 매칭 기반 분할 데이터셋)

---

#### 적용 기법

1. **Batch Norm Folding (BNF)**  
   - 학습 완료 후 Batch Normalization 계층의 평균·분산을 인접한 Linear/Conv 가중치에 병합  
   - 불필요한 계산을 제거하고, 추론 그래프를 단순화하여 실행 효율 향상  

2. **Cross Layer Equalization (CLE)**  
   - 연속된 계층 간의 출력 분포를 정규화하여 채널 불균형 완화  
   - 저정밀 양자화 시 발생하는 **채널 단위 오차(Activation Mismatch)** 최소화  

---

#### 실험 결과
 

- **CLE 적용 시** FP32 대비 정확도 손실이 *0.005 이내*로 유지  
- **추론 속도 약 42% 향상**  
- **활성화 함수 정밀도 실험:**  
  - `A32`, `A16`: 정확도 유지  
  - `A8`: 정확도 급감 (0.316 mIoU)  
  → **Cross Attention 구조가 Activation 정밀도에 민감함**을 확인  

---

#### 결론

- **CLE 기법**은 PTQ 환경에서 정확도 손실을 최소화하는 핵심 요소임을 검증  
- **W16A16 구성**은 정확도와 속도 간 **최적 균형점**으로 확인됨  
- 향후 연구 방향:
  - **QAT (Quantization-Aware Training)** 적용을 통한 추가 성능 개선  
  - **INT8 양자화 및 NPU 배포 실험**으로 확장 예정  

---
## Numerical Results
- 경진대회 Open에서 3등 Blind 11등

## Conclusion
- 

## Project Outcome
- 
