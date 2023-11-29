---
title: 04. 가설검정(작성 중)
author: haley
date: 2023-11-29 10:00:00 +0800
categories: [Blogging, Statistics]
tags: [study, stats]
---

<aside>
💡 제일 내용이 많고 중요한 부분
</aside>

---

## 가설 검정
> T-test,

- **통계적 가설검정**(statistical hypothesis testing): 특정한 가설(=귀무가설)을 배제하기 위한 절차
- 
- T-test
    - 두 집단 평균 비교 pg.ttest(A,B) → A집단과 B집단의 평균이 같다(⇒ A집단 평균 - B집단 평균 = 0)
    - 단일 집단의 평균 비교 pg.ttest(A, 10) → A집단의 평균이 10이다

```python
# 등분산성 검정 => Levene 검정
pg.homoscedasticity(dv='price', group='model', data=df)
stats.levene(df.price[df.model='A'], df.price[df.model='B'])

# 위 결과가 이분산 집단으로 나왔다면, scipy.stats 사용 시
stats.ttest_ind(df.price[df.model='A'], df.price[df.model='B'], equal_var=False)

# pingouin 사용 시
pg.ttest(df.price[df.model='A'], df.price[df.model='B'], correction='auto')
# 'auto' 옵션으로 설정 시, 자동으로 Welch T-test 수행하므로 따로 등분산성 검정할 필요 없음
```

- 단측 검정
- ㅇㅇㅇ

- 모수적 방법(Parametric Methods)
    - 수식이 복붙되는지는 원본 pdf다운받아서 붙여넣기 (p20)
- 비모수적 방법(Non-parametric Methods)
    - f의 함수 형태에 대해 명시적인 가정을 하지 않음
    - 장점:  f의 함수 형태에 대한 가정을 하지 않아도 되므로 더 넓은 범위의 f형태에 정확하게 적합될 가능성이 있음
    - 단점:  정확한 f추정을 위해서는 모수적 기법에서 보통 필요로하는 것 보다 훨씬 많은 수의 관측치 필요

- 인과관계를 알기 위해서는 무작위 통제실험(=A/B테스트)를 수행해야 함
    - 상관관계가 인과관계가 아님(ex. 앱삭제율과 구매 포기가 양의 상관관계 → 구매 단계 복잡도가 원인)
    - 무작위 통제 실험 (A/B테스트) 방법
        
        - 표본이 모집단을 대표하도록 조사 대상자들을 선정함(무작위 추출 등)
        - 조사 대상자들을 실험군 혹은 대조군 중 하나의 집단으로 무작위로 임의 배정
        - 실험군에는 알아보고자하는 독립변인 하나만을 조작하고 나머지 모든 조건은 대조군과 일치시킴
        - 참가자를 각 집단에 무작위 임의 배정하여 독립변수 외 다른 변수의 영향이나 기타 편향을 방지함
        
- 네이만-피어슨 추론 방식
    - 알지 못하는 모집단에 대해서 표본이 모집단과 같다/아니다에 대한 가설 설정

## T-test

- T-검정
- 비모수 버전

## ANOVA test

## Chi-squared test

- 카이 제곱 검정
    - 동질성 검정 - 지역에 따른 호흡기 질환 발병 여부 → 지역(독립변수, A/B/C) → 발병여부(종속변수, 발병O/발병X)
        - 발병O의 빈도, 발병X의 “빈도”를 가지고 비교
    - 독립성 검정 → 자동차의 크기(독립변수, 경/중/소/대) → 가족의 형태(종속변수, 1인/유/무)
    - 기본적으로 두 방법 모두 범주형 변수의 차이/관련 유무를 비교함
    - **절차**
        1. 표본 데이터 요약 (관측 빈도) → pivoting
        2. 귀무가설이 참이라 가정할 때, 모집단의 기대빈도 → (행합계*열합계)/표본 빈도 총합계
        3. 기대 빈도와 관측 빈도의 차이 
        4. 카이제곱(x^2) 검정 통계량 → (관측 빈도 - 기대 빈도)^2 / 기대빈도