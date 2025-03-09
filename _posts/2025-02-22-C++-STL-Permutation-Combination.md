---
title: "[C++] Permutation and Combination"
author: ramraid
date: 2025-02-22 09:30:00 +0800
categories: [C++, Modern Programming]
tags: [Programming, C++, Modern Programming, STL]
math: true
render_with_liquid: false
pin: false
---

# 개요

C++ 에서 순열, 조합 문제를 해결할 때, algorithm 라이브러리에 유용한 함수가 있다.

## std::next_permutation

```cpp
template< class BidirIt >
bool next_permutation( BidirIt first, BidirIt last );

template< class BidirIt, class Compare >
bool next_permutation( BidirIt first, BidirIt last, Compare comp );
```

## 순열 Permutation 에서의 활용

***example***
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main()
{
    std::vector<int> v;
    int v_size;
    std::cin >> v_size;

    for (size_t i = 0; i < v_size; i++)
        v.push_back(i);
    
    do {
        for (auto it : v)
            std::cout << it << " ";
        std::cout << std::endl;
    } while (std::next_permutation(v.begin(), v.end()));

    return 0;
}
```

***input***
```text
3
```

***result***
```text
0 1 2 
0 2 1
1 0 2
1 2 0
2 0 1
2 1 0
```

***other case***
```cpp
std::next_permutation(v.begin(), v.end(), [](auto a, auto b) { return a > b; })
```

이런 식으로 람다식을 사용하여 내림차순으로 만들 수도 있다.

> prev_permutation()을 사용하는게 맞긴 하지만..
{: .prompt-tip }

## 조합 Combination

***example***
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main()
{
    std::vector<int> v{1, 2, 3, 4, 5};
    std::vector<bool> comb{false, false, false, true, true};

    do {
        for (size_t i = 0; i < v.size(); i++)
        {
            if(comb[i])
                std::cout << v[i] << " ";
        }
        std::cout << std::endl;
    } while (std::next_permutation(comb.begin(), comb.end()));

    return 0;
}
```

***result***
```text
4 5 
3 5
3 4
2 5
2 4
2 3
1 5
1 4
1 3
1 2
```

## reference

[cppreference-algorithm-next_permutation](https://en.cppreference.com/w/cpp/algorithm/next_permutation)
