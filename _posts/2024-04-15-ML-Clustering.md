---
title: "[ML] Clustering"
author: ramraid
date: 2024-04-15 20:00:00 +0800
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

# Clustering

## Instance-Based Learning

- Parametric model
  - 데이터를 나타내는 고정된 크기의 파라미터 집합
  - ex. linear regression

- Nonparametric model
  - 데이터가 파라미터로 나타내기 어려운 데이터 (non-linear data)
  - 데이터 자체로 모델을 만든다.
  - ex. instance-based learning
  
- 주어진 query $x_q$, 에 대해, nearest neighbors $NN(k, x_q)$ 의 $k$를 찾는 것.
  - Classification : 가장 가까운 이웃 $NN(k, x_q)$ 값들에 기반하여 분류한다. (평균값 등)
  - Regression : 주어진 query에 대해서 한번 더 regression을 해서 query에 대한 답을 얻음

#### Curse of Dimensionality

2-dimension 에서는 실제로 nearest neighbor을 볼 수 있다.
하지만, 고차원 데이터에서는 어떻게 보이는가?

~~nearest neghbors가 사실은 그렇지 않다.~~

$k$ : neighbor의 수
$l$ : neighbor끼리의 평균 길이
$l^n$ : neighbor간 hypercube의 volume

$$\frac{l^n}{1^n}=l^n=\frac{k}{N}\to l=(\frac{k}{N})^\frac{1}{n}$$

#### Distance Functions

- 거리 측정
    - Minkowski distance ($L^p$ norm)

- Normalization

$$x_{j,i}\to \frac{(x_{j,i}-\mu_i)}{\sigma_i}$$

#### Finding Nearest Neighbors Efficiently

- $kD$-tree
  - $k$-Dimension의 데이터를 가지는 balnaced binary tree
  - 

## Clustering

- Unsupervised Learning
  - 예측할 수는 없다. 하지만 instance들을 여러 그룹으로 분리시킬 수 있다.

- Expressing the result of clustering
  - Disjoint 나 Overlapping으로 표현
  - Deterministic 이나 Probabilistic
  - Hierachical 이나 Flat
  
- K-means algorithm
- Hierarchical clustering
- Statistical clustering

#### K-means algorithm

- 각 클러스터에 값의 평균값을 기준으로 클러스터링을 반복
- initial center은 random하기 때문에 실행할 때마다 달라질 수 있는 문제점