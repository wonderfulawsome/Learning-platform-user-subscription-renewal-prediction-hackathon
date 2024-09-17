# 학습 플랫폼 이용자 구독 갱신 예측 AI 해커톤

## 1. 프로젝트 설명


### 주제
**학습 플랫폼 이용자의 구독 갱신 여부**를 예측하는 AI 알고리즘을 개발하는 것이다.

### 목표
이용자의 구독 기간, 로그인 활동, 학습 세션 참여도 등을 분석하여 학습 플랫폼 이용자의 구독 갱신 여부를 정확하게 예측하는 AI 모델을 개발하는 것이다.

## 2. 데이터 설명

데이터는 다음 네 가지 파일로 구성되어 있다:

### 1. `train_data.csv`
- **구성**: 학습에 사용될 데이터셋으로, 이용자의 구독 활동, 로그인 기록, 학습 활동 등 다양한 정보를 포함한다.
- **주요 변수**:
  - `subscription_duration`: 이용자가 구독한 기간.
  - `recent_login_time`: 최근 로그인 시간.
  - `average_login_time`: 평균 로그인 시간.
  - `total_completed_courses`: 완료한 코스 수.
  - `monthly_active_learning_days`: 월별 활성 학습 일수.
  - `target`: 구독 갱신 여부를 나타내는 목표 변수 (1: 갱신, 0: 미갱신).

### 2. `test_data.csv`
- **구성**: 학습된 모델로 예측할 테스트 데이터셋으로, `target` 값을 제외한 특성으로 구성되어 있다.

### 3. `data_info.csv`
- **구성**: 각 데이터 컬럼의 설명을 포함한 정보 파일이다.

### 4. `sample_submission.csv`
- **구성**: 제출 형식 파일로, 예측된 `target` 값을 채워 제출하는 데 사용된다.

## 3. 코드 설명

### `RandomForest, GradientBoost, HyperParameter.ipynb`
이 노트북에서는 랜덤 포레스트, 그래디언트 부스팅 모델을 사용해 구독 갱신 예측 모델을 개발하고, 하이퍼파라미터 튜닝을 수행한다.

#### 주요 단계:
1. **데이터 로드 및 확인**: `train_data.csv`와 `test_data.csv`를 로드하여 데이터의 결측값을 확인하고, 통계량을 파악한다.
2. **데이터 전처리**: 범주형 변수를 수치형으로 변환하기 위해 `LabelEncoder`를 사용하고, 필요한 경우 결측값을 처리한다.
3. **특성 생성**: 추가적인 학습 인사이트를 위해 `total_learning_time`, `login_time_difference`, `course_completion_rate`와 같은 특성을 생성한다.
4. **모델 학습**: Random Forest, Gradient Boosting 모델을 사용해 학습하고, 성능을 평가한다.
5. **하이퍼파라미터 튜닝**: `RandomizedSearchCV`를 사용해 Gradient Boosting 모델의 최적 하이퍼파라미터를 찾는다.
6. **모델 평가**: 최적화된 모델을 검증 데이터셋에서 평가하고, 정확도, 정밀도, 재현율, F1 점수를 계산한다.

### `Read2`
이 파일에서는 기초 통계량을 설명하고, 데이터 전처리 과정 및 새로운 특성 생성을 위한 설명을 제공한다.

#### 주요 내용:
- **기초 통계량**: 각 특성의 평균, 표준편차, 최솟값과 최댓값을 설명.
- **누락된 값 확인**: 모든 특성에서 결측값이 없음을 확인함.
- **범주형 변수 인코딩**: 범주형 변수를 `LabelEncoder`로 수치형으로 변환하는 과정.
- **특성 생성**: `total_learning_time` (총 학습 시간), `login_time_difference` (최근 로그인 대비 평균 로그인 시간 차이), `course_completion_rate` (코스 완료율) 등의 새로운 특성을 생성함.
- **모델 성능 비교**: Logistic Regression, Random Forest, Gradient Boosting 모델의 성능을 비교 분석함.

### 주요 모델 성능 비교:
- **Logistic Regression**: 재현율과 정확도가 높은 모델로 평가됨.
- **Random Forest**: 비교적 낮은 성능을 보임.
- **Gradient Boosting**: 정확도, 재현율, F1 점수에서 가장 균형 잡힌 성능을 보임.
