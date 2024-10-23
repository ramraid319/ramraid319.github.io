---
title: "[AL] Simulated Annealing Search"
author: ramraid
date: 2024-10-04 20:00:00 +0800
categories: [Computer Science, Algorithm, Local Search Algorithms]
tags: [Algorithm, Search Strategies]
toc: true
comments: true
math: true
mermaid: false
pin: false
---

## Simulated Annealing Search

Valley 하강법의 효율과 Random Walk의 Completeness

나빠보이는 움직임을 허용시켜서 국소 최소값에서 벗어난다.
**하지만 Step size와 빈도는 점차 감소된다.**

최선의 움직임보다는 Random 움직임이 선택된다.
그 움직임으로 더 좋은 상황이 나온다면 이 선택은 유지된다.

그렇지 않으면, $e^{-\Delta E/T}$ 에 의해 결정된다.

- $\Delta E$: 평가가 악화되는 정도, 움직임의 나쁜 정도의 지수적으로 선택될 확률이 감소한다.
- $T$: Temperature, Annealing schedule에 의해 결정된다. T가 높으면 나쁜 움직임이 발생할 가능성이 높다. 

> $T$가 0이면 Simple Hill-Climbing (First choice Hill-Climbing)이다
{: .prompt-info}

Annealing Schedule이 $T$를 충분히 낮추면, 글로벌 최적값은 확률이 1이 도달된다.

### Implementation

```text
function SIMULATED-ANNEALING(problem, schedule) returns a solution state
    inputs: problem, a problem
            schedule, a mapping from time to "temperature"
    current <-- MAKE-NODE(problem.INITIAL-STATE)
    for t <-- 1 to inf do
        T <-- schedule[t]
        if T = 0 then return current
        next <-- a randomly selected successor of current
        dE <-- next.VALUE - current.VALUE
        if dE < 0 then current <-- next
        else current <-- next only with probability e^(-dE/T)
```