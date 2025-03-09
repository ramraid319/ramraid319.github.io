---
title: "[Comp] Compiler"
author: ramraid
date: 2024-10-19 20:00:00 +0800
categories: [Computer Science, Compiler]
tags: [Compiler]
toc: true
comments: true
math: true
mermaid: false
pin: false
---

## Compiler

**Compiler**: 프로그래밍 언어로 쓰여진 코드를 다른 프로그래밍 언어로 변환(Transformation)시키는 프로그램

#### Program vs Process

**Program**: 컴퓨터에서 실행 가능한 Static한 파일

**Process**: 컴퓨터에서 실행중인 Dynamic한 프로그램

#### Programming Language

**Syntax**: 어떤 형식으로 코드를 작성해야 하는지 정의

**Semantics**: 코드가 어떤 의미를 가지는지, 어떤 동작 방식을 가지는지 정의

**Programming Language**: 문법적 규칙과 의미론적 규칙의 집합

### Compiler and Interpreter

#### Compilation

Source Language로 쓰여진 프로그램을 의미적으로 같은 Target Language로 변환하는 과정

**Analysis Phase**: 소스코드를 읽고, 정보를 수집, **FRONTEND (machine independent)**
  - **Scanner - 어휘 분석(Lexical Analysis)**: 문자열을 토큰화 시킨다
  - **Parser - 구문 분석(Syntax Analysis)**: 토큰열(Token String)을 구문 트리(Parse Tree)로 작성한다.
  - **의미 분석(Semantic Analysis)**: 의미있는 Annotated Parse Tree를 작성한다. (e.g. 2 $ \rarr $ i2f(2))
  - **중간 코드 생성(Intermediate Code Generator)**: 중간 코드는 전단부(Frontend)와 후단부(Backend)을 연결해주며, 인터프리터의 경우 중간 코드를 가상 머신에서 실행할 수 있다.
  
**Synthesis Phase**: 수집한 정보를 바탕으로 목적코드(Target Code)를 작성 **BACKEND(machine dependent)**
  - 중간 코드 최적화
  - 어셈블리 코드 생성 및 최적화
  - 기계어 코드 생성 및 최적화

> 에디터나 텍스트 포맷터, LaTex 등에서 Analysis-Synthesis 모델을 사용한다.
{: .prompt-info}

#### Compiler Pass

- **Phase**: 프로그램 변환의 단계들
- **Pass**: 코드 전체를 스캔하는 것
- 소스코드는 여러 형태를 띌 수 있다. (e.g. text, graph..)
- Phase 수집은 한 번 **(Single pass)** 혹은, 여러 번 **(Multi pass)** 에 걸쳐서 될 수 있다.
- **Single Pass** compiler: 소스에 필요한 모든 것은 사전에 정의되어 있어야한다.
- **Multi Pass** compiler: 전체 프로그램 표현들을 메모리에 보관해야할 수 있다.


#### Interpretation

  - 소스 프로그램에서 암시된 작업을 수행
  - 소스와 입력을 동시에 받아 출력을 생성
  - **소스를 입력받고 실행까지 한다! (컴파일러는 생성만)**

#### The Hybrid

  - 바이트 코드로 변환을 수행하면서 가상 머신에서 Interpretation도 수행
  - 컴파일러와 인터프리터가 동시에 있는 구조


#### Example 0

$$1 + 2 * 3$$

**Operands and Operators**
연산자는 $+$, $*$ 두 개
피연산자는 $2$, $3$, $6$, $1$ 네 개

**Tree**
(Add 1 (MUL 2 3))

> Generalized Linked List로 트리를 나타낼 수 있다.
{: .prompt-info}

**Code**
PUSH 1;PUSH 2;PUSH 3; MUL; ADD

#### Example 1

$$0 ? 1 : 3 ? 4 : 5$$

**Operands and Operators**
연산자는 삼항연산자 $?:$ 두 개
피연산자는 $3$, $4$, $5$, $(3?4:5)$, $0$, $1$ 6개

하지만 삼항 연산자의 연산 순서에 모호성이 있다.


#### Compiler Tools

**Mathmatical tools**: 문법이나 추상 구문에 이용

**Software Development tools**
  - Scanner generators
  - Parser generators
  - Syntax-directed translation engines
  - Automatic code generators
  - Data-flow engines

**Lex & Yacc**
  - **Lex**는 Scanner **Yacc**은 Parser를 위한 도구
