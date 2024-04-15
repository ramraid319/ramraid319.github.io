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

## Kotlin Grammar

#### Declare Variable

- val : value, 불변 타입
- var : variable, 가변 타입

#### Declare Function

```kotlin
fun plus_number(number1: Int, number2: Int): String {}

// fun {function name}({parameter: type}): {return type}
```
