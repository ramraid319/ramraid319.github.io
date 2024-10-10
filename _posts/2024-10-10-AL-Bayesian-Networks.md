---
title: "[AL] Bayesian Networks"
author: ramraid
date: 2024-10-10 20:00:00 +0800
categories: [Computer Science, Algorithm, Bayesian Networks]
tags: [Algorithm, Byaesian Networks]
toc: true
comments: true
math: true
mermaid: false
pin: false
---

# Bayesian Networks

## Syntax of Bayesian Networks

## Semantics of Bayesian Networks

"Numberical" Semantics의 의미는 모든 로컬 조건 분산 product한 것을 말한다.
(full joint distribution, 완전 결합 확률 분포)

$$P(x_1, ..., x_n) = \prod^n_{i=1} P(x_i|Parents(X_i))$$

이 full joint distribution은 chain rule과 conditional independenc에 의해

### Constructing Bayesian Networks

$$\bold{P}(X_1, ..., X_n) = \prod^n_{i=1} \bold{P}(X_i | X_1, ..., X_{i-1})$$ $$= \prod^n_{i=1} \bold{P}(X_i | Parents(X_i))$$

Cahin Rule과 Contruction을 적용하면 위와 같다.

### Conditional Independence Relations in Bayesian Networks

#### 위상적인 의미 (Topological semantics)

각 노드에 대해, 자손이 아닌 노드 (Non-descendants)가 주는 영향은 조건부 독립이다.

$$P(X|Parents(X)) = P(X|Parents(X), ND(X))$$

## Compact Conditional Distributions
