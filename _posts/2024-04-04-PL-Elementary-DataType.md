---
title: "[PL] PL Elementary DataType"
author: ramraid
date: 2024-04-04 20:00:00 +0800
categories: [Computer Science, Programming Language]
tags: [Programming Language]
math: false
# image:
#     path: /assets/img/cat.png
#     alt: 선형 회귀 :/
render_with_liquid: false
# pin: false
---

# Elementary DataType

### Data and Type

- Data
    - 처리 대상
    - 숫자, 문자, 군집 데이터, 복합 데이터, 메타 데이터(ex. 포인터)

- Type
    - 데이터를 분류한 것
    - 값 집합 + 연산 집합
    - 타입 자체의 속성 (배열인 경우 차원, 첨자 범위 등)을 갖는다.
    - Abstract Data Type : 연산의 구현 방법이 명시되지 않은 데이터 ( ex. 사각형, 학적부 등 )

### Data Objects and Data Values

- Data Value
    - 특정 값을 나타내는 비트 패턴

- Data Object
   - 데이터 값을 포함하는 Container 혹은 Memory Location
    - 변수 (Variable) 도 하나의 Data Object
    - ex.
       - Scalar data object : Numeric, Boolean, Characters, Enumerations
       - Composite object : String, Pointer
       - Structured object : Arrays, Records, Lists
    - OOP의 객체와는 다른 개념
    - Type, Location, Value, Name 을 가짐
    - Component
        - 다른 data object를 가리키는 pointer value (value 속성의 일종)



### Constants

- 상수
    - 변수의 일종
    - 반드시 초기화되어야 함 (value binding)
    - 값이 초기화된 후에는 바꿀 수 없음
- 상수의 종류
    - literal : 생긴 것 자체가 이름이자 값
    - named constant : 값 이외의 별도의 이름이 있음
    - manifest constant : 값 바인딩 (value binding) 이 정적(static)인 named constant

### Data Type Specification

- 이상적으로는...
    - 모든 데이터 타입 (사용자 정의 타입 포함) 에 대해 명확한 명세가 주어져야 함
- 그러나...
    - 특정 입력에 대해서는 정의되지 않을 수 있음
    - 전역 변수같은 기본적으로 주어지는 인수가 있을 수 있음
    - 부대효과, 자기수정

### Subtypes <--> Supertypes

```
 SmallType = 1..20 in Int
```

- 어떤 데이터 타입의 값 집합의 "일부"를 취하여 만든 타입
- Subtype 개념이 클라스 사이로 확장될 경우 상속 (Inheritance) 이라고 함

### Declarations

- 선언문
    - 컴파일러나 인터프리터에 데이터 객체의 이름과 타입 정보를 전달
    - 선언문은 "수행" 이 아닌, "elaboration" 된다고 말함
    - 선언문의 위치 및 종류에 따라 Scope와 Lifetime 이 결정됨

> Scope은 변수의 공간적인 개념, Life Time은 시간적인 개념
{: .prompt-info }

- 선언문의 종류
    - 명시적 선언 ex. int a = 0;
    - 암시적 선언 ex. FORTRAN. I-N으로 시작하는 변수는 정수형

- Operation 선언
    - 함수 선언도 가능함

- 선언의 목적
    - 저장 형태 결정
    - 메모리 관리
    - 다형연산 지원
    - 타입 검사

#### Type Checking

- 타입 검사
    - 연산자나 서브프로그램에 대해 적절한 개수의 인수와 적절한 타입을 사용하는지 검사
- 타입 검사 시기에 따른 분류
    - 정적 타입 검사 (static type checking) : 컴파일 시간에 검사
        ex. C, C++, Java, ...
    - 동적 타입 검사 (dynamic type checking) : 실행 시간에 검사
        ex. LISP, Perl, Prolog, ...
- Typeless Languages
    - 동적 타입 검사를 수행하는 언어 중 선언문도 없고 변수의 타입이 유동적인 언어, 주로 인터프리터를 사용하고, Flexible 함 ex. Python

#### Strong Typing

- 강력한 타입 검사
    - 타입 에러를 항상 검출할 수 있는 타입 검사
    - type safe function (operation) f: S-->R 에서 f를 수행한 결과 R 이외의 값은 나올 수 없는 경우를 type safe 하다고 한다.

- 강형언어 (Strongly-typed Language)
    - 강력한 타입 검사를 수행하는 언어
    - 대부분 강형언어라고 주장하지만, 그렇지 않은 경우가 많음
    ex. C의 union, void*, type casting 연산 등, 강력한 타입 검사를 무력화


#### Type Inference

- 타입 추론
    - 정적 타입 검사를 수행하는 언어는, 명시적 선언을 할 필요가 없음 (ex. auto)
    - 타입 추론이 명시적 선언을 보완하는 역할을 함
- ML
    - 모호하지 않은 경우에 타입 선언을 생략하기도 하는 언어
    - 언어 자체에 타입 추론 기능을 제공

#### Type Conversion and Coercion

- 타입 변환이 필요한 경우
    - 서로 다른 타입 (mixed mode) 인 경우, 타입 변환을 하여 연산
- 타입 변환의 분류
    - 명시적 : type casting 으로 타입 변환 연산을 명시적으로 나타냄
    - 암시적 : 타입 변환 규칙이 정해져 있음 (type coercion)
- 타입 변환의 분류
    - 확장 변환 (widening) : 정보 손실 없음
    - 축소 변환 (narrowing) : 정보가 손실될 수 있음

## Assignment

A := B + C;

*Pick up contents of location B, Add contents of location C, Store result into address of A*

> L-value : 객체의 위치 (box), R-value : 변수의 내용 (contents)
{: .prompt-info }

#### Assignment Issues

- Side Effect
    - 값을 다른 값에 binding 하기 때문에 Side Effect 발생
- 연속 지정 (Cascading Assignments)
    - Pascal Assignment : integer * integer -> void
    - C Assignment : integer * integer -> integer
- 지정 연산 종류
    - Scalar Assignment : value copying
    - Pointer Assignment : pointer copying
    - Record Assignment : bit-wise copying, field-wise copying

## Scalar Data and Composite Data

- Scalar Data
    - 하나의 데이터 객체는 하나의 값만 나타냄
    - 하드웨어를 통해 직접 지원
- Composite Data
    - 복합데이터, 군집데이터
    - 하나의 데이터 객체가 여러 정보를 포함
    - 소프트웨어의 도움을 받아 지원

### Numeric Data Types

- 정수
    - 정수 integer, subranges
- 실수
    - 부동소수점 수 floating-point numbers, 고정소수점 수 fixed-point real numbers
- 기타
    - 복소수 complex number, 유리수 rational numbers

#### Integer

- 2's complement 로 구현
- 산술연산, 관계연산, 대입연산, 비트연산
- 통상 descriptor가 없음

#### Subrange Types

- Integer 타입의 서브타입 ex. 1..10
- 연산은 정수형 연산을 그대로 사용
- 작은 공간에 저장할 수 있음 + 정밀한 타입 검사 가능 (month = 1..12, month = 13?? -> type error)

#### Floating-Point Real Numbers

- 정수형의 모든 연산 가능
- 소수점 이하를 처리하기 위한 연산, round, truncate, ceiling, floor 등
- IEEE Standard 754 에 32 bit, 64 bit 표현 형식 정의

### Composite Data Types

- Composite Data : 여러 데이터를 한 단위의 데이터로 만듦 ex. char -> string
- Derived Type : 기존 타입을 새로운 타입으로 만듦

#### Character Strings

- 문자열
    - primitive data type의 문자들로 이루어짐
    - 문자열 자체를 primitive type으로 제공하기도 함
    - Fixed Length : ex. char A[10]
    - Variable Length : ex. E = "ABC"

#### Pointer

- 포인터?
    - 다른 데이터 객체의 주소를 가리키기 위한 데이터 타입
- Pointer를 사용하는 이유
    - Recursive data structure 구현
    - 

> 내용 업데이트중
{: .prompt-warning }