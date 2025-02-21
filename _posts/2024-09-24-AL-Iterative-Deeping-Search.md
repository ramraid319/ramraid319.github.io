---
title: "[AL] Iterative Deeping Search"
author: ramraid
date: 2024-09-24 20:00:00 +0800
categories: [Computer Science, Algorithm, Uninformed Search Strategies]
tags: [Algorithm, Search Strategies]
toc: true
comments: true
math: true
mermaid: false
pin: false
---

## Iterative Deepening Search

- 상태 공간의 지름을 모를 때, Depth Limit를 증가시키며 탐색

Iterative-lengthening-search: Path-cost limit를 증가시키며 찾음
{: .prompt-info}

### Implementation

```text
function ITERATIVE-DEEPENING-SEARCH(problem) returns a solution, or failure
  for depth = 0 to inf do
    result <-- DEPTH-LIMITED-SEARCH(problem, depth)
    if result != cutoff then return result
```

### Evaluation

- Breadth-first 처럼, Optimal, Complete하다.
  - BFS보단 약간 느리긴 하다..
- Depth-first 처럼 적당한 memory를 요구한다.
- 확장을 많이 하는 경우, 오버헤드가 매우 작다.
- Depth-Limited Search : $\sum{b^d}$의 노드가 생성, $O(b^d)$ 시간, 공간복잡도
- Iterative-Deepening Search : $db + (d-1)b^2 + b^3 + ... + 2b^{d-1} + b^d$, $O(bd)$ 시간, 공간복잡도