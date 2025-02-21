---
title: "Kotlin Programming"
author: ramraid
date: 2024-04-15 20:00:00 +0800
categories: [Kotlin]
tags: [Kotlin, Android Studio]
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

## Kotlin 이란?

- JVM 에서 동작하는 프로그래밍 언어
- Android 공식 언어로, 객체지향과 함수형 프로그래밍 스타일 지원

##### 안정성

- Null Pointer Exception을 완화하기 위한 **Null Safe** 지원

```kotlin
var a: String ? = "NPE test"    // ? : 예외적으로 NULL 허용
a = null
```

```kotlin
println(${a!!})     // !! : Null Assertion, 변수가 null이 아님을 보장
```

- 엘비스 연산자

```kotlin
val l = (b?.length) ?: -1   // NULL이면 -1, 아니면 (b.length)
```

- 세이프콜

```kotlin
println(a?.length)      // NULL이면 뒤의 메소드 실행하지 않음
```

## Kotlin Grammar

#### Declare Variable

- val : value, 불변 타입
- var : variable, 가변 타입

#### Declare Function

```kotlin
fun plus_number(number1: Int, number2: Int): String {}

// fun {function name}({parameter: type}): {return type}
```

#### Collection Data Type

연관된 데이터를 하나의 변수로 관리하는 방법

선언과 초기화 -> 사용 -> 수정

- Array
  - plus() 함수를 사용해서 배열에 값을 추가

```kotlin
var list1:Array<Int> = arrayOf(10, 20, 30)
list1 = list1.plus(40)
```

- List
  - 순서가 있는 데이터 집합, 데이터의 중복을 허용
  - List는 읽기 전용, MutableList 는 수정 가능
  - MutableList는 add() 함수로 값을 추가

```kotlin
var list2: List<Int> = listOf(1, 2, 3, 4, 5)
var list3: MutableList<Int> = mutableListOf(1, 2, 3, 4, 5)
list3 = list3.add(6)
```

```kotlin
// 3의 배수
var filtered_list1 = list1.filter{it%3==0}
var filtered_list2 = list2.filter{it%3==0}
var filtered_list3 = list3.filter{it%3==0}
```

#### Condition

- if-else

```kotlin
if (ranking <= 5) idx = 0
else if (ranking <= 10>) idx = 1
```

- when

```kotlin
when(ranking % 5) {
    0 -> idx = 0
    1 -> idx = 1
    2 -> idx = 2
    3 -> idx = 3
    4 -> idx = 4
}
```

#### Loop

- for

```kotlin
for (i in grade) print(i + " ")
for (i: Int in 1 .. 5)              // 1 <= .. <= 5
for (i in 1 .. len)                 // 1 <= .. <= len
for (i in 1 until len)              // 1 <= .. < len
for (i: Int in 1 .. 5 step(2))      // 1 <= .. <= 5 step:2
for (i: Int in 5 downTo 1)          // 5 >= .. >= 1
for (i: Int in 5 downTo 1 step(2))  // 1 >= .. >= 5 step:2
```

- while

```kotlin
while (idx < grade.size) print(grade[idx++] + " ")
```

#### Casting

```kotlin
a.toString()    // cast to String

if(b is String) // is : True 1, False 0
```

#### Enum Class

- 동일한 data type의 data를 인스턴스로 하는 class
- 관련된 상수들의 집합을 정의하고, 하나의 타입으로 취급
- 객체이기 때문에 해당 값들을 변수에 할당하거나 함수의 매개변수로 전달
- 인스턴스 생성과 상속을 방지, 상수값의 타입 안정성 보장

```kotlin
enum class Year { Freshman, Sophomore, Junior, Senior }
```

#### Exception

- try-catch
  - try : 코드 실행을 시도, 해당 구역 에러 발생 감지
  - catch : try 구역의 에러 발생시 분기되어 해당 코드가 수행됨
  - finally : try-catch와 상관 없이 무조건 수행
  - 에러에 취약한 영역 감지, 정상 종료 시키는 것이 목적

```kotlin
try {
    1/divNumber
} catch (e : Exception) {
    println(e)
} finally {
    print("Hello, World")
}
```
> java.lang.ArithmeticException: / by zero
> Hello, World

- throw
  - 조건에 맞을 경우, 정의된 에러를 발생
  - Error를 유발시키는 것이 목적, 조치를 취하지 않으면 비정상 종료

```kotlin
if (divNumber == 0)
    throw Exception("error : divide by zero")
```

#### Class

```kotlin
public class Grade constructor(val name: String, score: Int) {}
```

- Class Inheritance

```kotlin
open class Person (school: String) {        // open : 상속 허용
    var school = school
    open fun print_school() {
        println(school)
    }
}

public class Grade constructor
        (school: String, score: Int) : Person(school) { // 상속
            
        }
```

#### Lambda function

- 익명함수, 간단한 함수 정의
- 모듈화로 테스트와 디버깅이 수월해짐
- 람다식과 고차함수로 다양한 함수 조합 가능, 생산성을 높임

```kotlin
val sum:(Int, Int)->(Int) = {a:Int, b:Int->(a+b)}
```

#### High-order function

- 다른 함수를 매개변수로 받거나 함수를 반환하는 함수

```kotlin
fun high_order_function(a: Int, operation:(Int, Int)->Int) {
    val result = operation(2, 3)
    println(result)
}

high_order_function(1) { a, b->  // 함수 외부에서 매개변수함수 정의
    a + b
}
```

```kotlin
enum class Delivery {STANDARD, EXPEDITED}
class Order(val itemCount: Int)

fun calcCost (delivery: Delivery): (Order)->Double{
    if(delivery == Delivery.EXPEDITED) {
        return {order -> 6+2.1*order.itemCount}
    }
    return {order->61.2*order.itemCount}
}

fun main() {
    val calculator = calcCost(Delivery.EXPEDITED)
    println("Cost : ${calculator(Order(3))}")
}
```

#### Extension function

- 클래스 밖에서 메소드 추가

```kotlin
fun Adder.add(a: Int, b: Int, c: Int, d: Int): Int {
    return a + b + c + d
}
```