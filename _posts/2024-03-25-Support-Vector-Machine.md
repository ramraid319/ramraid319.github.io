---
title: Support Vector Machine
author: ramraid
date: 2024-03-25 20:00:00 +0800
categories: [Machine Learning]
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

#### Classification Using a Separating Hyperplane

### The Maximal Margin Classifier

#### Construction of Maximal Margin Classifier

#### The Non-separable Case

## Support Vector Classifier

## Support Vector Machine

### Classification with Non-Linear Decision Boundaries

#### Support Vector Machine

만약 3차원이라면 $X_1^3, X_2^3, ... $ 로 더 늘어날 것.
$\sum_{}^{}\sum{}^{} \beta_(jk)^2=1$ 로 제한한 이유는 꼼수 방지.

Kernal function?
- $f(x_1, x_2)=\alpha$ 와 같이 두 개의 벡터로 커널을 만드는 것

고차원에서 데이터의 boundary를 정해서 저차원에 투영시키는 것
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