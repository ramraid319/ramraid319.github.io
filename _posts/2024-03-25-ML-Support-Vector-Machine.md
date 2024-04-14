---
title: "[ML] Support Vector Machine"
author: ramraid
date: 2024-03-25 20:00:00 +0800
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

> !주의! 게으름 피우느라 아직 볼 가치가 없는 글입니다.
{: .prompt-danger }

# Support Vector Machine (SVM)

## Hyperplane

$p$-dimensional 공간에서 hyperplane (초평면)은 $p-1$ dimension의 flat affine 부분공간이다.

Hyperplane의 수학적 정의는 아래와 같다.
$$\beta_0+\beta_1X_1+\beta_2X_2+...+\beta_pX_p=0$$

> 예를 들어, 2-dimensional hyperplane은 $\beta_0+\beta_1X_1+\beta_2X_2=0$ 이다.
{: .prompt-info}

$$\beta_0+\beta_1X_1+\beta_2X_2+...+\beta_pX_p>0$$

$$\beta_0+\beta_1X_1+\beta_2X_2+...+\beta_pX_p<0$$

위와 같이 Hyperplane을 기준으로 공간을 two halves로 나누는 것이 가능하다.

#### Classification Using a Separating Hyperplane

이 Hyperplane을 이용해서 Classification을 할 수 있다.

$p$-dimensional 공간에서 $n$ 개의 훈련 관측값으로 구성된 $n$ x $p$ 행렬 X

$$x_1=\begin{bmatrix}x_{11}\\
...\\
x_{1p}\end{bmatrix}, ..., x_n=\begin{bmatrix}x_{n1}\\
...\\
x_{np}\end{bmatrix}$$

![Hyperplane](assets\img\posts\MachineLearning\ML-Support-Vector-Machine\ML-Support-Vector-Machine-01.png){: width="972" height="589" }
_Hyperplane_

$$\beta_0+\beta_1X_{i1}+\beta_2X_{i2}+...+\beta_pX_{ip}>0 y_i=1$$

$$\beta_0+\beta_1X_{i1}+\beta_2X_{i2}+...+\beta_pX_{ip}<0 y_i=-1$$

파란색 Class를 $y_i=1$, 빨간색 Class를 $y_i=-1$라고 Label 을 설정할 수 있다.

분리된 hyperplane은 모든 $i=1,...,n$ 에 대해, 아래 특성을 가진다.

$$y_i(\beta_0+\beta_1X_{i1}+\beta_2X_{i2}+...+\beta_px_{ip})>0$$

### The Maximal Margin Classifier

Classify Hyperplane은 무수히 많다. 따라서, Maximal Margin Classifier 을 이용해 가장 적절한 Hyperplane을 찾을 수 있다.

![MaximalMargin](assets\img\posts\MachineLearning\ML-Support-Vector-Machine\ML-Support-Vector-Machine-02.png){: width="972" height="589" }

하지만 $p$-dimension 이 커지면, overfitting될 수 있다.

만약, $\beta_0, \beta_1, ... ,\beta_p$ 가 maximal margin hyperplane의 coefficients라고 하면, maximal margin classifier, $f(x^*)=\beta_0 + \beta_1x^*_1 + \beta_2x^*_2 +...+\beta_px^*_p$ 은 테스트 관측값 $x^*$를 분류한다.

#### Construction of Maximal Margin Classifier

*maximize* $M$
*subject to* $\sum^p_{j=1}\beta^2_j=1$
$y_i(\beta_0+\beta_1X_{i1}+\beta_2X_{i2}+...+\beta_px_{ip})>M$ for all $i=1,...,n$

#### The Non-separable Case

![MaximalMargin](assets\img\posts\MachineLearning\ML-Support-Vector-Machine\ML-Support-Vector-Machine-03.png){: width="972" height="589" }

하지만, Maximal Margin Classifier 로 분류할 수 없는 경우도 있다.

![MaximalMargin](assets\img\posts\MachineLearning\ML-Support-Vector-Machine\ML-Support-Vector-Machine-04.png){: width="972" height="589" }

또는, 한 개의 관측값이 Hyperplane 을 극단적으로 변화시킬 수 있다.

## Support Vector Classifier



## Support Vector Machine

### Classification with Non-Linear Decision Boundaries

#### Support Vector Machine

만약 3차원이라면 $X_1^3, X_2^3, ... $ 로 더 늘어날 것.
$\sum_{}^{}\sum{}^{} \beta_(jk)^2=1$ 로 제한한 이유는 꼼수 방지.

Kernal function?
- $f(x_1, x_2)=\alpha$ 와 같이 두 개의 벡터로 커널을 만드는 것

> 고차원에서 데이터의 boundary를 정해서 저차원에 투영시키는 것
{: .prompt-info }

polynomial kernel 은 boundary가 tight하지 않다.. 멀리 있는 것들에는 영향이 크지 않다.

redial kernel 과 같은 경우는 exponential 이기 때문에, local sensitive 하다.

$\gamma$ 가 커지면 local sensitive 정도도 커짐
{: .prompt-info }

SVM은 결국 margin을 최대화하기 위해 데이터를 분리하는 모델이다.

Support Vector 은 margin에 걸쳐있는 것들이다.
{: .prompt-info }


## TODO

- [ ] Support Vector Machine
    - [ ] Hyperplane
    - [ ] The Maximal Margin Classifier
    - [ ] Support Vector Classifier
    - [ ] Support Vector Machine