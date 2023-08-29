# DFS와 BFS

## DFS(Depth-First Search, 깊이 우선 탐색)
- DFS는 현재 노드에서 다음 노드로 깊게 들어가며 탐색한다.
- 스택(stack)을 사용하여 구현할 수 있으며, 재귀 함수를 사용하여 구현하는 것이 일반적이다.
- 방문하지 않은 인접 노드를 찾아 방문하고, 더 이상 방문할 인접 노드가 없으면 이전 노드로 돌아가서 다시 탐색한다.

## BFS (Breadth-First Search, 너비 우선 탐색)
- BFS는 현재 노드의 모든 인접 노드를 먼저 방문하며 탐색한다.
- 큐(queue)를 사용하여 구현한다.
- 방문하지 않은 인접 노드를 모두 큐에 넣고, 큐에서 노드를 꺼내 방문하며 탐색한다.

```python
from collections import defaultdict, deque

# 그래프 생성 (인접 리스트)
graph = defaultdict(list)
graph[1] = [2, 3, 4]
graph[2] = [1, 5]
graph[3] = [1]
graph[4] = [1, 6, 7]
graph[5] = [2]
graph[6] = [4]
graph[7] = [4]

# DFS
def dfs(graph, v, visited):
    # graph: 그래프, v: 현재 노드, visited: 방문 여부를 나타내는 딕셔너리
    visited[v] = True                        # 현재 노드를 방문했다고 표시
    print(v, end=' ')
    for neighbor in graph[v]:                # 현재 노드의 인접 노드 순회
        # 인접 노드에 방문하지 않았다면 재귀로 함수 호출
        if not visited[neighbor]:
            dfs(graph, neighbor, visited)

visited = {node: False for node in graph}
print("DFS:", end=' ')
dfs(graph, 1, visited)
print()

# BFS
def bfs(graph, start):
    # graph: 그래프, start: 시작 노드
    visited = {node: False for node in graph}
    queue = deque([start])                   # 시작 노드를 포함하는 큐 생성
    visited[start] = True
    while queue:                             # 큐가 비어있지 않는 동안 반복
        v = queue.popleft()                  # 큐에서 노드 하나를 꺼냄
        print(v, end=' ')
        for neighbor in graph[v]:
            if not visited[neighbor]:        # 인접 노드에 방문되지 않았다면
                queue.append(neighbor)       # 인접 노드를 큐에 추가
                visited[neighbor] = True

print("BFS:", end=' ')
bfs(graph, 1)
```

## 관련 문제
### 백준
- [[S2] DFS와 BFS](https://www.acmicpc.net/problem/1260)
