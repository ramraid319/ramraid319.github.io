---
title: "[ML] Linear Regression"
author: ramraid
date: 2024-03-11 20:00:00 +0800
categories: [Computer Science, Machine Learning]
tags: [Machine Learning, Linear Algebra]
math: true
# image:
#     path: /assets/img/cat.png
#     alt: 선형 회귀 :/
render_with_liquid: false
# pin: false
---

# Linear Regression

## Simple Linear Regression

X와 Y 사이의 **Linear Relationship**을 아래와 같이 나타낸다.

$$ Y \approx  \beta_0 + \beta_1X $$

$ \beta_0 $ 과 $ \beta_1 $ 은 각각 intercept 와 slope 를 나타내는 상수이다. coefficients 또는 parameters 라고 부른다.

$$ \hat y = \hat\beta_0 + \hat\beta_1x $$

위 수식처럼 나타내기도 하는데, $\hat y$ 는 $Y$는 $X=x$일 때의 예측값을 나타낸다. $\hat \space$ 는 unknown parameter 또는 coefficient 를 표현할 때 사용한다.

## Estimating the Coefficients

우리의 목적은 결국 $n$ 개의 데이터로부터 가장 가까운 직선의 intercept $\hat \beta_0$ 와, slope $\hat \beta_1$ 을 찾는 것이다.

$$let, e_i = y_i-\hat y_i$$

$$RSS = e_1^2 + e_2^2 + ... + e_n^2$$

$e_i$ 는 $residual$,  실제 값과 예측값의 차이를 나타내고, $RSS$ 는 Residual Sum of Squares 로, 모든 $residual$ 의 제곱의 합이다.

$$RSS = (y_1 - \hat \beta_0 - \hat \beta_1x_1)^2 + (y_2 - \hat \beta_0 - \hat \beta_1x_2)^2 + ... + (y_n - \hat \beta_0 - \hat \beta_1x_n)^2 $$

최소제곱법으로 $RSS$ 를 최소화하는 $\hat\beta_0$ 과 $\hat\beta_1$ 을 구한다.

$$\hat\beta_0 = \frac{\sum_{i=1}^{n}(x_i-\overline x)(y_i-\overline y)}{\sum_{i=1}^{n}(x_i-\overline x)^2}$$

$$\hat\beta_1 = \overline y - \hat\beta_1 \overline x$$

> $\overline y \equiv \frac{1}{n}\sum_{i=1}^{n}y_i$ 와 $\overline x \equiv \frac{1}{n}\sum_{i=1}^{n}x_i$ 는 샘플의 mean이다.
{: .prompt-info }

결과적으로, 위 두 수식으로 simple linear regression 에서 최소제곱법으로 coefficient 를 추정할 수 있다.

## Multiple Linear Regression

단순 Linear Regression을 여러 개의 특성이 있는 데이터셋의 경우 Multiple Linear Regression 으로 확장 가능하다.
여러 개의 특성 $x_i$와 연속적인 목표 변수 $y$ 사이의 관계를 모델링하면 아래와 같다.

$$y=w_0x_0 + w_1x_1 + ... + w_mx_m=\sum_{i=0}^{m}w_ix_i=w^Tx$$

편의상 $x_0=1$로 간주하여 벡터 형태로 표현한다.

2차원의 경우 $w$는 평면을 나타내고, 3차원 이상인 경우 $w$는 **Hyperplane (초평면)** 을 나타낸다.

Regression은 차원에 관계없이 동일한 방법을 이용한다.

![Hyperplane](/assets/img/posts/MachineLearning/ML-Linear-Regression/ML-Linear-Regression-01.png){: width="972" height="589" }
_Hyperplane_

## TODO

- [ ] Linear Regression
    - [x] Simple Linear Regression
    - [x] Estimating the Coefficients
    - [ ] Multiple Linear Regression
    - [ ] Correlation Analysis
    - [ ] Ordinary Leat Squares
    - [ ] Model Evaluation 