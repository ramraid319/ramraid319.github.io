---
title: Linear Regression
author: ramraid
date: 2024-02-24 20:30:00 +0800
categories: [Machine Learning]
tags: [writing]
toc: true
comments: true
math: true
mermaid: false
image:
    path: /assets/img/cat.png
    alt: 선형 회귀 :/
# render_with_liquid: false
pin: false
---

# Linear Regression

## Simple Linear Regression

X와 Y 사이의 linear relationship을 아래와 같이 나타낸다.

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

$\overline y \equiv \frac{1}{n}\sum_{i=1}^{n}y_i$ 와 $\overline x \equiv \frac{1}{n}\sum_{i=1}^{n}x_i$ 는 샘플의 mean이다.
{: .prompt-info }
결과적으로, 위 두 수식으로 simple linear regression 에서 최소제곱법으로 coefficient 를 추정할 수 있다.