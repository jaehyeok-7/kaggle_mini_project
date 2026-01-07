<div align="center">
  <img src="https://img.shields.io/badge/python-3776AB?style=for-the-badge&logo=python&logoColor=white">
  <img src="https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white">
  <img src="https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white">
  <img src="https://img.shields.io/badge/lightgbm-FFD43B?style=for-the-badge&logo=lightgbm&logoColor=black">
</div>

# 📖 프로젝트 주제 : 대사 지표 간 연관성 분석: 회귀분석 및 분산분석, 로지스틱 회귀분석을 활용한 통계적 접근
- 대사 지표(혈당, 인슐린, BMI 등) 간의 상관관계를 통계적으로 분석하고, 머신러닝 기법을 통해 당뇨병 고위험군을 예측하는 데이터 분석 프로젝트

## 1. Project Overview 
- **주제** : 생활 습관 또는 신체 상태를 활용한 당뇨병 유무 분류 
- **데이터셋** : [Diabetes Health Indicators Dataset](https://www.kaggle.com/datasets/mohankrishnathalla/diabetes-health-indicators-dataset/data) 
- **핵심 목표** : 설문지를 활용해서 **당뇨병 고위험군을 선별할 수 있는 예측 모델** 구축 
- **프로젝트 기간** : 2025년 12월 29일 ~ 2025년 12월 31일 

## 2. Data Dictionary (주요 핵심 변수)
- 분석에 사용된 주요 생체 지표 및 임상 데이터 (총 31개 변수, 10만 건 데이터) 

| 변수명 | 설명 | 비고 |
| :--- | :--- | :--- |
| **HbA1c** | 당화혈색소 | 지난 2~3개월간의 평균 혈당 상태 |
| **Glucose** | 공복 혈당 수치 | 당뇨 진단의 핵심 지표 |
| **Insulin** | 인슐린 수치 | 혈당을 세포로 들이는 '문지기' 역할 |
| **BMI** | 체질량 지수 | 비만도 측정 및 인슐린 저항성 관련 지표 |
| **Triglycerides** | 중성지방 | 혈중 지방 농도 (위험 요인) |
| **HDL** | 고밀도 콜레스테롤 | 혈당을 낮추는 보호 요인 |
| **Diabetes_binary** | 당뇨 여부 (**Target**) | 0: 정상, 1: 당뇨/전단계 |

## 3. Problem Definition
- **데이터 특성** : 31개의 변수와 100,000개의 행으로 구성된 대규모 데이터셋 분석 
- **분석 방향** 
    + **통계 분석** : 다중회귀(인슐린 및 혈당 영향 요인), 분산분석(당뇨 단계별 HbA1c 차이), 로지스틱 회귀(당뇨 진단 확률)
    + **머신러닝** : Logistic Regression, XGBoost, LightGBM 모델 간 성능 비교

## 4. Data Preprocessing
- **클래스 불균형 해소** : 층화 샘플링(Stratified Sampling)을 통해 학습/검증 데이터의 클래스 비율 유지 
- **변수 처리** 
    + **수치형 변수**: StandardScaler를 이용한 표준화 적용
    + **범주형 변수**: One-Hot Encoding 및 Ordinal Encoding 적용
- **데이터 분리**: 훈련 데이터 80%, 검증 데이터 20% 구성 

## 5. 통계분석 핵심 인사이트
- **인슐린 수치 영향** : **BMI($\beta=0.540$)**가 가장 강력한 정(+)의 영향력을 보이며, 당뇨 가족력($\beta=0.1926$)도 유의미한 영향 확인.
- **HbA1c 결정 요인** : **식후 혈당($\beta=0.0210$)**이 압도적인 영향력을 가지며, 상관계수 **0.93**으로 거의 완벽한 선형 관계를 나타냄.
- **당뇨 단계별 차이** : ANOVA 분석 결과, 정상/전당뇨/당뇨 그룹 간 HbA1c 수치 차이는 통계적으로 매우 유의함($p < 0.001, F=27,387$).

## 6. 모델링 평가지표
- 중요도 하위 변수를 제거한 **LightGBM (Reduced)** 모델이 최적의 성능을 기록함.

| Model | CV ROC-AUC | Val ROC-AUC | 비고 |
| :--- | :--- | :--- | :--- |
| Logistic Regression | 0.6937 | 0.6940 | - |
| XGBoost | 0.7238 | 0.7239 | - |
| LightGBM | 0.7251 | 0.7251 | - |
| **LightGBM (Reduced)** | **0.7251** | **0.7255** | **최종 모델 선정** |

> **Note** : 변수 제거 후 Kaggle **Public Score 0.69614**, Private Score 0.69283 달성 (전 단계 대비 약 0.36% 향상).

## 7. Feature Importance (옵션)
- SHAP 활용
- 예측 모델에서 영향력이 가장 컸던 지표 순위 
1. AGE
2. BMI

![SHAP Rank](output/Rank.png)

## 8. Conclusion 
- 결론1 : BMI는 당뇨병 발생 위험의 가장 강력한 예측인자
- 결론2 : 나이가 증가함에 따라 당뇨병 발생 위험이 증가
- 결론3 : 인슐린 저항성은 비만과 밀접한 관련

# 보고서
- 프로젝트 상세 보고서는 PDF 슬라이드 자료를 참고하여 주세요
- 📄 프로젝트 상세 보고서 : [대사 지표 간 연관성 분석 프로젝트보고서](report/대사%20지표%20간%20연관성%20분석%20프로젝트보고서.pdf)
- 분석코드 : [분석코드](분석코드/분석코드.ipynb)

# 🔗 배지 및 이모지 공식 소스 링크
| 용도 | 사이트 이름 | 링크 |
| :--- | :--- | :--- |
| **배지 생성** | Shields.io | https://shields.io/ |
| **로고/색상 검색** | Simple Icons | https://simpleicons.org/ |
| **이모지 검색** | Emoji Cheat Sheet | https://github.com/ikatyang/emoji-cheat-sheet |
