# AI Based Dementia Prediction

## 프로젝트 개요
[AI-Hub의 웨어러블 데이터](https://aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=data&dataSetSn=226)를 사용, 치매 확률을 예측하는 AI 모델을 개발하는 프로젝트입니다.  
심박수, 걸음수, 수면 시간 등의 라이프로그 데이터를 분석하고, **LSTM 기반의 시계열 모델**로 시간적 패턴을 학습하도록 설계하였습니다.

현재는 라이프로그 데이터에 사용자별 **MMSE(Mini-Mental State Examination)** 데이터를 포함하여 LSTM 기반 모델을 제작했습니다.  
**향후에는 MMSE 데이터를 제거하고 라이프로그 데이터만으로 치매 의심자를 예측하는 모델을 구현할 예정입니다.**  

또한, **3가지 AI 모델(LSTM 및 다른 두 모델)을 비교**하여 가장 적합한 모델을 탐구하고,  
각 사용자의 이메일을 입력하면 관련 정보를 시각화하는 **웹사이트 형태의 서비스**로 확장할 계획이며, **사용자가 이메일을 입력하면 개인화된 데이터를 제공하는 모바일 어플 제작**도 고려 중에 있습니다.

프로젝트의 진행 상황에 따라 **README를 지속적으로 업데이트**할 예정입니다.

---

## **기술 스택**

- **언어**:  
  - Python  

- **프레임워크 및 라이브러리**:  
  - **PyTorch**: `torch`, `torch.nn`, `torch.optim`, `torch.utils.data`  
  - **Scikit-learn**: `train_test_split`, `StratifiedKFold`, `MinMaxScaler`, `OneHotEncoder`, `SimpleImputer`  
  - **Imbalanced-learn**: `RandomOverSampler`  

- **데이터 처리 및 분석**:  
  - **Pandas**: `pd.DataFrame` 등 데이터 조작 및 분석  
  - **NumPy**: `np.array` 등 수치 데이터 처리  

- **모델 학습 관리 및 시각화**:  
  - **Weights & Biases (wandb)**: 실험 및 하이퍼파라미터 튜닝 관리  

- **데이터셋 관련 모듈**:  
  - `TensorDataset`, `DataLoader` (PyTorch 기반 데이터셋 관리)

---

## 방법론 (MMSE 데이터를 포함할 때)
- **데이터**: AI-Hub 웨어러블 라이프로그 데이터
- **데이터 전처리**:
  - 결측값 처리: 선형 보간법 적용
  - 데이터 병합: 이메일을 기준으로 다중 데이터셋 병합
  - 비수치형 데이터 제거
  - One-hot Encoding: MMSE 데이터의 3개 카테고리(CN(정상), Dem(치매), MCI(경도인지장애))에 대해 수행
- **중복 데이터 처리**:
  - 중복된 수치 데이터(몇십만 건)를 탐지하여 제거
- **모델**:
  - LSTM(Long Short-Term Memory) 기반의 시계열 데이터 모델링

---

## 주요 성과
- **모델 성능(MMSE 데이터를 포함한 LSTM 모델)**:
  - Validation 데이터 기준:
    - **Accuracy: 60% ~ 84%**
    - **Loss: 0.4 ~ 0.5**
  - Test 데이터 기준:
    - **Accuracy: 약 70%**
    - **Loss: 0.54 ~ 0.68**

---

## 이후 계획
  - **Test 데이터에서 정확도가 낮은 이유를 분석하고 보유한 원천 데이터를 분석하여 전처리를 다시 진행할 예정.**
  - 하이퍼파라미터 튜닝 및 성능 개선
  - MMSE 데이터를 제외한 모델 실험: 보유한 라이프로그 데이터(수면 데이터, 걸음거리 데이터)만으로 LSTM 모델 제작 및 성능 평가 예정.
  - LSTM 모델 외에 2가지 모델을 추가로 제작하여 주어진 라이프로그 데이터에 가장 적합한 모델을 비교 분석할 예정.

---

## 개인 기여
- **데이터 전처리 및 분석**: 결측치 처리, 이메일 기준 데이터 병합, 중복된 수치 데이터 제거.  
- **모델 설계 및 성능 평가**: LSTM 모델 구조 설계 및 하이퍼파라미터 최적화 진행.  
- **프로젝트 결과 보고 및 자료 작성**: 전처리 과정, 모델 성능 결과를 시각화하여 PPT 및 리포트 작성.

---

## 참고 자료
- 데이터셋: [AI-Hub 웨어러블 라이프로그 데이터](https://aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=data&dataSetSn=226)
