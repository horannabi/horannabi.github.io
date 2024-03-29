---
layout: default
title: 01_그래프(1)
parent: Algorithm
nav_order: 1
has_children: false
---

# 그래프

## 1. 그래프 기본 개념  

### 1) 그래프란?  
- 정점(Node, Vertex)과 간선(Edge)으로 이루어진 자료구조의 일종  
- G = (V, E)로 나타냄


### 2) 단순 경로와 단순 사이클  
- 같은 정점을 두 번 이상 방문하지 않는 경로/사이클  
- 일반적안 경로/사이클은 단순 경로/사이클을 의미함


### 3) 가중치 (Weight)  
- 간선에 가중치가 있는 경우 A 노드에서 B 노드로 이동하는 거리/시간/비용 등  


### 4) 차수  
- 정점과 연결돼 있는 간선의 갯수  

<hr/>

## 2. 그래프를 표현하기 위한 방식  

> **1. 인접 행렬(Adjecency matrix):** 2차원 배열을 활용
> 
> **2. 인접 리스트(Adjacent list):** 연결 리스트를 활용


### 1) 인접 행렬  
- 정점의 갯수 N => N^2의 이차원 배열 이용  
- A[i][j] = w (i --> j 간선이 있을 때 1 or 가중치 w/ 없을 때 0)  
- 공간복잡도: O(V^2)  


> **- 장점:** 두 노드의 간선의 존재 여부를 바로 알 수 있음
> 
> **- 단점:** 노드의 개수가 많을 수록 불필요한 메모리 낭비가 일어남

``` c++
int a[10][10];    // N * N의 이차원 배열 선언 (N = 노드의 갯수)

int main() {
  int n;
  scanf ("%d", &n);
  for (int i=0; i<n; i++) {
    int u, v, w;
    scanf("%d %d %d", &u, &v, &w);
    a[u][v] = a[v][u] = w;          // w(weight)가 없을 경우 1 대입
  }
}
```


### 2) 인접 리스트  
- 링크드 리스트로 구현  
- A[i] = [ ... , j] (i와 연결된 정점을 갖고 있음)  
- 링크드 리스트는 구현하는 시간이 오래 걸리므로 vector와 같이 길이를 변경할 수 있는 배열을 이용하여 구현  
- 공간복잡도: O(E)  


> **- 장점:** 연결된 것들만 기록하여 노드가 많아질 수록 저장 공간 효율성이 좋음  
> 어떤 노드에 인접한 노드들을 바로 알 수 있음
>   
> **- 단점:** 두 노드가 연결되어 있는지 확인이 인접 행렬보다 느림


**i) 가중치가 없을 때**
``` c++
vector<int> a[10];
int main() {
  int n;
  scanf ("%d", &n);
  for (int i=0; i<n; i++) {
    int u, v;
    scanf("%d %d", &u, &v);
    a[u].push_back(v); a[v].push_back(u);
  }
}
```

**ii) 가중치가 있을 때**
``` c++
vector<pair<int,int>> a[10];
int main() {
  int n;
  scanf ("%d", &n);
  for (int i=0; i<n; i++) {
    int u, v, w;
    scanf("%d %d %d", &u, &v, &w);
    a[u].push_back(make_pair(v,w)); a[v].push_back(make_pair(u,w));
  }
}
```

