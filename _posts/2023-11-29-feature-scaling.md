---
title: Standardization, Normalization 헷갈려
author: haley
date: 2023-11-29 10:00:00 +0800
categories: [Blogging, MachineLearning]
tags: [study, ML]
---


## Feature Scaling 필요한 알고리즘

- Gradient Descent Based Algorithms (민감O)
    - Linear Regression, Logistic Regression, Neural Network
    - 경사하강법에서 x값은 경사하강법의 단계의 크기에 큰 영향을 미치므로, 경사하강이 최소값으로 부드럽게 이동하고, 하강 단계가 모든 특징에 대해 동일한 속도로 업데이트 되도록 하기 위해 피처 스케일링이 필요 → 파라미터 업데이트 시 일정하게 업데이트 위해
- Distance Based Algorithms (민감O)
    - K-Nearest Neighbors, K-means, SVM
    - 데이터 점들간의 거리로 유사성을 판단하기 때문에 피처의 크기에 영향을 받음
    - 스케일링 전과 후의 유클리드 거리(Euclidean distance)가 변하는걸 생각하면 됨
- Tree Based Algorithms (민감X)
    - Decision Tree, Bagging, Random Forest, Boosting 등
    - 결정 트리는 특징을 기반으로 노드를 분류해나가기 때문에 feature scale에 민감하지 않음 (=표준화 안해도 큰 영향 없음)

<aside>
💡 1. Feature Scaling 방법이라고 할 때 → sklearn에서 말하는 scaler들이 있는 것!
2. Normalization 한다고 할 때 → 정규화 안에 표준화가 포함되어 있는 것!
3. 정규화/표준화를 정의적으로 구분지어서 말할 수도 있는 것!
</aside>

## Normalization, 정규화

- 데이터셋의 numerical value 범위의 차이를 왜곡하지 않고 공통 척도로 변경하는 것이 목적
- 대표적인 방법으로는 표준화(z-score standardization)과 최소극대화(minmaxscaler) 정규화가 있음
- 학습 데이터에서는 성능 좋지만 테스트 데이터에서는 성능이 낮을 때 의심해 볼 수 있는 것
    - 단순 overfitting 문제가 아니라 두 데이터의 분포가 달라서인 경우도 있음
- 데이터 간 분포가 다르면, 각 분포에 맞춰 모델 업데이트 과정에서 학습이 제대로 이루어지지 않을 수 있음 + 속도도 느릴 수 있음
- 위 문제를 정규화 실행 시 아래와 같은 이점이 있음
    - local minima 방지, 빠른 최적화
    - internal covariate shift 줄일 수 있음
    - loss function 매끄럽게 함(정규화로 기울기 크기 제한)
- 자세한 내용은 reference 3번째 글 참조

## Standardization, 표준화

- StandardScaler → 평균=0 분산=1 되게 조정, 표준정규분포의 속성을 갖도록 feature rescaling
- z-score = x_scaled = (x - mean) / std
- 모든 feature들을 공통의 척도로 변경해 주는게 목적

```python
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train) # or scaler.fit(X_train); X_train = scaler.transform(X_train)
X_test = scaler.transform(X_test)
```

- 헷갈리기 쉬운 것
    
    fit() → training 시키는 것
    transform() → trained model의 mean, variance에 맞도록 transformation   
    fit_transform() → training and transformation
    

## + Log transformation

- skewed 되어있는 데이터의 왜곡을 줄이기 위한 것이기 때문에 정규화 이전에 선행되어야 함
- 정규성을 높이고 분석에서 정확한 값을 얻는 것이 목적
    
    1. 큰 수를 작게 만들고
    
    2. 그로 인해 복잡한 계산을 쉽게 만들고
    
    3. 왜도와 첨도를 줄여서 데이터 분석 시 의미있는 결과를 도출
    

## + Regularization, 정칙화

- 정규화, 정칙화, 규제화, 규칙화 다양하게 부름
- 학습 데이터에만 너무 특화되지 않고 ‘일반화(generalization)’가 가능하도록 일종의 규제(penalty)를 가하는 기법
- 주로 overfitting 막기 위해 하이퍼파라미터 수정하는 방식(weight 조정)
- L1(LASSO) regularization, L2(Ridge) regularization

**비교 정리**

| Normalization | Standardization |
| --- | --- |
| 값의 범위를 0~1사이 값으로 변경 | 값의 평균=0, 분산=1로 변경 (특정 범위로의 값 제한 없음) |
| 최대, 최소값 사용 | 평균, 표준편차 사용 |
| feature 크기 서로 다를 때 사용 → scale 큰 feature 영향 커지는 것 방지 | feature 크기 서로 다를 때 사용 → scale 큰 feature 영향 커지는 것 방지 |
| DL학습 속도 향상, local minima 빠질 위험 감소 | DL학습 속도 향상, local minima 빠질 위험 감소 |
| 분포에 대해 모를 때 유용
(KNN 및 Neural Network처럼 데이터의 분포를 가정하지 않는 알고리즘에서 유용) | 피처가 정규분포(가우시안 분포)인 경우 유용 (꼭 그렇지 않아도 됨)
(경계 범위가 없기 대문에 데이터에 outlier 있어도 표준화에 영향을 받지 않을 것) |
| MinMaxScaler, MaxAbsScaler | StandardScaler, RobustScaler |
- 기타 Data Scaling 기법
    - MinMaxScaler → 최대값=1, 최소값=0으로 조정, 아웃라이어에 취약,  x’ = (x - x_min) / (x_max - x_min)
    - RobustScaler → ****중앙값=0, IQR(1분위~3분위값)=1로 조정, 아웃라이어 영향을 최소화, 정규분포 보다 더 넓게 분포
    - MaxAbsScaler → 0 기준으로 절대값이 가장 큰 수가 1 or -1이 되도록 조정, 양수로만 구성된 데이터셋에서는 아웃라이어에 민감

<aside>
💡 - 모든 스케일러 처리 전에는 Outlier Rejection 선행되어야 함(IQR 등)
- 데이터의 분포 특징에 따라 적절한 스케일러를 적용해주는 것이 좋음
- 스케일링시 Feature별로 크기를 유사하게 만드는 것은 중요하지만, 그렇다고 모든 Feature의 분포를 동일하게 만들 필요는 없음
</aside>


- 기타 StandardScaler적용 된 Z_price 에 변환 가능한 것들. 표준 점수의 일종
    - **T점수(표본점수)** → df[’T_price’] = 10*df[’Z_price’] + 50 ⇒ 평균=50, 표준편차=10
    - **스태나인(stanine)점수** → (ex. 수능등급) 이걸 활용하면 일종의 범주형 변수를 만들 수 있을 듯!
        - s = (2*df[’Z_price’] + 5.5).astype(int) ⇒ 싼차(1) ~ 비싼 차(9)
        - s = (-2*df[’Z_price’] + 5.5).astype(int) ⇒ 싼차(9) ~ 비싼 차(1)
        - s[s<1]=1, s[s>9]=9 로 만들기


---
---
**Reference**
https://bskyvision.com/849  
https://hleecaster.com/ml-normalization-concept/  
https://hyen4110.tistory.com/20  
https://dacon.io/forum/406086  
https://mkjjo.github.io/python/2019/01/10/scaler.html  
[https://velog.io/@cosmicdev/데이터-분석-로그-변환](https://velog.io/@cosmicdev/%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%B6%84%EC%84%9D-%EB%A1%9C%EA%B7%B8-%EB%B3%80%ED%99%98)