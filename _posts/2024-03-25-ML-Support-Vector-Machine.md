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

![Hyperplane](/assets/img/posts/MachineLearning/ML-Support-Vector-Machine/ML-Support-Vector-Machine-01.png){: width="972" height="589" }
_Hyperplane_

$$\beta_0+\beta_1X_{i1}+\beta_2X_{i2}+...+\beta_pX_{ip}>0 y_i=1$$

$$\beta_0+\beta_1X_{i1}+\beta_2X_{i2}+...+\beta_pX_{ip}<0 y_i=-1$$

파란색 Class를 $y_i=1$, 빨간색 Class를 $y_i=-1$라고 Label 을 설정할 수 있다.

분리된 hyperplane은 모든 $i=1,...,n$ 에 대해, 아래 특성을 가진다.

$$y_i(\beta_0+\beta_1X_{i1}+\beta_2X_{i2}+...+\beta_px_{ip})>0$$

### The Maximal Margin Classifier

Classify Hyperplane은 무수히 많다. 따라서, Maximal Margin Classifier 을 이용해 가장 적절한 Hyperplane을 찾을 수 있다.

![MaximalMargin](/assets/img/posts/MachineLearning/ML-Support-Vector-Machine/ML-Support-Vector-Machine-02.png){: width="972" height="589" }

하지만 $p$-dimension 이 커지면, overfitting될 수 있다.

만약, $\beta_0, \beta_1, ... ,\beta_p$ 가 maximal margin hyperplane의 coefficients라고 하면, maximal margin classifier, $f(x^*)=\beta_0 + \beta_1x^*_1 + \beta_2x^*_2 +...+\beta_px^*_p$ 은 테스트 관측값 $x^*$를 분류한다.

#### Construction of Maximal Margin Classifier

*maximize*($\beta_0, \beta_1, \dots, \beta_p$) $M$ (margin의 넓이, M 을 최대화하는 $\beta$ 를 선택)

*subject to* $\sum^p_{j=1}\beta^2_j=1$

$y_i(\beta_0+\beta_1X_{i1}+\beta_2X_{i2}+...+\beta_px_{ip})>M$ for all $i=1,...,n$

#### The Non-separable Case

![MaximalMargin](/assets/img/posts/MachineLearning/ML-Support-Vector-Machine/ML-Support-Vector-Machine-03.png){: width="972" height="589" }

하지만, Maximal Margin Classifier 로 분류할 수 없는 경우도 있다.

![MaximalMargin](/assets/img/posts/MachineLearning/ML-Support-Vector-Machine/ML-Support-Vector-Machine-04.png){: width="972" height="589" }

또는, 한 개의 관측값이 Hyperplane 을 극단적으로 변화시킬 수 있다.

## Support Vector Classifier

Non-separable case를 해결하기 위해, Support Vector Classifier 혹은 Soft Margin Classifier 를 이용한다.

모든 관측값에 대해 Maximal 한 값을 찾는 대신, 어느정도의 관측값의 오차를 허용한다.

*maximize*($\beta_0, \beta_1, \dots, \beta_p, \epsilon_1, \dots, \epsilon_n $) $M$

*subject to* $\sum^p_{j=1}\beta^2_j=1$

$y_i(\beta_0+\beta_1X_{i1}+\beta_2X_{i2}+...+\beta_px_{ip})\geq M(1-\epsilon_i)$

$\epsilon_i\geq0, \sum^n_{i=1}\epsilon_i\leq C$

여기서 $C$는 non-negative tuning parameter 다.
$\epsilon$은 slack variable이라고 부르며, 각 관측값이 margin이나 hyperplane의 wrong side 에 있게 한다.

$\epsilon_i$은 margin과 hyperplane을 기반으로 $i$번째 관측값이 어디에 위치했는지를 나타낸다.

$\epsilon_i=0$이면, $i$번째 관측값은 margin의 correct side에 있는 것이고,

$\epsilon_i>0$이면, $i$번째 관측값은 margin에 violated (위배) 라고한다.

$\epsilon_i>1$이면, hyperplane의 wrong side에 있다고 말한다.

그러면 이제 tuning parameter $C$가 무엇인지 알 수 있는데, $C$는 $\epsilon_i$의 합을 제한하여 margin에 위배되는 수와 그 심각도를 결정한다.

만약 $C=0$ 이면, margin에 대한 위반을 제한한다.

$C>0$ 이면, $C$ 이상의 관측값은 hyperplane의 wrong side에 위치할 수 없다.

![SVClassifier](/assets/img/posts/MachineLearning/ML-Support-Vector-Machine/ML-Support-Vector-Machine-05.png){: width="972" height="589" }

서로 다른 *tuning parameter* $C$ 에 fitting된 Support Vector Classifier

#### Classification with Non-Linear Decision Boundaries

Support Vector Classifier의 경우, 두 개의 Class를 분류하는데 적절하지만, non-linear dicision boundaries는 다르다.

$$X_1, X_2, \dots X_p$$

기존에는 p개의 features를 이용해서 fitting 했다면,

$$X_1, X^2_1, X_2, X^2_2, \dots X_p, X^2_p$$

2p features를 이용해 support vector classifier를 fitting할 수 있다.

*maximize*($\beta_{0}, \beta_{11}, \beta_{12} \dots, \beta_{p2}, \epsilon_1, \dots, \epsilon_n $) $M$

*subject to* $y_i(\beta_0+\sum^p_{j=1}\beta_{j1}x_{ij}+\sum^p_{j=1}\beta_{j2}x^2_{ij})\geq M(1-\epsilon_i)$

$\sum^n_{i=1}\epsilon_i\leq C, \epsilon_i\geq0, \sum^p_{j=1}\sum^2_{k=1}\beta^2_{jk}=1$


#### Support Vector Machine

SVM은 SVC의 확장, 변수와 출력값 사이의 non-linearity를 표현하기 위해서 Kernel 을 활용하여 효율적으로 변수 공간을 확장한다.

> 고차원에서 데이터의 boundary를 정해서 저차원에 투영시키는 것
{: .prompt-info }

> Kernel function? $f(x_1, x_2)=\alpha$ 와 같이 두 개의 벡터로 커널을 만드는 것
{: .prompt-info }

$$f(x)=\beta_0+\sum^n_{i=1}\alpha_i<x, x_i>$$

Linear support vector classifier은 위와 같이 표현 가능하다.

*n parameters $\alpha_i$, $i=1,\dots,n$*
*one training observation $\beta_0$*

$\alpha_i$와 $\beta_0$를 추정하기 위해서 $\begin{pmatrix} n\2 \end{pmatrix}$ 개의 내적 $<x, x_i>$이 필요하다.

이를 generalization하면, $K(x_i, x_{i'})$ 으로 나타낼 수 있다.

$$K(x_i, x_{i'})=\sum^p_{j=1}x_{ij}x_{i'j}$$

이는 linear kernel 이고, Pearson Correlation을 사용하여 관측값 pair의 similarity를 수량화하는데 필요하다.

$$K(x_i, x_{i'})=(1+\sum^p_{j=1}x_{ij}x_{i'j})^d$$

이는 polynomial kernel of degree $d$ 이고, linear kernel을 대신해 더 유연한 decision boundary를 만들 수 있다.

$$K(x_i, x_{i'})=\beta_0 + \sum_{i\epsilon S}\alpha_iK(x,x_i)$$

위와 같이 non-linear kernel과 결합된 support vector classifier를 support vector machine이라고 한다.

![non-linear](/assets/img/posts/MachineLearning/ML-Support-Vector-Machine/ML-Support-Vector-Machine-06.png){: width="972" height="589" }

> Support Vector 은 margin에 걸쳐있는 것들이다.
{: .prompt-info }

$$K(x_i, x_{i'})=\exp(-\gamma\sum^p_{j=1}(x_{ij}-x_{i'j})^2)$$

polynomial kernel 은 boundary가 tight하지 않다.. 멀리 있는 것들에는 영향이 크지 않다. 그래서 위와 같은 radial kernel을 이용하기도 한다.

> redial kernel 는 exponential 하기 때문에, local sensitive 하다.
{: .prompt-info }

> $\gamma$ 가 커지면 local sensitive 정도도 커진다.
{: .prompt-info }

SVM은 결국 margin을 최대화하기 위해 데이터를 분리하는 모델이다.

# TODO : LAB 추가