---
title: "[AL] Breadth First Search"
author: ramraid
date: 2024-09-12 20:00:00 +0800
categories: [Computer Science, Algorithm, Uninformed Search Strategies]
tags: [Algorithm, Search Strategies]
toc: true
comments: true
math: true
mermaid: false
pin: false
---

# Uninformed Search Strategies

#### Uniformed search (blind ssearch)

현재 state에서 goal state까지 필요한 step의 수나 path cost에 대한 정보가 없음

#### Informed search (heuristic search)

어떤 state가 더 유망한지 알고있음. --> 더 효율적

# Breadth-first Search

frontier에 있는 가장 얕은 expand되지 않은 노드를 expand한다.

```text
function BREADTH-FIRST-SEARCH(problem) --> return a solution, or failure
    node <-- a node with STATE = problem.INITIAL-STATE, PATH-COST = 0
    if problem.GOAL-TEXT(node.STATE) --> return SOLUTION(node)
    frontier <-- a FIFO queue with node as the only element
    explored <-- an empty set
    loop do
        if EMPTY?(frontier) --> return failure
        node <-- POP(frontier)
        add node.STATE to explored
        for each action in problem.ACTIONS(node.STATE) do
            child <-- CHILD-NODE(problem, node, action)
            if child.STATE is no in explored or frontier -->
                if problem.GOAL-TEST(child.STATE) --> return SOLUTION(child)
                frontier <-- INSERT(child, frontier)
```

frontier는 FIFO queue다. $O(b^d)$ 이기 때문에 frontier가 매우 커진다.

GRAPH-SEARCH의 메모리 크기는 TREE-SEARCH의 두 배를 초과하지 않는다.

## Evaluation

Complete하고 Optimal하다.
- 모든 operators가 같은 cost를 가질 때 최적이다.

Time & Memory complexity
- 최악의 경우, solution을 찾기 전 생성된 노드의 수 : $b + b^2 + b^3 + ... + b^d, O(b^d)$
- goal을 찾기 전에 d의 전체 노드 층이 확장된다. --> $O(b^{d+1})$, 즉 exponential한 time & memory complexity