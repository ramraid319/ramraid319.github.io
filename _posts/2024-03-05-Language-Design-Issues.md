---
title: Language Design Issues
author: ramraid
date: 2024-03-05 20:00:00 +0800
categories: [Computer Science, Programming Language]
tags: [Programming Language]
math: false
# image:
#     path: /assets/img/cat.png
#     alt: 선형 회귀 :/
render_with_liquid: false
# pin: false
---

# Language Design Issues

## 프로그래밍 언어?

프로그래밍 언어는 사람과 기계의 의사소통, 기계를 제어할 수 있는 표현이다.

Writing 도 중요하지만, Reading 또한 중요하기 때문에, 가독성 (Readability) 가 중요하다.

### 프로그래밍 언어를 학습하는 목적

- 효과적인 알고리즘 개발
     - 언어에서 제공하는 여러 기능을 활용하여 알고리즘 개발
     - 잘못 사용하면 실행시간이 늘어나고, 리소스 낭비, 오류가 생길 수 있다.
- 더 적합한 언어 선택
- 새로운 언어를 쉽게 설계

### 프로그래밍 언어의 기준

- 문제 영역 (Problem Domain)
    - 사무응용, 과학계산, 시스템 프로그래밍, 웹, 인공지능 등
- 패러다임 (Programming Paradigm)
    - 절차언어, 함수형 언어, 모듈 기반 언어, 객체 지향 언어, Generic Programming, 선언적 언어
- 계산 모델 (Computational Model)
    - 명령형 언어 : 폰 노이만 컴퓨터 구조를 기반
    - 함수형 언어 : 순환 함수 이론을 기반
    - 논리 언어 : 수학적 논리를 기반

### 좋은 언어?
- 명료성, 간결성, 일관성이 있어야 배우기 쉽다.
- 직교성 (Orthogonality)
    - 여러 개의 기능들이 독립적이고, 임의로 조합할 수 있어야 한다.
    - 함수형 언어는 직교성을 지원한다.
    - 객체지향 언어는.. 언어에 따라 다르다.
- 자연스러운 응용 분야
    - 필요한 것을 바로 만들고 쓸 수 있어야 한다.
- 추상화 지원
- 프로그램 테스트의 용이성
- 프로그램 이식성
    - 지원하는 플랫폼이 다양한가?

### 프로그래밍 언어의 비용

- 프로그램 수행 비용
- 프로그램 번역 비용
- 프로그램 작성 비용
- 프로그램 관리 비용

## Programming Paradigm & Compute Model



| 프로그래밍 패러다임  | 계산 모델                    |
| :----------------- | :--------------------------- |
| 명령형 언어         | von Neumann Model            |
| 함수형 언어         | Recursive Function Model     |
| 논리 언어           | Deductive Reasoning Model    |

패러다임과 계산 모델은 밀접하지만, 정확히 일대일 대응은 아니다.
{: .prompt-info }

객체지향 패러다임은 대부분 명령형 언어로 지원, 그러나 함수형 언어로 지원할 수도 있음

### 명령형 언어 / Imperative, Procedural Languages

