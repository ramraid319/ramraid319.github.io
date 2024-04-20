---
title: "[PL] Modeling Language Properties"
author: ramraid
date: 2024-03-21 20:00:00 +0800
categories: [Computer Science, Programming Language]
tags: [Programming Language]
math: false
render_with_liquid: false
# pin: false
---

## Formal Languages

#### Chomsky Hierarchy

문법의 분류와 각 문법이 생성하는 언어를 인식하기 위한 오토마타

Type 3 : 정규 문법 (Regular Grammar) // Finite Automata
Type 2 : 문맥 자유 문법 (Context Free Grammar) // nondeterministic PDA
Type 1 : 문맥 민감 문법 (Context Sensitive Grammar) // Linear Bounded Automata
Type 0 : 무제한 문법 (Unrestricted Grammar) // Turing Machine

#### Regular Grammar

Id → aX | ... | zX | a | ... | z
X → aX | ... | zX | 0X | ... | 9X | a | ... | z | 0 | ... | 9

좌변 : nonterminal 한 개
우변 : 정해진 한쪽 끝에만 nonterminal이 한 개 올 수 있음

#### Context Free Grammar

E → E + T | T
T → T * F | F
F → n | ( E )

좌변 : nonterminal 한 개
우변 : 제한 없음

#### Context Sensitive Grammar

S → abc | aSBc
cB → Bc
bB → bb

L(G) = {a^nb^nc^n | n >= 1}

좌변의 길이가 우변의 길이보다 크면 안됨 → ε는 생성할 수 없음

#### Unrestricted Grammar

S → ACaB
Ca → aaC
CB → DB
CB → E
aD → Da
AD → AC
aE → Ea
AE → ε

L(G) = {a^n | n = 2^m, m >= 1}

제한 없음

## Turing Machine and Decidability

Turing Machine
- 읽고 쓸 수 있는 무한 길이의 테이프와 유한 제어로 구성된 유효 절차 모델
- 인간의 계산을 흉내
- Memory : 무한 배열

Decidability
- Undecidable Problem : Turing Machine으로 일반 해를 찾을 수 없는 문제

## Language Semantics

Grammatical Model
속성문법 : 문법의 각 기호에 속성을 부여하고 속성 값을 구하는 것으로 의미 표현

Operational Model
기능적 의미론 : 가상 기계 상에서 프로그램의 동작을 보임

Applicative Model 
표기적 의미론 : 각 프로그램이 나타내는 함수가 해당 프로그램의 의미라고 파악

Axiomatic Model
공리적 의미론 : 프로그램 수행 전과 수행 후의 술어 변화가 프로그램 명세와 일치하는지 증명

Specification Model
어떤 데이터에 대한 여러 함수의 관계를 정립하고, 구현 내용이 동일함을 입증

#### Attribute Grammar 속성 문법

Attribute Grammar = Grammar + Evaluation Rules
- 문법 기호 (teminal, nonterminal) 에 속성을 부여
- 속성을 구하는 규칙을 문법과 함께 제시

#### Operational Semantics 기능적 의미론

실제 컴퓨터와 유사한 가상기계의 동작을 통해 프로그램 의미를 표현

#### Denotational Semantics 표시적 의미론

Applicative Model
프로그램의 의미를 함수로 파악 → 람다 표기 : 함수 표현에 유리함

#### Axiomatic Semantics 공리적 의미론

프로그램 요소에 대한 precondition과 postcondition을 통해 프로그램의 의미 파악

{P}program{Q}
P : 프로그램 수행 전의 조건 (assertion) / input specification
Q : 프로그램 수행 후의 조건 / output specification

## Axiomatic System

Theorems 를 유도할 수 있는 임의의 공리 집합

#### The Weakest Precondition

wp(P, Q) : 프로그램 P를 수행한 후 Q 조건을 만족하기 위한 weakest precondition

weakest precondition이 프로그램 input spec. 으로부터 추론되고, 사후조건이 원하는 output spec. 이라면, Correct Program