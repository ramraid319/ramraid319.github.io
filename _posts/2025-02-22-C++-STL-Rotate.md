---
title: "[C++] Rotate"
author: ramraid
date: 2025-02-22 10:30:00 +0800
categories: [C++, Modern Programming]
tags: [Programming, C++, Modern Programming, STL]
math: true
render_with_liquid: false
pin: false
---

# 개요

C++ 에서 컨테이너의 elements들을 왼쪽으로 회전시키는 algorithm 라이브러리의 함수이다.

## std::rotate

```cpp
template< class ForwardIt >
ForwardIt rotate( ForwardIt first, ForwardIt middle, ForwardIt last );
template< class ExecutionPolicy, class ForwardIt >
ForwardIt rotate( ExecutionPolicy&& policy, ForwardIt first, ForwardIt middle, ForwardIt last );
```

## 활용

***example***
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    int v_size;
    std::cin >> v_size;

    std::vector<int> v(v_size);
    for (int i = 0; i < v_size; i++) {
        v[i] = i;
    }

    for (int i = 0; i < v_size; i++) {
        for (int num : v) std::cout << num << " ";
        std::cout << std::endl;
        std::rotate(v.begin(), v.begin() + 1, v.end());
    }

    return 0;
}
```

***input***
```text
5
```

***output***
```text
0 1 2 3 4 
1 2 3 4 0
2 3 4 0 1
3 4 0 1 2
4 0 1 2 3
```

## reference

[cppreference-algorithm-rotate](https://en.cppreference.com/w/cpp/algorithm/rotate)
