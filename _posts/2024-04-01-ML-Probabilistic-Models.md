---
title: "[ML] Probabilistic Models"
author: ramraid
date: 2024-04-01 20:00:00 +0800
categories: [Computer Science, Machine Learning]
tags: [Machine Learning, Linear Algebra]
toc: true
comments: true
math: true
mermaid: false
# image:
#     path: /assets/img/cat.png
#     alt: 선형 회귀 :/
# render_with_liquid: false
pin: false
---

# Probabilistic Models

## Inferring Rudimentary Rules

- instance set를 분류하는 가장 간단한 규칙을 1R 이라고 한다.
- 하나의 특정 속성을 모두 테스트하는 규칙 집합의 형태로 표현된 one-level decision tree를 생성한다.
    - 때로는 하나의 특성이 Class를 결정하는데 충분하다. ex. 🦄 vs 🦓
- 하나의 특성과 branch를 테스트하는 규칙을 만든다.
- 각 branch는 특성의 서로 다른 값에 대응한다.
- 훈련 데이터가 최상의 결과를 (더 자주) 내는 Class를 이용한다.
- Error rate는 훈련 데이터에서의 error 수로 결정된다.
- 각 attribute는 서로 다른 규칙 set을 생성한다.
- 각 attribute의 규칙에 대해 error rate가 가장 좋은 것을 고른다.

## Missing Values and Numeric Attributes

> Numeric Attributes는 기본적으로 정규분포나 Gaussian 확률 분포를 따른다고 가정한다.
{: .prompt-info }

- 1R은 missing value와 numeric attribute도 수용 가능

> missing value는 다른 attribute value로 처리된다. ex. {sunny, rainy, MISSING}
{: .prompt-info }

![Breakpoints](assets\img\posts\MachineLearning\ML-Probabilistic-Models\ML-Probabilistic-Models-01.png){: width="985" height="157" }

- 훈련 데이터를 Numeric value로 정렬, 정렬된 sequence는 braking points로 나뉘어짐

> 같은 value인데 다른 class로 나뉘는 경우? breakpoint를 옮겨 no가 더 많은 mixed partition을 만듦.
{: .prompt-info }

![NumericAttributes](assets\img\posts\MachineLearning\ML-Probabilistic-Models\ML-Probabilistic-Models-02.png){: width="945" height="156" }

- 너무 branching를 세세하게 하면, overfitting이 발생한다. overfitting을 피하기 위해서, 각 partition이 minimum number의 majority example을 갖게 해야한다.

![NumericAttributes](assets\img\posts\MachineLearning\ML-Probabilistic-Models\ML-Probabilistic-Models-03.png){: width="940" height="105" }

- majority class가 같은 partitions는 합칠 수 있다.

## Simple Probabilistic Modeling

- Conditional Probability
  
$$P(Y|X)=\frac{P(X\cap Y)}{P(X)}$$

- Independence
  
$$P(Y|X)=\frac{P(X\cap Y)}{P(X)}=\frac{P(X)P(Y)}{P(X)}=P(Y)$$

- Bayes' Theorem
  
$$P(A\cap B)=P(A)P(B|A)=P(B)P(A|B)$$
$$P(A|B)=\frac{P(B|A)P(A)}{P(B)}$$

  - $P(A|B)$ : posterior (사후확률), 사건 B가 발생한 후 갱신된 사건 A의 확률
  - $P(A)$ : prior (사전확률), 사건 B가 발생하기 전에 가지고 있던 사건 A의 확률
  - $P(B|A)$ : likelihood (가능도), 사건 A가 발생한 경우 사건 B의 확률
  - $P(B)$ : normalizing constant, evidence (정규화 상수, 증거), 확률의 크기 조정

#### Naive Bayes

$P(C|x_1,...x_n)=aP(x_1,...,x_n)P(C)=\alpha P(C)\prod_i P(x_i|c)$

e.i.
$$P(Yes|Sunny, Cool, High, True)∝P(Sunny|Yes)P(Cool|Yes)P(High|Yes)P(True|Yes)=\frac{2}{9} \frac{3}{9} \frac{3}{9} \frac{3}{9} \frac{9}{14} = 0.0053$$

> $$P(Yes|Cool, High, True)∝P(Cool|Yes)P(High|Yes)P(True|Yes)$$ Missing values 가 있어도 Naive Bayes는 문제 없다.
{: .prompt-info }

- Laplace estimator (Laplace Correction)
  - 다른 weight도 적용시킬 수 있다.
$$\frac{4+\mu p_1}{8+\mu}, \frac{1+\mu p_2}{8+\mu}, \frac{3+\mu p_3}{8+\mu}$$

$$p_1+p_2+p_3 = 1$$