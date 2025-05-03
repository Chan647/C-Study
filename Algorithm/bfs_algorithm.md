
# 📌 C++ 알고리즘 : 너비 우선 탐색 (BFS, Breadth-First Search)

---

## ✅  BFS(Breadth-First Search)란?
- 그래프에서 가까운 노드부터 먼저 방문하는 탐색 알고리즘
- 큐(Queue)를 이용해서 탐색하며, 최단 거리 탐색 등에 자주 사용됨
- 너비 우선 탐색은 레벨별로 방문함
- 먼저 들어간 노드를 먼저 꺼냄 (FIFO)
- 트리, 그래프 모두에 적용 가능

---

## 🔄  BFS 동작 순서

1. 시작 노드를 큐에 삽입하고 방문 처리
2. 큐에서 노드를 꺼냄
3. 꺼낸 노드에 인접한 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리
4. 큐가 빌 때까지 2~3 과정을 반복

---

## ✅  BFS 구현 예제

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

vector<vector<int>> graph = {
    {},         // 0번 노드는 사용하지 않음
    {2, 3, 8},  // 1번 노드에 연결된 노드들
    {1, 7},
    {1, 4, 5},
    {3, 5},
    {3, 4},
    {7},
    {2, 6, 8},
    {1, 7}
};

vector<bool> visited(9, false); // 방문 기록

void bfs(int start) {
    queue<int> q;
    q.push(start);
    visited[start] = true;

    while (!q.empty()) {
        int node = q.front();
        q.pop();
        cout << node << " ";

        for (int i = 0; i < graph[node].size(); i++) {
            int next = graph[node][i];
            if (!visited[next]) {
                q.push(next);
                visited[next] = true;
            }
        }
    }
}

int main() {
    bfs(1); 
    return 0;
}
```

---

## ✅ 출력 결과

```
1 2 3 8 7 4 5 6
```

- 시작점인 1번 노드에서 가까운 순서대로 방문하는 모습

---

## ✅ 요약

| 항목 | 설명 |
|------|------|
| 자료구조 | Queue |
| 장점 | 최단 거리 탐색 가능 |
| 사용 예시 | 미로 찾기, 최단 경로 문제 |
| 시간복잡도 | O(V + E) (V: 노드 수, E: 간선 수) |

---

## 🆚 DFS vs BFS

| 항목 | DFS | BFS |
|------|-----|-----|
| 방문 순서 | 깊이 우선 | 너비 우선 |
| 자료구조 | 스택 or 재귀 | 큐 |
| 주요 사용처 | 백트래킹, 순열/조합 | 최단 거리, 레벨 탐색 |
