---
title: "[ML] Logistic Regression"
author: ramraid
date: 2024-03-18 20:00:00 +0800
categories: [Computer Science, Machine Learning]
tags: [Machine Learning, Linear Algebra]
math: true
# image:
#     path: /assets/img/cat.png
#     alt: 선형 회귀 :/
render_with_liquid: false
# pin: false
---

#### Classification

특정 상황에서 Y가 Categorical한 경우가 많다.
각 데이터가 어떤 클래스에 속하는지 판별하는 것이 목적

Class Lable 은 순서가 없고, 이산형 변수. 즉, Classification은 Category를 예측, Regression은 Continuous Value를 예를한다.

# Logistic Regression

선형 Binary Classification 문제를 위한 로지스틱 회귀 (사실상 Classification Model)

- Odds Ratio : $\frac{P}{(1-P)}$
- Logit Function (Log-odds) : $logit(P)=\ln\frac{P}{(1-P)}$

> Logit Function은 0과 1 사이의 입력 값을 실수 범위 출력 값으로 변환
{: .prompt-info}

다양한 특성을 기반으로 Class Lable을 추정하는 것이 목표, 아래와 같이 관계 설정 가능

$$logit(P(y=1|x))=w_0x_0+w_1x_1+...+w_mx_m=\sum^m_{i=0}w_ix_i=w^Tx$$

> 추정하고자 하는 것 : 어떤 샘플이 특정 클래스에 속할 확률
{: .prompt-info}

$$\phi(z)=\frac{1}{1+e^{-z}}$$

> $\phi(z)$는 Sigmoid Function, 범위가 [0, 1] 이므로 특정 샘플이 해당 클래스에 속할 확률이 된다.
{: .prompt-info}

Threshold Function을 통해 Classification 결과로 변환

- 가능도 (우도, Likelihood)
$$L(w)=P(y|x;w)=\prod^n_{i=1}P(y^{(i)}|x^{(i)};w)=\prod^n_{i=1}(\phi(z^{(i)}))^{y^{(i)}}(1-\phi(z^{(i)}))^{1-y^{(i)}}$$

- 로그 가능도 (Log-likelihood)
$$l(w)=\log{L(w)}=\sum^n_{i=1}[y^{(i)}\log{(\phi(z^{(i)}))+(1-y^{(i)})\log{(1-\phi(z^{(i)}))}}]$$

    - Likelihood가 작을 때 일어날 수 있는 Underflow 방지
    - 곱을 합으로 바꾸어 Gradient 계산이 용이

#### Logistic Model

$$p(X) = \frac{e^{\beta_0 + \beta_1X}}{1+e^{\beta_0 + \beta_1X}}$$

기존 Linear Model 을 사용하면, large balance 에 대해, 값이 1보다 커질 수 있다. 이 문제를 해결하기 위해서, 위와 같은 모델을 이용해, output이 0에서 1 사이의 값이 나오도록 한다. (maximum likelihood)

위 식을 이용하여 아래 식을 유도할 수 있다.

$$\log{\frac{p(X)}{1-p(X)}}=\beta_0+\beta_1X$$

좌항은 log odds 또는 logit 이라고 부른다. Logistic Regression Model은 X에 대해 Linear한 logit을 가진다.

####  Estimating the Regression Coefficients

Logistic Regression의 Coefficients Estimation은 maximum likelihood method를 이용한다.

likelihood function

$$l(\beta_0, \beta_1)=\prod_{i:y_i=1}p(x_i)\prod_{i':y_{i'}=0}(1-p(x_{i'}))$$

#### Multinomial Logistic Regression

$$\log{\frac{Pr(Y=k|X=x)}{Pr(Y=K|X=x)}}=\beta_{k0}+\beta_{k1}x_1+ ... +\beta_{kp}x_p$$

$$Pr(Y=k|X=x)=\frac{e^{\beta_{k0}+\beta_{k1}x_1+ ... +\beta_{kp}x_p}}{\sum^{K}_{l=1}e^{\beta_{l0}+\beta_{l1}x_1+ ... +\beta_{lp}x_p}}$$

$$\log{\frac{Pr(Y=k|X=x)}{Pr(Y=K|X=x)}}=(\beta_{k0}-\beta_{k'0})+(\beta_{k1}x_1-\beta_{k'1})x_1+ ... +(\beta_{kp}x_p-\beta_{k'p})x_p$$