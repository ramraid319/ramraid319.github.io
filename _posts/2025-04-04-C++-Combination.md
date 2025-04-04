---
title: "[C++] Combination"
author: ramraid
date: 2025-04-04 10:30:00 +0800
categories: [C++, Modern Programming]
tags: [Programming, C++, Modern Programming, builtin]
math: true
render_with_liquid: true
pin: false
---

# 개요

[[C++] Permutation and Combination](https://ramraid319.github.io/posts/C++-STL-Permutation-Combination/)

이전에 `algorithm`의 `next_premutation`을 사용해서 combination을 만들었었는데, bitmasking을 사용하면 더 효율적일 수 있다.

## Example

```cpp
void findCombination(int n, int k)
{
    for (int mask = 0; mask < (1 << n); mask++) // (1)
    {
        if (__builtin_popcount(mask) != k) continue; // (2)
        vector<int> comb(n, 0);
        for (int i = 0; i < n; i++)
            if (mask & (1 << i))
                comb[i] = 1;
        // print combination
        for (auto& it : comb)
            cout << it << " ";
        cout << endl;
    }
}
```

$nCk$ 라고 하면, 위와 같이 모든 조합의 경우를 찾을 수 있다.

1. 먼저 `1 << n` 번 1씩 증가시키며 비트 표현 가능한 모든 경우를 구한다. 예를 들어 `n=5`면, `0b000000`이상 `0b100000`미만이므로 `0b00000` 이상 `0b11111` 이하가 된다.
2. `__builtin_popcount()` 혹은 `std::popcount`로 비트 1의 수를 세어, k와 같은 경우만 취급한다.

## reference

[std::popcount](https://en.cppreference.com/w/cpp/numeric/popcount)
