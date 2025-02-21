---
title: "[PL] Language Design Issues"
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

- 프로그램 [ 수행 / 번역 / 작성 / 관리 ] 비용

## Programming Paradigm & Computation model

| 프로그래밍 패러다임 | 계산 모델                 |
| :------------------ | :------------------------ |
| 명령형 언어         | von Neumann Model         |
| 함수형 언어         | Recursive Function Model  |
| 논리 언어           | Deductive Reasoning Model |

패러다임과 계산 모델은 밀접하지만, 정확히 일대일 대응은 아니다.
{: .prompt-info }

객체지향 패러다임은 대부분 명령형 언어로 지원, 그러나 함수형 언어로 지원할 수도 있음

#### 명령형 언어 / Imperative, Procedural Languages

- 계산 모델
    - State Transition Machine
    - 입력은 초기 State, 상태 전이를 계속한 후, 최종 State에 출력이 있음.
- 특징
    - 상태 변경에 중심을 둔다.
~~~
s1; s2; s3;
~~~
- 예) FORTRAN, COBOL, C, Pascal 등

#### 함수형 언어 / Functional Languages, Applicatigve Languages

- 계산 모델
    - 입력 값과 출력 값은 연관성이 없음
    - 변수, 대입 연산이 없음
- 특징
    - 주로 함수를 작성, 합성한다.
~~~
P1(P2(P3(X)))
~~~
- 예) LISP, Scheme, ML, Haskell

#### 규칙기반 언어 / Rule-Based Languages, Logic Languages

- 계산 모델
    - 논리 규칙으로 추론
    - 명제의 조합을 입력 --> 명제 또는 명제의 일부를 출력
- 특징
    - 문제의 특성을 논리 규칙으로 설정
    - 순서를 중요시함
~~~
'Goal <-- Hypotheses>'
~~~
- 예) Prolog

#### 객체지향 언어 / Object-Oriented Languages

- 계산 모델
    - 주로 명령형 패러다임 언어에 구현됨
- 특징
    - Identity 를 갖는 객체들로 구성
    - 객체는 property, behavior를 가지고 있음
    - 객체 = 클래스의 실체 ( instance )
    - IS - A 관계 : 추상화간의 포함관계, Subclass
- 예) Smalltalk, C++, Java

#### 구조화 프로그래밍
_GOTO 논란과 함께 출현했다._

- 순차구조 / Sequence Structure
- 선택구조 / Selection Structure
- 반복구조 / Repetition Structure

하향식 설계 ( top-down design )
프라임 프로그램 ( prime program )