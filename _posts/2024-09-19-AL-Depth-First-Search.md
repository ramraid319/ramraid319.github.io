---
title: "[AL] Depth First Search"
author: ramraid
date: 2024-09-19 20:00:00 +0800
categories: [Computer Science, Algorithm, Uniformed Search Strategies]
tags: [Algorithm, Search Strategies]
toc: true
comments: true
math: true
mermaid: false
pin: false
---

# Depth First Search
## Background

- Frontier 가 스택이다. (LIFO)
- 즉, Frontier의 첫번째에 있는 노드는 제일 깊은 unexpanded 노드다.
- 
## Tree-Search based implementation

### Features

- 새로운 state가 ancestors 중 하나와 같다면 제거한다.

> Redundant path는 그대로다.
{: .prompt-danger }

### Evaluation

- Modest memory requirements : $O(bm)$

> $b$ : branching factor, $m$ : maximum depth
{: .prompt-info}

- Takes $O(b^m)$ time
  - $m$ 이 $d$ 보다 훨씬 크면 매우 느림.
  - 하지만, solution들이 모여있다면, BFS보다는 좋음.
- infinite-depth 공간에서는 적용할 수 없다. -> Depth-limited Search 이용

