---
title: "[C++] Delegates"
author: ramraid
date: 2025-03-05 10:30:00 +0800
categories: [C++, Modern Programming]
tags: [Programming, C++, Modern Programming, STL]
math: false
render_with_liquid: true
pin: false
---

# 개요

C++ 에서는 여러가지 방식으로 Delegate를 사용할 수 있다.

## 1. functors

```cpp
struct Functor
{
  int operator()(double d)
  {
    return (int) d+1;
  }
};

Functor f;
int i = f(3.14);
```

## 2. lambda expressions (C++11)

```cpp
auto func = [](int i) -> double { return 2*i/1.15; };
double d = func(1);
```

## 3. function pointers

```cpp
int f(double d) {...}
typedef int (*MyFuncT) (double d);
MyFuncT fp = &f;
int a = fp(3.14);
```

## 4. pointer to member functions ***(fastest)***

```cpp
struct DelegateList
{
  int f1(double d) {}
  int f2(double d) {}
};

typedef int (DelegateList::* DelegateType)(double d);

DelegateType d = &DelegateList::f1;
DelegateList list;

int a = (list.*d)(3.14);
```

## 5. binding

```cpp
struct MyClass
{
  int Something(double d);
};

// auto f = std::bind(...); C++11
std::function<int(double d)> f = std::bind(&MyClass::Something, this, std::placeholders::_1);
```

## 6. templates

```cpp
template <class FunctionT>
int Something(FunctionT func)
{
  return func(3.14);
}
```

## reference

[stackoverflow - What is a C++ delegate?](https://stackoverflow.com/questions/9568150/what-is-a-c-delegate)
