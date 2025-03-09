---
title: "[Comp] Formal Language and Grammar"
author: ramraid
date: 2024-10-20 20:00:00 +0800
categories: [Computer Science, Compiler]
tags: [Compiler]
toc: true
comments: true
math: true
mermaid: false
pin: false
image:
    path: ../assets/img/posts/Compiler/Chomsky-Hierarchy.png
    alt: Chomsky-Hierarchy
---

#### Syntax and Semantics

**Language Definition**: 프로그래밍 언어는 Syntax, Semantics 두 측면에서 정의될 수 있다.

- **Syntax**는 어떤 것이 올바른 형태인지를 정의, 주로 Formal Language로 설명된다.
- **Semantics**는 프로그램이 어떤 행동을 실행할지 설명, 주로 Natural Language로 설명된다.

### Formal Language

**알파벳은 Symbol이다.**

**문자열**은 알파벳의 나열이다.

**Formal Language**는 문자열의 집합이다.

**Grammar**는 Language를 표현할 수 있다.

예를 들어,
  - Alphabet:   $\sum = \braket{0, 1}$
  - String:     $101 \in \sum^*$
  - Language:   $L = \braket{1, 11, 101, 111}$

#### BNF and EBNF

**BNF**

- BNF는 Context-Free Grammar에 대한 표기법
- 구문 클래스를 정의하는 규칙의 집합

```text
<expression> ::= <number> + <number>
               | <number> - <number>
               ;
<number>     ::= "0" | "1"
               ;
```

이러한 규칙을 생성 규칙이라고 한다.

**EBNF**

```text
<program> ::= { F | L | R };
```

Extended BNF, 선택과 반복에 관한 메타 심볼들을 더 추가했다.

그러나 표현력은 BNF와 같다 ($L(E) = L(B)$)

- 대괄호는 Optional 기호
- Bar 기호는 선택 기호
- 중괄호는 반복 기호
- 이중 화살표로 **파생**(규칙의 적용)을 표시

$\alpha \rArr^* \beta$ : $\alpha$ 가 0개 이상의 단계를 거쳐 $\beta $를 유도

$\alpha \rArr^+ \beta$ : $\alpha$ 가 1개 이상의 단계를 거쳐 $\beta $를 유도

파생이 끝나면 일련의 상수를 얻을 수 있다.

#### Grammar

**Formal Grammar**: Grammar는 언어를 만들기 위한 규칙의 집합

- Unrestricted Grammars (Type 0)
- Context-Sensitive Grammars (Type 1)
- Context-Free Grammars (Type 2)
- Regular Grammars (Type 3)

![Chomsky-Hierarchy](../assets/img/posts/Compiler/Chomsky-Hierarchy.png)

#### Context-Free Grammar

Grammar를 $G = (N, T, P, S)$ 로 표현
- $N$: nonterminals의 집합
- $T$: terminals의 집합
- $P$: Production Rules의 집합
- $S$: 시작 기호로 지정된 nonterminal

$$L(G) = \{ w| S \rArr^+ w\}$$

문맥 자유 문법은, 모든 생성 규칙이 nontermianl $A$와 grammar symbol string $x$에 대해 $A \rarr x$ 의 형태를 가짐

프로그래밍 언어의 구문을 정의할 때, 일반적으로 문맥 자유 문법을 사용한다.
