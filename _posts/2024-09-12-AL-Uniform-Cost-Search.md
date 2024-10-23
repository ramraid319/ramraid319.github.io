---
title: "[AL] Uninformed Cost Search"
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

## Uninformed Cost Search

가장 얕지(Shallowest) 않은 노드 중, Frontier의 최소비용의 아직 확장되지 않은 노드를 확장시킨다.

가장 얕은 Goal보다는 **최소 비용 Solution**을 찾는 것

### Graph-Search based Implementation

Frontier는 path cost이 낮은 순서로로 정렬되는 우선순위 큐를 이용한다.

Graph-Search는 이전 경로보다 더 낫다면 중복 경로도 허용한다.

> Tree-Search 구현도 가능은 하지만 덜 효율적이다
{: .prompt-info}

### Implementation

```text
function UNIFORM-COST-SEARCH(problem) returns a solution, or failure
    node <-- a node with STATE = problem.INITIAL-STATE, PATH-COST = 0
    frontier <-- a priority queue ordered by PATH-COST, with node as the only element
    explored <-- an empty set

    loop do
        if EMPTY?(frontier) then return failure
        node <-- POP(frontier)
        if problem.GOAL-TEST(node.STATE) then return SOLUTION(node)
        add node.STATE to explored
        for each action in problem.ACTIONS(node.STATE) do
            child <-- CHILD-NODE(problem, node, action)
            if child.STATE is not in explred or frontier then
                frontier <-- INSERT(child, frontier)
            else if child.STATE is in frontier with higher PATH-COST then
                replace that frontier node with child
```

### Evaluation

모든 action 비용이 최소 $\epsilon > 0$ 이면, Optimal하며 Complete하다.

- Time, Memory Complexity: $O(b^{1+[C^*/\epsilon]})$

$C^*$: Optimal Solution의 비용

> 만약 모든 비용이 같다면, $b^{1+d}$
{: .prompt-info} 

Uniform-cost Search는 BFS보다 불필요한 노드 확장으로 더 많은 일을 한다