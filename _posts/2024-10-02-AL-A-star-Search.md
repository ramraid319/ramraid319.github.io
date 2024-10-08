---
title: "[AL] A* Search"
author: ramraid
date: 2024-10-02 20:00:00 +0800
categories: [Computer Science, Algorithm, Informed Search Strategies]
tags: [Algorithm, Search Strategies]
toc: true
comments: true
math: true
mermaid: false
pin: false
---

## A* Search

평가 비용을 최소화함

$$f(n) = g(n) + h(n)$$

Uniform-cost Search와 같지만, $g$ 대신 $g + h$ 를 사용한다.

### Tree

트리 탐색에서의 A* 알고리즘은 $h(n)$이 비용을 과하게 평가하지 않을 때 최적이다. 즉, $h(n)$은 허용 가능한 범위에서 이루어져야 한다.

$C^*$ 가 최적 비용이라고 한고, suboptimal한 goal node $G_2$가 frontier에 나타난다고 가정하면,

$$f(G_2) = g(G_2) + h(G_2) = g(G_2) > C^*$$
$$(h(G_2) = 0)$$

그러나, frontier 노드 $n$은,
$$f(n) = g(n) + h(n) \leq C^*$$

$f(n) < g(G_2)$이므로, $G_2$는 확장되지 않는다.

$h(n)$이 허용 가능하더라도 A* 그래프 검색은 중복 경로를 무시하여, frontier에 최적 경로의 노드가 하나도 없을 수 있다.

A* 그래프 탐색의 최적화를 위해 **consistency** 라는 더 강력한 조건이 필요하다.

$h(n)$은 모든 노드 $n$에 대해, $n$과 다음 노드 $n'$은 아래 식을 만족한다.
$$h(n) \leq c(n, a, n') + h(n')$$
$c(n, a, n')$은 $n$에서 $n'$로의 action $a$의 step cost이다

### Graph

그래프 탐색에서의 A* 알고리즘은 $h(n)$이 consistent면, 최적이다.

모든 경로에서 $f(n)$의 값은 감소하지 않고, A* graph search로 확장된 시퀀스는 $f(n)$의 감소하지 않는 순서로 되어있다.

## Evaluatoin

A* Search Algorithm은 최적이며 완전하다.

- Time Complexity : Exp time complexity
- Space Complexity : Exp space complexity
- $f(n) > C^*$인 모든 subtree를 pruning한다.