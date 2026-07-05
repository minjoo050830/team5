# Team5
## “Sleeptune”

당신의 생체 신호를 조율하여, 최적의 수면 상태를 찾아드립니다.
ML을 1차 엔진으로 활용하는 AI 수면 코치 - 머신러닝이 수면 장애 위험도와 개인별 목표치를 정밀 분석하고, Gemini AI가 맞춤형 수면 가이드와 오늘 밤 실천 미션을 제공합니다.

### **프로젝트 개요**

기존 수면 관리 서비스는 개인 특성을 충분히 반영하지 못하며, 단순한 수면 시간 추천이나 데이터 제공에 그치는 경우가 많습니다. LLM 단독 기반 서비스는 개인의 생체 데이터가 부족해 일반적인 조언만 제시하는 한계가 있습니다.

**Sleeptune**은 ML의 정밀 분석과 LLM의 맞춤형 해석을 결합하여 이러한 문제를 해결합니다.

| **기존 서비스의 한계** | **Sleeptune의 해결 방식** |
| --- | --- |
| 개인 특성 미반영 | RF 기반 수면 상태 3분류(Normal / Insomnia / Sleep Apnea) → 페르소나 도출  |
| 단순 수면 시간 추천 | KNN 유사 수면군 비교로 개인 목표치 산출 |
| LLM 단독 → 일반적 조언 | ML 결과 + 생활습관 데이터를 LLM에 전달 |

### **주요 기능**

- **수면 상태 분류** - Random Forest 3분류 모델로 Normal / Insomnia / Sleep Apnea 위험도 예측
- **수면 페르소나 부여** - RF 분류 결과와 SHAP 기여도 분석을 결합하여 사용자에게 6가지 맞춤 페르소나 제공
- - **개인별 목표치 추천** - KNN 기반 유사 수면군 매칭으로 걸음 수, 수면 시간, 스트레스 수준, 심박수 등 개인 목표치 제공
- **SHAP 기반 요인 분석** - 사용자의 수면에 가장 큰 영향을 미치는 생체 지표 시각화
- **Gemini AI 수면 코칭** - ML 분석 결과 + 생활습관 데이터 + 증상 정보를 Gemini 2.5 Flash에 전달하여 맞춤형 수면 가이드 및 오늘 밤 실천 미션 생성
- **5-Fold 교차검증** - 모델의 안정성과 일반화 성능 검증

### 수면 페르소나

RF의 전역 피처 중요도(Importance)와 사용자 값의 분포 극단성을 곱하여 개인별 방해 요인 1위를 도출하고, 이를 수면 상태 분류 결과와 결합하여 총 6가지 페르소나를 결정합니다.

기여도 점수 = Importance × |pct − 0.5| × 2
페르소나	수면 상태	주요 기여 요인	위험도
Recovery Booster	Normal	걸음 수 또는 수면의 질	낮음
 Deep Rest	Normal	나이·심박수·스트레스 등 기타 요인	낮음
Stress Sleeper	Insomnia	스트레스 수준	높음
Irregular Rhythm	Insomnia	나이·BMI·심박수 등 기타 요인	중간
Obstructive Apnea Risk	Sleep Apnea	BMI 또는 혈압	높음
Apnea Risk	Sleep Apnea	나이·BMI·심박수 등 기타 요인	높음

시스템 구조
<img width="2048" height="2952" alt="image" src="https://github.com/user-attachments/assets/0d2a05a6-95a2-4d75-80b8-4fbc2d796106" />

기술 스택
분류	기술 및 라이브러리
언어	Python 3
ML / 모델링	RandomForestClassifier, NearestNeighbors, StratifiedKFold, StandardScaler
설명 가능성 AI	SHAP (TreeExplainer)
LLM	Google Gemini 2.5 Flash
데이터셋	Kaggle — Sleep Health and Lifestyle Dataset
실행 환경	Google Colab

### 데이터셋

- **출처:** Kaggle — Sleep Health and Lifestyle Dataset
- **사용 피처:** 나이, 성별, BMI, 혈압(수축기/이완기), 심박수, 일일 걸음 수, 스트레스 수준, 수면의 질, 수면 시간
- **예측 타겟:** 수면 상태 분류 (Normal / Insomnia / Sleep Apnea)

### 팀원
팀원명	GitHub ID
강민주	minjoo050830
윤선화	
장지나	jinasy-hash

모든 팀원이 데이터 전처리, 모델링, 프롬프트 엔지니어링, 문서화 등 프로젝트 전 과정에 함께 기여하였습니다.
