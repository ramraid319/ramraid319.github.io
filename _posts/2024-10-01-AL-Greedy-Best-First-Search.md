---
title: "[AL] Greedy Best-first Search"
author: ramraid
date: 2024-10-01 20:00:00 +0800
categories: [Computer Science, Algorithm, Informed Search Strategies]
tags: [Algorithm, Search Strategies]
toc: true
comments: true
math: true
mermaid: false
pin: false
---

# Informed Search Strategies

큐의 노드 순서를 결정하기 위해 평가 함수를 적용한다.
평가 함수 $f(n)$ 은 노드 $n$부터 goal까지의 거리이다.

주로 **우선순위 큐**로 frontier nodes의 순서를 관리한다.

$$f(n) = g(n) + h(n)$$

$g(n)$은 시작 노드에서 $n$ 까지의 cost
$h(n)$은 Heuristic function이라 하고, $n$에서 goal까지의 최소 추정 cost

## Greedy Best-first Search

$$f(n) = h(n)$$

평가 함수는 오직 Heuristic function만으로 평가한다.
즉, $n$에서 가장 이익이 되는 경우를 적용한다.

{: .prompt-info }

Uniform-Cost Search 에서는 $f(n) = g(n)$이다.

### example

**TODO**

### Evalutation

- 유한 공간에서 불완전, 최적화되지 않는다. (무한 공간에서는 완전함)
- Heuristic funtion이 좋으면 시공간 복잡도가 줄어들음
- Time Complexity : $O(b^m)$, $m$은 탐색 공간에서의 maximum depth
- Space Complexity : 메모리에 모든 leaf nodes를 남김
