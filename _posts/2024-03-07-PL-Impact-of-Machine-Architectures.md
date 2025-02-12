---
title: "[PL] Impact of Machine Architectures"
author: ramraid
date: 2024-03-07 20:00:00 +0800
categories: [Computer Science, Programming Language]
tags: [Programming Language]
math: false
# image:
#     path: /assets/img/cat.png
#     alt: 선형 회귀 :/
render_with_liquid: false
# pin: false
---

# Impact of Machine Architectures

## Computer

Computer : 프로그램을 저장하고 실행할 수 있는 알고리즘과 데이터 구조의 집합

Actual Computer : : 물리적 장치들로 구성된 컴퓨터

Software-Simulated Computer : 다른 컴퓨터 상에서 작동하는 소프트웨어로 구성된 컴퓨터

#### Computer Hardware

![ComputerHardware](/assets/img/posts/ProgrammingLanguage/PL-Impact-of-Machine-Architectures/PL-Impact-of-Machine-Architectures-01.png){: width="454" height="490" }

구성 요소
- Data
- Primitive Operations
- Sequence Control
- Data Access
- Storage Management
- Operating Environment

#### Machine Cycle

![ComputerHardware](/assets/img/posts/ProgrammingLanguage/PL-Impact-of-Machine-Architectures/PL-Impact-of-Machine-Architectures-02.png){: width="454" height="490" }

Fetch -> Decode instruction -> Fetch operands -> Branch to designated operation

## Language and Virtual Machine

#### Firmware Computers

- 이론적 기반
  - 정확하게 정의된 알고리즘이나 데이터 구조는 하드웨어에서 구현 가능

- Firmware 컴퓨터의 형태 : 하드웨어와 이를 제어하기 위한 마이크로 프로그램

> Firmware : 하드웨어에 저장된 마이크로 프로그램
> Emulation : 소프트웨어적으로 마이크로 프로그램 수행을 흉내
{: .prompt-info }

#### Virtual Architecture

- Language Machine
  - 이론적으로 특정 언어를 하드웨어나 펌웨어 형태로 지원하는 것이 가능 (Language Proccessor)
  - ex. LISP machine, BASIC machine
  - but, 고비용.. -> General Purpose Processor + 언어 처리기 (SW)

- 고급 언어의 구현 방법
  - 번역 (translation)
  - 소프트웨어를 통한 시뮬레이션 (interpreter)

#### 언어 구현 구조

![ComputerHardware](/assets/img/posts/ProgrammingLanguage/PL-Impact-of-Machine-Architectures/PL-Impact-of-Machine-Architectures-03.png){: width="858" height="381" }

#### 가상기계

구현된 프로그래밍 언어는 그 자체로 가상기계로 볼 수 있다.

- Java 언어 기계
- Java 바이트코드 기계 (JVM)
- 실제 하드웨어

#### 언어 구현의 차이

1. 가상 기계에 대한 오해 : 구현할 언어의 정확한 정의
2. 구현 플랫폼의 차이 : 하드웨어 플랫폼이 다를 경우, 지원 기능의 차이로 언어 구현이 달라질 수 있다.
3. 구현 방법의 차이

## Binding

프로그램 구성요소와 속성의 묶음

#### Binding Time

바인딩이 일어나는 시점

```C
static int X;
scanf("%d", &X);
X = X + 10;
```

1. 언어 정의 시점 / 변수의 가능한 타입, +의 일반적 의미, 숫자 10의 의미
2. 언어 구현 시점 / 숫자 10의 내부 표현 형태
3. 프로그램 번역 시점 / 변수의 타입, 위 +의 의미
4. 링크 시점 / scanf() 호출 시 수행될 내용
5. 로드 시점 / 변수 X의 주소
6. 프로그램 수행 시점 (Dynamic Binding) / 변수의 값

- 바인딩 시각은 **정확한 정보량**과 연관
  - 개체에 대해 얼마나 정확한 정보를 말할 수 있는가?
  - ex. "if" : 키워드, 제어 구조의 일종
  - ex. "sum" : 함수 이름인지, 변수 이름인지, 타입은? 내용은?
- 특정 개체의 특정 속성에 대한 바인딩 시각은 언어에 따라 다름

Early binding
  - 번역 전에 파악할 수 있는 정보가 많음
  - 실행 파일을 효율적으로 높일 수 있도록 번역
  - Compilation

Late Binding
  - 프로그래머의 선택이 더 중요
  - 더 유연한 프로그래밍
  - Interpretation