# AI Based Dementia Prediction

## 프로젝트 개요

이 프로젝트는 웨어러블 기기의 라이프로그 데이터를 활용하여 치매를 조기에 예측할 수 있는 AI 모델을 개발하는 것입니다. 치매는 조기 발견이 매우 중요한 질환이며, 조기 진단을 통해 환자와 가족의 삶의 질을 개선할 수 있습니다. 본 프로젝트에서는 AI-Hub에서 제공하는 데이터를 사용하여 치매 고위험군을 예측하고자 하며, 주된 목표는 LSTM 모델을 기반으로 한 시간순 데이터 분석을 통해 치매를 보다 정확하게 예측하는 것입니다.

## 데이터셋

### 데이터 출처
- AI-Hub에서 제공하는 치매 고위험군 웨어러블 라이프로그 데이터 및 생활습관 데이터를 사용하였습니다.

### 데이터 구성
- **Activity Data**: 웨어러블 기기를 통해 기록된 신체 활동 데이터입니다.
- **Sleep Data**: 웨어러블 기기를 통해 기록된 수면 데이터입니다.
- **MMSE Data**: Mini-Mental State Examination(간이정신상태검사) 데이터를 포함하였습니다. MMSE는 인지 기능을 평가하기 위한 검사입니다.
- 데이터들은 **train, validation** 셋으로 나누어져 있습니다.

## 모델 아키텍처

본 프로젝트에서는 순환 신경망(RNN) 계열의 **LSTM(Long Short-Term Memory)** 모델을 사용하였습니다. LSTM은 시계열 데이터의 패턴을 효과적으로 학습할 수 있어, 시간에 따른 상태 변화를 예측하는 데 적합합니다.

### 모델 구조
- **입력층**: 웨어러블 데이터를 입력받아 시간 순서대로 분석합니다.
- **LSTM 계층**: 데이터의 시간적 의존성을 파악합니다. **256개의 hidden units**을 사용하였습니다.
- **Fully Connected Layer**: 최종적으로 치매 고위험군(CN, Dem, MCI)을 분류합니다.
- **출력층**: One-hot 인코딩된 3개의 클래스를 출력합니다.

### 학습 방법
- **손실 함수**: BCEWithLogitsLoss를 사용하여 다중 클래스 분류 문제를 해결합니다.
- **옵티마이저**: **AdamW**와 **SAM(Sharpness-Aware Minimization)**를 결합하여 학습을 안정화하고 성능을 높였습니다.
- **에폭(Epochs)**: 총 **100 epochs** 동안 학습을 진행하였습니다.

## 데이터 전처리

- **결측치 처리**: 선형 보간법을 사용하여 각 사용자별 결측치를 보완하였습니다.
- **One-Hot Encoding**: 진단명(DIAG_NM)을 One-Hot Encoding하여 모델의 입력으로 사용하였습니다.
- **중복 데이터 제거**: EMAIL과 주요 지표를 기준으로 중복된 데이터를 제거하여 데이터의 순도를 높였습니다.

## 주요 결과
- **훈련 정확도 및 손실**: 모델 학습 중 WandB를 통해 실시간으로 로그를 기록하였습니다.
- **평가 지표**: 모델의 성능은 정확도(Accuracy)로 평가되었으며, validation 정확도를 통해 과적합 여부를 판단하였습니다.

## 설치 및 실행 방법

1. **필수 라이브러리 설치**:
   ```sh
   pip install -r requirements.txt
   ```

2. **데이터 준비**:
   - 데이터를 `Lifelog_data/Processed` 디렉토리에 저장합니다.

3. **모델 학습**:
   ```sh
   python train.py
   ```

4. **모델 테스트**:
   ```sh
   python test.py
   ```

## 파일 구조

```
AI_Based_Dementia_Prediction/
├── Lifelog_data/
│   ├── Processed/
│   │   ├── train_data.csv
│   │   └── val_data.csv
├── LSTM_with_mmse_data.ipynb
├── train.py
├── test.py
└── README.md
```

## 사용된 도구 및 기술
- **프로그래밍 언어**: Python
- **딥러닝 프레임워크**: PyTorch
- **데이터 전처리**: Pandas, NumPy
- **모델 최적화**: SAM (Sharpness-Aware Minimization)
- **시각화 및 로깅**: WandB (Weights & Biases)

## 기여
- 이 프로젝트는 데이터 과학 학부생들의 팀 프로젝트로 수행되었습니다.
- 주요 기여자: ClearSky001 (GitHub 아이디)

## 참고 문헌 및 자료
- [AI-Hub 데이터셋 링크](https://aihub.or.kr/)
- [Weights & Biases 사용법](https://wandb.ai/site)

## 라이선스
- 본 프로젝트의 코드 및 데이터는 연구 및 학습 목적으로만 사용 가능합니다.

## 문의
- 프로젝트 관련 문의사항은 GitHub 이슈나 [이메일](mailto:clearsky001@example.com)을 통해 연락해주세요.
