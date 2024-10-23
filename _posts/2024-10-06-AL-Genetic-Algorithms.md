---
title: "[AL] Genetic Algorithms"
author: ramraid
date: 2024-10-06 20:00:00 +0800
categories: [Computer Science, Algorithm, Local Search Algorithms]
tags: [Algorithm, Search Strategies]
toc: true
comments: true
math: true
mermaid: false
pin: false
---

## Genetic Algorithms

- 유한 String을 State로 정한다. 대개 0, 1로 이루어져 있다.

- Fitness Function으로 상태가 평가되고, 그에 비례하는 확률에 따라 Reproduction한다.

**Metaheuristic Algorithm**
다른 Local Search Algorithm은 Heuristic을 사용하지 않지만, Simulated Annealing과 Genetic Algorithm 은 High-Level의 Heuristic 을 사용한다.

- Crossover : 빈번히 일어나는 단계
- Mutation : 낮은 확률로 돌연변이

### Implementation

```text
function GENETIC-ALGORITHM(population, FITNESS-FN) returns an individual
    inputs: population, a set of individuals
        FITNESS-FN, a function that measure the fitness of an individual
    repeat
        new_population <-- empty set
        for i = 1 to SIZE(population) do
            x <-- RANDOM-SELECTION(population, FITNESS-FN)
            y <-- RANDOM-SELECTION(population, FITNESS-FN)

            child <-- REPRODUCE(x, y)
            if (small random probability) then child <-- MUTATE(child)
            add child to new_population
        population <-- new_population
    until some individual is fit enough, or enough time has elapsed
    return the best individual in population, according to FITNESS-FN

function REPRODUCE(x, y) returns an individual
    inputs: x, y, parent individuals

    n <-- LENGTH(x)
    c <-- random number from 1 to n
    return APPEND(SUBSTRING(x, 1, c), SUBSTRING(y, c+1, n))
```