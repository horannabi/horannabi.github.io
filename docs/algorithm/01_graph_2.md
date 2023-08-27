---
layout: default
title: 01_그래프(2)
parent: Algorithm
nav_order: 2
has_children: false
---

## 1. 그래프의 탐색  

### 1) 그래프 탐색 방법  

> **DFS (깊이 우선 탐색, Depth-First Search)**: 루트 노드에서 시작하여 다른 분기(Branch)로 넘어가기 전, <u>한 노드에서 갈 수 있는 끝에 도달할 때까지 탐색</u>
>
> **BFS (너비 우선 탐색, Breadth-First Search)**: <u>현재 노드와 가까운(인접한) 노드</u>를 순차적으로 탐색


### 2) DFS vs BFS 사용 구분  
- 공통: 완전 탐색  
- BFS: 최단거리 구하기  


### 3) 구현 방법  
- DFS: 스택 or 재귀함수  
- BFS: 큐  

<hr/>

## 2. 깊이 우선 탐색 (DFS)  
: 재귀 호출로 구현

### 1) 인접행렬 사용  

```c++
void dfs(int x) {
  check[x] = true;
  printf("%d", x);
  for (int i=1; i<=n; i++) {
    if (a[x][i] == 1 && check[i] == false) {
      dfs(i);
    }
  }
}
```

### 2) 인접리스트 사용

```c++
void dfs(int x) {
  check[x] = true;
  printf("%d", x);
  for (int i=1; i<a[x].size(); i++) {
    int y = a[x][i];
    if (check[y] == false) {
      dfs(y);
    }
  }
}
```

<hr/>

## 3. 너비 우선 탐색 (BFS)  
: 큐로 구현

### 1) 인접행렬 사용  

```c++
queue<int> q;
check[1] = true; q.push(1);
while (!q.empty()) {
  int x = q.front(); q.pop();
  printf("%d ", x);
  for (int i=1; i<=n; i++) {
    if (a[x][i] == 1 && check[i] == false) {
      check[i] = true;
      q.push(i);
    }
  }
}
```

### 2) 인접리스트 사용

```c++
queue<int> q;
check[1] = true; q.push(1);
while (!q.empty()) {
  int x = q.front(); q.pop();
  printf("%d ", x);
  for (int i=1; i<a[x].size(); i++) {
    int y = a[x][i];
    if (check[y] == false) {
      check[y] = true; q.push(y);
    }
  }
}
```
