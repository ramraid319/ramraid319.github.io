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

# Uninformed Cost Search

가장 얕지 않은 노드 중, Frontier의 최소비용의 아직 확장되지 않은 노드를 확장시킨다.

## Graph-Search based Implementation

Frontier로 path cost를 기준으로 정렬되는 우선순위 큐를 이용한다.

