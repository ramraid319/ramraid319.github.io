---
title: "[ML] Introduction"
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

### 인공지능?

#### 강 인공지능 vs 약 인공지능

- 강 인공지능
    - 다양한 분야에서 활용
    - 알고리즘을 설계하면, AI가 스스로 데이터를 찾아 학습
    - 정해진 규칙을 벗어나 능동적으로 학습해 창조 가능
- 약 인공지능
    - 특정 분야에서만 활용
    - 알고리즘 + 기초 데이터, 규칙을 입력해야 함
    - 이를 바탕으로 학습 가능, 규칙을 벗어난 창조는 불가

#### 머신러닝 vs 딥러닝

- 머신러닝
    - 특징을 인간이 정의하여 사용
- 딥러닝
    - 특징을 스스로 추출할 수 있는 능력 학습

### 데이터

#### 벤치마크 데이터셋?

- 벤치마크 데이터셋은 공통된 기준으로 인공지능 정확도를 평가하고 경쟁할 수 있는 기반, 인공지능 발전의 핵심
- 자연어 이해, 이미지 분류, 얼굴인식 등 다양한 종류의 글로벌 벤치마크 존재

#### 문제점

- 데이터 편향 문제
- 개인정보
- AI 어뷰징
- Data Scarcity Problem
    - 재난상황 등을 학습할 때, 소수의 데이터셋으로 학습 가능한 AI 필요
    - Domain Adaption : 사용 가능한 도메인 (게임 등) 에서 기반 지식 학습 -> 목표 도메인의 지식 학습에 이용
    - Transfer Learning : 다른 Task를 위해 만들어진 모델을 새로운 Task에 적용
    - Meta Learning : 다양한 Task에서 잘 동작하는 Parameter 학습하여 소수의 특정 Task 데이터셋 만으로도 빠르게 학습
- Data Security
    - Adversarial Attack : 입력 데이터를 공격하여 AI의 판단 결과에 영향 -> 사람이 인지할 수 없는 미세한 Perturbation 주입

## Machine Learning

- Machine Learning Pipeline
    - Preprocessing : Feature Extraction + Scaling, Feature Selection, Dimensionality Reduction, Sampling
    - Learning : Model Selection,  Cross-Validation, Performance Metrics, Hyper-parameter Optimization
    - Evaluation
    - Prediction

#### Supervised Learning

- Labeled Data
- Direct Feedback
- Predict Outcome / Future

#### Unsupervised Learning

- No Labels
- No Feedback
- Find Hidden Structure in Data

#### Reinforcement Learning

- Decision Preocess
- Reward System
- Learn Series of Actions