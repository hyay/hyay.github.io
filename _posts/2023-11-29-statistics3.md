---
title: 03. 신뢰구간
author: haley
date: 2023-11-29 10:00:00 +0800
categories: [Blogging, Statistics]
tags: [study, stats]
---

<aside>
💡 신뢰 구간과 CLT, python 코드와 함께  **⇒ 다시 정리**
</aside>

---

## 신뢰 구간, p-value
> 가설 검정을 하기 전에 필수적으로 알아야하는 것

- **신뢰수준**(confidence level): 모수가 추정된 신뢰구간에 포함되는 표본의 비율(양극단 값 제외한 범위)
    
    
    | 신뢰수준 | 유의수준(양측, 단측) | Z 표준화 값 |
    | --- | --- | --- |
    | 90% | 10%, 5% | 1.287,  1.65 |
    | 95% | 5%,  2.5% | 1.645,  1.96 |
    | 99% | 1%,  0.5% | 2.325,  2.58 |
    - 신뢰수준이 높을수록, 표본이 작을수록, 데이터 자체의 변산성이 클수록 → 오차범위가 넓다
        - 표본이 클수록 오차범위가 좁음  (*헷갈리는 것!*)
            - 표본 한 개가 큰 것(한번의 조사를 많은 대상에게 함) → 오차 범위 적어짐
                - 큰 표본(하나의 부분집합 안에 사례가 많음) = 회사가 큼
            - 다양한(많은) 표본을 생각하는 것 → 오차 범위 커짐
                - 많은 표본(부분집합이 여러개 있음) = 회사가 많음
- **신뢰구간**(Confidence Interval) = 통계량 ± 오차범위
    - 평균의 신뢰구간(CI) 추정

```python
# 방법 1. 직접 계산
from scipy import stats
x = np.linspace(평균 - 4 * 표준오차, 평균 + 4 * 표준오차, 1000)
# 방법1. 직접 계산
stats.t.pdf(x, df=표본크기-1, loc=평균, scale=표준오차)
임계값 = -stats.t.ppf(1 - (1-신뢰수준)/2), df=표본크기-1) # = 1.96
오차한계 = 임계값 * 표준오차
하한, 상한 = 표본평균 - 오차한계, 표본평균 + 오차한계

# 방법 2. pingouin 사용
import pingouin as pg 
pg.ttest(df.price, 0, confidence=0.95) # 평균의 신뢰구간 구하기(CI95%)

# 방법 3. scipy interval 사용
import scipy.stats as stats 
stats.t.interval(0.95, df=len(df)-1, loc=df.price.mean(), 
								 scale=df.price.std()/np.sqrt(len(df)))
# stats.t.interval(신뢰수준, df=표본크기-1, loc=평균, scale=표준오차)
# 표준오차 = 표준편차/np.sqrt(표본크기)
```

- **Bootstrapping 이용한 신뢰구간 추정**
    - 원리: `df.price.sample(n, replace=True).mean()` → 샘플링 x10000번 반복 수행
        - 시뮬레이션 결과의 동일성을 보장할 수 없지만 **큰수의 법칙**에 의해 동일한 결과로 수렴
    - 표본이 충분할 때(n≥30) 모평균의 신뢰구간 추정

```python
mu = 0.5 # 모평균
num_simul = 10000
max_sample_size = 30
coverage_ratios = []
ns =[]
n = 10
sample = np.random.normal(mu, scale=1, size=n)
se = scipy.stats.sem(sample) # 표준 편차
# 원리: 아래 신뢰구간이 모평균을 커버한다
stats.t.interval(confidence_level, df=n-1, loc=np.mean(sample), scale=se) 

# 방법 1. 시뮬레이션
# 아래 np.random.uniform(0,1,size=(num_simul, n))이여도 동일(normal, uniform 상관x)
for n in range(2, max_sample_size+1):
	sample = np.random.normal(mu, scale=1, size=(num_simul, n))
	se = scipy.stats.sem(sample, axis=1) # 표준 편차
	lowers, uppers = stats.t.interval(0.95, df=n-1, loc=np.mean(sample,axis=1), scale=se) 
  count = np.sum((lowers<=mu)&(mu<=uppers))
  coverage_ratios.append(count/num_simul)
  ns.append(n)
plt.plot(ns, coverage_ratios)
plt.axhline(y=0.95, color='red', linestyle='--')

# 방법 2. scipy 함수 활용
import scipy.stats as stats 
stats.bootstrap([df.price], np.median, n_resamples=10000, confidence_level=0.95)
```

- **큰 수의 법칙**
    - 수학적 확률 = 논리적 추론을 통해 알 수 있는 확률 (ex. 주사위 눈 확률 1/6)
    - 통계적(경험적) 확률 = 실제 시행을 하게되면 나오는 확률 (ex. 실제로 1/6이 안나올 수 있음)
    - 수학적 확률과 통계적 확률이 일치하지 않지만, 무수히 많이 반복하다보면 결국에 같아진다는 것이 큰 수의 법칙
- **중심극한정리(CLT, Central Limit Theorem)**
    - 표본의 크기를 극한으로 근사시킬 때 표본평균의 분포는 중심으로 모이게 된다. 
    (확률변수의 표본의 크기 n = 30, 100, … , 무한대로 커지면) (분포=샘플링한 결과)
    - 어떤 확률변수의 평균은 정규분포를 따른다 → 중심극한정리에 의해 정규분포 얻게되는 것
    - 이 분포의 평균은 모평균의 평균을, 분산은 모분산을 표본크기로 나눈 값을 따른다
    - 평균은 모평균과 같아졌고, 분산의 크기는 매우 작아짐((모집단 분산/샘플 수) 만큼)
        
        !https://s3-us-west-2.amazonaws.com/secure.notion-static.com/638b2d6e-3e74-4a16-9517-d134c7ab25f1/Untitled.png
        
- **p-value**
    - 관행적인 이유도 있고, 계산이 편한 이유가 있어서 신뢰구간 보다 p-value 많이 씀
    - 모수에 대한 특정한 가설과 통계량이 일치함을 보여주는 지표
    - 표집분포에서 모수를 특정 값으로 가정할 때, 표본평균 바깥쪽 영역의 넓이
    - 가정된 모수가 신뢰구간을 벗어남/포함됨 을 결정하는 기준으로 활용(p-value와 유의수준(0.05) 비교)
    - pg.ttest(df.price, target_value) → CI95% 들어가는지에 대한 p-value 보면 됨
        - 0.05넘으면 신뢰구간 포함, 미만이면 신뢰구간 벗어남
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/72da19c7-016b-4b17-b9cd-fe45f7c17a35/Untitled.png)
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4aa694d1-ec8a-4af4-84d3-1b1f6cad5ee0/Untitled.png)
        
    - 관찰 통계량과 귀무가설 차이 ↑ → p-value ↓
    - 표본의 크기 ↑  → p-value ↓
        - 데이터를 많이 모을수록 신뢰구간은 좁아지고 p-value는 작아지니까
            - 표본 수 클수록(조사 대상이 많을수록=데이터 많을수록) 오차범위 커지니까 신뢰구간은 좁은 것, p-val은 작은 것
            - 표본 한개의 크기(반복수행) 클수록 오차범위 작아지니까 p-val은 큰 것?
    - 표본의 크기 ↑ → 신뢰 구간 ↓
        - 모집단=1000, 표본(10 vs 1000)일 때,   
        전수조사 = 오차범위x = 신뢰구간 있을 필요x → 신뢰구간 좁아짐
        - 동전 던지기 1번 vs 10번 앞면 확률 → 1/2 vs 1/1024
    - 표본으로 모집단을 추정 → 표본의 개수 결정?
        - ROI 관점에서는 표본이 무조건 크다고 좋은 것이 아님 → 그만큼 비용이 많이 들어가니까
        - 적절한 표본의 크기를 어떻게 결정할지가 비즈니스 의사결정에 있어서 중요요소로 작용함

---

## 암기하자1

- **모비율 신뢰구간 표본 크기 결정 → $n = \frac{Z^2 \cdot p \cdot (1-p)}{E^2}$**
    - ex. 불량률 10%, 신뢰수준 95%, 허용오차 1%   
    → n = (1.96)**2*0.1*(1-0.1) / 0.01**2 = 1383
- **모평균 신뢰구간 표본 크기 결정 → $n = \frac{Z^2 \cdot \sigma^2}{E^2}$**
    - ex. 모평균 500g, 모표준편차 10g, 신뢰수준 95%, 허용오차 5g   
    → n = (1.96)**2*(10)**2 / 5**2 = 384

---

## 암기하자2

- **신뢰구간에 영향을 주는 요소**
    - 신뢰 수준 ↑  →  신뢰구간 ↑
    - 표본의 크기 ↑  →  신뢰구간 ↓
    - 변산성(불확실성) ↑  →  신뢰구간 ↑
- **p-value에 영향을 주는 요소**
    - 가설과 통계량의 거리 ↑  →  p-value ↓
    - 표본의 크기 ↑  →  p-value ↓
    - 변산성(불확실성) ↑  →  p-value ↑

---
---
**Reference**

- 유튜브 DDL 강의
- 통계 온라인 강의