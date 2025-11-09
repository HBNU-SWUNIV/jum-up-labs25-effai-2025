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

## Numerical Results
- 경진대회 Open에서 3등 Blind 11등

## Conclusion
- ABCD

## Project Outcome
- ABCD
