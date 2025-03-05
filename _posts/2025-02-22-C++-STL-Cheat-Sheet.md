---
title: "[C++] STL Cheat Sheet"
author: ramraid
date: 2025-02-22 08:30:00 +0800
categories: [Programming, C++, Modern Programming, STL]
tags: [Programming, C++, Modern Programming, STL]
math: true
# image:
#     path: /assets/img/posts/ComputerGraphics/Lerp.png
#     alt: Lerp
render_with_liquid: false
pin: false
---

# 개요

C++ 에서는 Standard Template Library (STL) 을 제공한다. 

이는 일반적인 자료구조, 알고리즘의 클래스 및 함수 템플릿이다.

주로 **"최적화된"** stack, queue와 같은 유용한 container들을 사용한다.

이 글은 [GeeksForGeeks](https://www.geeksforgeeks.org/cpp-stl-cheat-sheet/)의 자료를 참고하여 작성했다.

# Components of STL

C++ STL에서 제공하는 요소들이 있는데, 크게 4가지가 있다.

1. Containers
2. Iterators
3. Algorithms
4. Functors

## Containers

Container는 동적 배열이나, 해시맵, Linked List, 트리 등과 같이 구조화된 데이터를 다룰 때 유용한 템플릿이다.

컨테이너는 크게 4가지로 나눌 수 있다.

### Sequential Container
  - Vector
  - List
  - Deque
  - Array
  - Forward List

#### Vector

```cpp
// 벡터 선언
vector <data_type> vector_name; // 1차원 벡터
vector < vector <data_type> > vector_name; // 2차원 벡터
vector < stack <data_type> > vector_name; // 다른 container도 활용 가능
```

```cpp
vec.begin(); // return (iterator)  "첫 번째 요소" O(1)
vec.end();   // return (iterator)  "마지막 요소 **바로 뒤**" O(1)
vec.size();  // return (size_type)       "현재 element의 수" O(1)
vec.empty(); // return (bool)      "비어있는가?" O(1)
vec.at();    // return (data_type) "특정 위치의 요소" O(1)
vec.assign();// return (void)      "vector에 값 할당" O(n)
    vec.assign(n, val);  // n 크기 벡터에 모든 값을 val로 할당
    vec.assign({val1, val2, val2, ...}); // 여러 값 할당
    vec.assign(first, last); // 다른 컨테이너의 iterator로 할당
vec.push_back(); // return (void)  "vector의 맨 뒤에 새로운 요소 삽입" O(1)
vec.pop_back();  // return (void) "vector의 맨 뒤 요소 제거" O(1)
vec.insert();    // return (iterator)  "특정 위치에 element 삽입" O(n)
vec.erase();     // return (iterator)  "특정 위치 혹은 범위의 요소 삭제" O(n)
vec.clear();     // return (void)      "모든 요소 제거" O(n)
```

#### List

```cpp
// 리스트 선언
list <data_type> list_name;
```

```cpp
list_name.begin(); // return (iterator)  "첫 번째 요소" O(1)
list_name.end();   // return (iterator)  "마지막 요소 **바로 뒤**" O(1)
list_name.size();  // return (size_type)       "현재 element의 수" O(1)
list_name.empty(); // return (bool)      "비어있는가?" O(1)
list_name.push_front(); // return (void)  "vector의 맨 앞에 새로운 요소 삽입" O(1)
list_name.push_back(); // return (void)  "vector의 맨 뒤에 새로운 요소 삽입" O(1)
list_name.pop_front();  // return (void) "vector의 맨 앞 요소 제거" O(1)
list_name.pop_back();  // return (void) "vector의 맨 뒤 요소 제거" O(1)
list_name.insert();    // return (iterator)  "특정 위치에 element 삽입" O(n)
list_name.erase();     // return (iterator)  "특정 위치 혹은 범위의 요소 삭제" O(n)
list_name.clear();     // return (void)      "모든 요소 제거" O(n)
list_name.remove();    // return (void)      "해당하는 요소를 제거" O(n)
    list_name.remove_if();    // return (void)      "람다식도 활용 가능" O(n)
```

## TODO

#### Deque

#### Array

#### Forward List

### Container Adapters
  - Stack
  - Queue
  - Priority Queue
   
### Associative Containers
  - Set
  - Multiset
  - Map
  - Multimap
   
### Unordered Containers
  - Unordered Set
  - Unordered Multiset
  - Unordered Map
  - Unordered Multimap
   
