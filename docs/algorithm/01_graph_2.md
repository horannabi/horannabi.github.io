---
layout: default
title: 01_그래프(2)
parent: Algorithm
nav_order: 2
has_children: false
---

## 1. 그래프의 탐색  

### 1) 그래프 탐색 방법  

- DFS(깊이 우선 탐색): 루트 노드에서 시작하여 다른 분기(Branch)로 넘어가기 전, <u>한 노드에서 갈 수 있는 끝에 도달할 때까지 탐색</u>  
- BFS(너비 우선 탐색): <u>현재 노드와 가까운(인접한) 노드</u>를 순차적으로 탐색  

<br/>

### 2) DFS vs BFS 사용 구분  
- 공통: 완전 탐색  
- BFS: 최단거리 구하기

<br/>

### 3) 구현 방법  
- DFS: 스택 or 재귀함수  
- BFS: 큐  

