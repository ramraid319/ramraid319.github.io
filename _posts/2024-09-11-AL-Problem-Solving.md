---
title: "[AL] Problem Solving"
author: ramraid
date: 2024-09-12 20:00:00 +0800
categories: [Computer Science, Algorithm, Uniformed Search Strategies]
tags: [Algorithm, Search Strategies]
toc: true
comments: true
math: true
mermaid: false
pin: false
---

# Problem Solving

initial state에서 goal state까지의 sequence of operators (path)

#### Combinatorial Explosion

- $O(n!)$ : 비효율적

#### Nearest neighbor heuristic

- $O(n^2)$ : 비교적 짧은 지간 내에 거의 최적의 solution을 찾는다

#### To formalize or operationalize

imformal한 문제를 formal하게 바꾸는 것

- Initial state 정의
- Operators 정의
- Goal test 정의
- Path cost function 정의 : 각 path에서 진행한 action들의 cost 합

Solution : inital state에서 goal state까지의 path
Optimal Solution : Solution 중, 가장 cost가 낮은 것

### Searching for Solutions (TREE-SEARCH)

```text
function TREE-SEARCH(problem) --> returns a solution, or failure
    initialize the frontier using initial state of *problem*
    loop do
        if the frontier is empty --> return failure
        choose a leaf node and remove it from the frontier
        if the node contains a goal state --> return the corresponding solution
        expand the chosen node, adding the resulting nodes to the frontier
```
explored set의 모든 확장된 노드를 저장하여 중복되는 path를 피할 수 있다.
- 새로 생성되는 노드들은 이전에 생성된 노드들(explored set이나 frontier에 존재하는)과 겹치면 제거한다 --> GRAPH-SEARCH 알고리즘

### Searching for Solutions (GRAPH-SEARCH)

```text
function GRAPH-SEARCH(problem) --> returns a solution, or failure
    initialize the frontier using the initial state of problem
    initialize the explored set to be empty
    loop do
        if the frontier is empty --> return failure
        choose a leaf node and remove it from frontier
        if the node contains a goal state --> return the corresponding solution
        add the node to the explored set
        expand the chosen node, adding the resulting nodes to the frontier
            only if not in the frontier or explored set
```

### Searching for Solutions (CHILD-NODE)

```text
function CHILD-NODE(problem, parent, action) --> returns a node
    return a node with
        STATE = problem.RESULT(parent.STATE, action)
        PARENT = parent
        ACTION = action
        PATH-COST = parent.PATH-COST + problem.STEP-COST(parent.STATE, action)
```

### Evaluation Criteria

- Completeness : 해답을 찾는가?
- Optimality : 최적의 해를 찾는가?
- Time Complexity : 얼마나 오래 걸리는가?
- Space Complexity : 메모리가 얼마나 사용되는가?

#### Expression

- $b$, branching factor나 다음 노드의 최대 수
- $d$, 가장 얕은 goal node의 depth
- $m$, 상태 공간에서의 모든 path의 최대 길이 (maybe $\infty$)

### Two Search Strategies

#### Uninformed Search (Blind Search)

현 상태에서 goal까지 남은 step이나 path cost를 모름

#### Informed Search (Heuristic Search)

어떤 state가 더 유망한지 판별 가능.. 더 효율적이다.