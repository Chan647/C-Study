# 📌 C++ 알고리즘 : 깊이 우선 탐색 (DFS, Depth-First Search)

---

## 📚 DFS(Depth-First Search)란?

- 그래프 또는 트리에서 한 방향으로 끝까지 깊게 탐색한 후, 더 이상 갈 수 없으면 되돌아와서 다른 경로를 탐색하는 알고리즘
- 스택(Stack) 또는 재귀 함수를 이용하여 구현됨
- 방문한 노드를 다시 방문하지 않도록 체크가 필요
- 재귀 함수 또는 명시적 스택 사용 가능
- 구현이 간단하고 직관적

---

## ✅ DFS 예제 


### 예제 그래프

```
1 - 2
|   |
3 - 4
```
---

```cpp
#include <iostream>
#include <vector>

using namespace std;

vector<vector<int>> graph;
vector<bool> visited;

void dfs(int node) {
    visited[node] = true;
    cout << node << " ";

    for (int next : graph[node]) {
        if (!visited[next]) {
            dfs(next);
        }
    }
}

int main() {
    int n = 4;

    graph.resize(n + 1);
    visited.resize(n + 1, false);

    graph[1].push_back(2);
    graph[1].push_back(3);
    graph[2].push_back(1);
    graph[2].push_back(4);
    graph[3].push_back(1);
    graph[3].push_back(4);
    graph[4].push_back(2);
    graph[4].push_back(3);

    cout << "DFS 시작 노드: 1\n";
    dfs(1);

    return 0;
}
```

---

## ✅ 코드 설명

| 코드 | 설명 |
|------|------|
| `graph` | 인접 리스트로 그래프 표현 |
| `visited` | 노드 방문 여부 저장 |
| `dfs(node)` | 재귀적으로 노드를 방문하며 탐색 |
| `graph.resize(n+1)` | 1번 노드부터 시작하므로 n+1 크기 할당 |
| `dfs(1);` | 1번 노드부터 DFS 시작 |

---

## ✅ 출력 결과

```
DFS 시작 노드: 1
1 2 4 3
```

---

## ✅ 요약

- DFS는 한 방향으로 깊게 탐색 후, 막히면 되돌아오는 방식
- 재귀적 구현이 직관적이며 활용도가 높음
- 방문 체크 필수