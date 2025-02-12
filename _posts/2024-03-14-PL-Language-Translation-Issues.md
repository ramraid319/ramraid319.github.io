---
title: "[PL] Language Translation Issues"
author: ramraid
date: 2024-03-14 20:00:00 +0800
categories: [Computer Science, Programming Language]
tags: [Programming Language, Automata]
math: true
# image:
#     path: /assets/img/cat.png
#     alt: 선형 회귀 :/
render_with_liquid: false
# pin: false
---

# Language Translation Issues

## 구문과 의미

- 구문 Syntax
  - '제대로 생긴 프로그램' 에 대한 규정
  - Readability
  - Writeability
  - Ease of verifiability
  - Ease of Translation
  - Lack of ambiguity

- 의미 Semantics
  - '어떤 동작'을 하는가에 대한 규정

#### 구문 표기법

표준적 구문 표기법

- BNF (Backus-Naur Form)
- EBNF (Extended BNF)
- CFG (Context-Free Grammar)
- 위 표기법의 표현력은 모두 같다.

Static Semantics

- CFG로 나타낼 수 없는 범위의 구문 규정
- Semantics의 범주에 포함시키기도 함
- Attribute Grammar로 표현

#### 의미 표기법

- Axiomatic Semantics
  - 프로그램의 의미를 predicate transformer로 해석
- Denotational Semantics
  - 프로그램의 의미를 semantic function을 통한 evaluation으로 해석
- Operational Semantics
  - 프로그램의 의미를 state transformer로 해석
  - state는 machine state를 나타냄

#### 번역

- 어휘분석 (Lexical Analysis; scanning)
  - 프로그램을 단어로 나눔
  - 주석 제거

```
x := a*2 + b*(x*3)
->  id<x> assign id<a> times int<2> plus id<b>
    times lparen id<x> times int<3> rparen
```

- 구문분석 (Syntax Analysis; parsing)
  - BNF 등에 입각하여 단어들의 나열을 tree로 표현

- 의미분석 (Semantic Analysis)
  - 정적 의미 분석 (타입 검사 포함)
  - 각 구성요소들이 제대로 사용되었나 검사

- 코드 생성 (Code Generation)
  - tree로부터 수행 가능한 코드 생성

- 최적화 (Optimization)
  - 트리 형태 또는 코드 형태에서 수행 성능 개선

#### BNF (Backus-Naur Form)

- Nonterminal (비단말기호)
  - 다른 형태로 치환 가능한 기호 (변수) 들의 유한 집합
  - 꺾은 괄호로 감싸 나타냄
  - < sentence > < subject > < predicate > < verb > < article > < noun >
- Terminal (단말기호)
  - 더 이상 치환할 수 없는 기호 (상수) 들의 유한 집합
  - 그냥 쓰거나 따옴표로 감싸서 나타냄
  - the, boy, girl, ate, cake, "*"
- Start Symbol (시작기호)
  - 특별히 지정된 하나의 비단말기호
  - < sentence >
- Rules (productions; 생성규칙)
  - 각 비단말기호를 어떻게 바꿔 쓸 수 있는가에 대한 유한 개의 rewriting rules
  > < sentence > ::= < subject > < predicate >
  > < subject > ::= < article > < noun >
  > < noun > ::= boy | girl | cake
  - CFG 에서는 A -> BC 와 같이 표현하기도 함
- 치환 연산 (Replacement Operator)
  - 비단말기호를 규칙에 따라 다시 쓰는 것

#### 유도 Derivation

시작기호로부터 치환 연산을 반복하여 적용하는 과정
이렇게 만들어진 단말기호 나열을 문장이라고 함

e.g.
> < sentence >
> -> < subject > < predicate >
> -> < article > < noun > < predicate >
> -> the < noun > < predicate >
> -> the < noun > < verb > < article > < noun >
> -> the < noun > < verb > the < noun >
> -> the boy < verb > the < noun >
> -> the boy ate the < noun >
> -> the boy ate the cake

#### 용어

- Sentence : 시작기호로부터 유도된 단말기호의 나열
- Sentential Forms (문장형태) : 장차 문장이 될 수도 있는 형태 (이미 되었거나)
- Language : 문법의 규칙에 따라 유도 가능한 모든 문장들의 집합

## Parse Tree

유도 과정을 나타낸 트리, Derivation tree 라고도 함

- Grammar : B -> 0B | 1B | 0 | 1
- Derivation : B --> 0B --> 01B --> 010

#### 모호성 Ambiguity

어떤 문법에서 같은 문자열에 대해 두 개 이상의 파스트리가 얻어질 수 있음

구문이 모호하면 다른 의미를 내포함 가능성이 있음

대처법으로는, 문법을 변경하거나 파서에서 특정 트리를 선택하도록 한다.

#### EBNF (Extended BNF)

- Opriontal Elements: [...]
> < number > ::= < digits > [ . < digits > ]
- Alternative Elements: (...|...|...)
> < signed number > ::= (+|-) < number >
- Sequence of Elements: {...}*
> < identifier > ::= < letter > {< letter > | < digit >}*

#### Syntax Chart

- 구문 규칙을 그림으로 표현
- 좌측 비단말기호는 가장 처음 화살표의 시작 부분에 위치
- 단말기호 : 동그라미
- 비단말기호 : 네모

e.g.
> < expr > ::= < term > { (+ | -) < term > }*

![SyntaxChart](/assets/img/posts/ProgrammingLanguage/PL-Language-Translation-Issues/PL-Language-Translation-Issues-01.png){: width="420" height="209" }

## Finite State Automata: DFA와 NFA

- Grammar : 문법은 언어 생성기
- Automata : 오토마타는 언어 인식기

- Finite Automaton
  - FA M이 인식하는 언어 $L(M)=(w | \delta(A, w) = C)$ A는 초기상태, C는 최종상태 중 하나

#### DFA와 NFA

DFA (deterministic FA) : 어떤 상태에서 한 입력 기호를 보고 갈 수 있는 상태가 단 하나

NFA (nondeterministic FA) : 어떤 상태에서 한 입력 기호를 보고 갈 수 있는 상태가 여러개일 수 있음 (여러 가능성 중 하나라도 최종 상태에 도달하면 인식)

#### NFA -> DFA 변환

모든 NFA M은 DFA M' 으로 변환 가능, 갈 수 있는 모든 상태들의 집합을 DFA의 상태로 간주 (Subset Construction)

## 정규식과 정규언어

#### 정규문법 (Regular Grammar)

> < nonterminal > ::= < terminal > < nonterminal > | < terminal >

다음과 같은 생성규칙으로 이루어진 문법

우변의 특정 위치에만 비단말기호가 올 수 있으며, 하나만 허용됨

e.g.
$A \to 0A | 1A | 0$

*어떤 정규문법은 우변의 좌측 끝에만 비단말기호가 올 수 있음 (Left Linear)*

#### 정규식 (Regular Expression)

- 단말기호는 정규식
- a와 b가 정규식이면 (a|b), (ab), (a*)도 정규식
- 공문자열 $\epsilon$, 공집합 $\phi$ 도 정규식

정규식은 정규언어를 간단한 식으로 표현할 수 있다.

e.g.

2로 나누어 질 수 있는 이진 문자열
$(0|1)*0$

01을 포함한 이진 문자열
$(0|1)*01(0|1)*$

#### 정규언어 (Regular Language)

정규언어 : 일반적으로 프로그래밍 언어의 어휘의 패턴을 나타내기에 충분한 언어
정규식 : 어휘의 패턴을 나타내는 방법
FA : 어휘를 인식하기 위한 기계 -> 어휘분석기

정규언어가 필요한 이유?

Identifier, Number, Keywords, Special Symbols 와 같은 토큰을 정의 가능

## Pushdown Automata

PDA = FA + Stack
결과적으로 상태가 무한히 늘어남

입력 문자 개수를 셀 수 있음 e.g. $a^nb^n$

동작
- 입력기호(current input symbol)와 스택기호(stack top)를 읽음
- 상태전이 및 스택변경
- 입력문자열을 모두 읽고 스택이 비어있으면(혹은 최종 상태에 도달하면) 입력문자열 인식

#### PDA와 유도

- 초기 상태 : Stack Top에 시작기호가 있음
- 상태 전이
  - Stack Top이고 현재 입력기호와 같으면, Stack Top을 pop하고 현재 입력을 하나 읽는다.
  - Stack Top이 nonterminal X면, 생성규칙 X -> a 에 대하여 a를 X대신 Stack Top에 넣는다. (입력문자는 읽지 않음)
- 주의
  - 위 PDA는 비결정적임 (임의의 nonterminal X에 대해 X가 좌변인 생성규칙은 많을 수 있음)
  - 위 PDA는 스택을 비울 때 입력 문자열을 인식

#### NDPDA 와 DPDA

nondeterministic PDA와 deterministic PDA가 인식하는 언어는 다르다.

#### LR Parsing

DPDA가 인식하는 언어는 LR(k) 으로 표현 가능

**L**eft to right scan
generating **R**ight parse
with **k** symbol lookahead

LR(k) 파서의 종류
- CLR(k) : canonical LR
- SLR(k) : simple LR
- LALR(k) : lookahead LR

YACC : LALR(1) 파서 생성기, 일상적인 프로그래밍 언어 파싱 가능

#### Recursive Descent Parsing

순환 하강 파서
- 간단한 하향식 구문분석
- 문법 (BNF 또는 CFG)과 파서의 구조가 동일
- nonterminal에 해당하는 recursive 프로시저들로 구성


순환 하강 파서 구성 방법
- 각 생성규칙에 대해 생성규칙의 우변을 따라하는 프로시저 구성
- nonterminal -> 프로시저 호출
- terminal -> lookahead와 일치하는가 검사하고 일치하면 skip, 그렇지 않으면 syntax error

e.g.

BNF Rule
> < expression > ::= < term > {(+|-)< term >}*

Expression Procedure

```pascal
procedure Expression;
begin
    Term; (* Call Term to find first term *)
    while ((nextchar = '+') or (nextchar = '-') do)
    begin
        PlusType := nextchar; (*Save the operator*)
        nextchar := getchar; (*skip over operator*)
        Term;
        output(PlusType);
    end
end
```

Expression Procedure

```C
void Expression() {
    Term(); /*Call Term to find first term*/
    while (nextchar == '+' || nextchar == '-') {
        nextchar = getchar(); /*Skip over operator*/
        Term();
    }
}
```


## 요약

언어 = 구문 (Syntax) + 의미 (Semantics)
- Syntax : 제대로 생긴 프로그램을 정의
- Semantics : 제대로 생긴 프로그램의 수행 형태를 정의

프로그램 번역
- 어휘분석 -> 구문분석 -> 의미분석 -> 코드생성 및 최적화

구문 표기법
- CFG = BNF = EBNF = Syntax Chart

유도 Derivation
- Sentence, Sentential Form, Language

Parse Tree와 모호성
- 모호한 문법 : 어떤 문장에 대한 Parse Tree가 둘 이상이 되는 문법
- 우선순위로 해결, 또는 문법을 변경하여 해결

Finite State Automata
- 유한 개의 상태로 이루어진 상태 변환 기계
- DNA : 상태 전이가 결정적
- NFA : 상태 전이가 비결정적 (모든 DFA는 NFA로 표현 가능)

정규문법
- 특수한 형태의 생성규칙으로 이루어진 문법
- 정규언어를 정의

정규식
- 패턴 정의 방법
- 정규언어가 만족해야 할 패턴

정규식 -> NFA -> DFA (어휘분석 프로그램)

문법 : 언어 L(G)에 대한 설계도 G, 문장 생성기

오토마타 : 문자열, 패턴 인식기

Pushdown Automata : FA에 스택 추가 -> 무한한 상태 공간

Parsing 기법
- LR Parsing : Knuth, Bottom-Up
- Recursive Descent Parsing : 간단한 Top-Down

Recursive Descent Parser 구성
- Nonterminal : 프로시저
- Terminal : 일치하는지 검사
- Simple Code Generator