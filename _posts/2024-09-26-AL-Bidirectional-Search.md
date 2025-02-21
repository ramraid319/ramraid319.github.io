---
title: "[AL] Bidirectional Search"
author: ramraid
date: 2024-09-26 20:00:00 +0800
categories: [Computer Science, Algorithm, Uninformed Search Strategies]
tags: [Algorithm, Search Strategies]
toc: true
comments: true
math: true
mermaid: false
pin: false
image:
    path: ../assets/img/posts/Algorithm/Bidirectional-Search.png
    alt: Bidirectional Search
---

## Bidirectional Search

Initial과 Goal State에서 동시에 시작해서, $O(b^{d/2})$ 안에 찾을 수 있음 ($2b^{d/2} << b^d$)

![Bidirectional](../assets/img/posts/Algorithm/Bidirectional-Search.png)


### Issues
- Goal State가 여러개 있는 경우
- Goal State의 정보만 가진 경우
- 새로 생긴 노드가 반대편에도 나타났는지 확인할 효율적인 방법이 필요
- 각 절반에서 사용할 Search Strategy는?

#### Comparing Uniformed Search Strategies

![ComparingUniformedSearchStrategies](../assets/img/posts/Algorithm/Comparing-Uniformed-Search.png)

#### Tree Search vs. Graph Search

![Tree-Graph-Search](../assets/img/posts/Algorithm/TreeVSGraph.png)