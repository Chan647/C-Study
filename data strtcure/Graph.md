#  자료구조 : 그래프(Graph)

## 📊 그래프(Graph)란?

- 그래프(Graph)는 정점(Vertex)과 간선(Edge)으로 구성된 자료구조
- 현실 세계의 다양한 관계나 네트워크를 모델링할 수 있음
- 정점(Vertex): 노드라고도 부르며, 데이터를 저장하는 단위
- 간선(Edge): 정점 간의 관계(연결)를 나타냄
- 방향 그래프(Directed Graph): 간선이 방향을 가짐 (`A → B`)
- 무방향 그래프(Undirected Graph): 간선이 쌍방향 (`A — B`)



## 🧱 그래프 표현 방식

### 1. 인접 행렬 (Adjacency Matrix)

- 2차원 배열 사용
- 간선 존재 여부를 0 또는 1로 표시
- 정점 수가 많고 간선이 적을 경우 메모리 낭비

### 2. 인접 리스트 (Adjacency List) ✅

- 각 정점에 대해 연결된 정점 목록을 리스트로 저장
- 공간 효율성이 좋음

## 시간복잡도

- 정점 추가	               O(1)
- 간선 추가	               O(1)(무방향: O(2))
- 인접 정점 순회  	       O(degree)
- 전체 정점/간선 순회	   O(V + E)
- DFS / BFS	              O(V + E)
- 다익스트라 (힙 사용)	   O((V + E) log V)
- 벨만-포드	               O(VE)
- 플로이드-워셜	           O(V³)

## 🧪 예시 

```cpp
#include <iostream>
#include <map>
#include <list>
using namespace std;

class Graph {
private:
    map<int, list<int>> adj;

public:
    void addEdge(int u, int v, bool isDirected) {
        adj[u].push_back(v);
        if (!isDirected) {
            adj[v].push_back(u);
        }
    }

    void printGraph() {
        for (auto pair : adj) {
            cout << "정점 " << pair.first << "의 연결: ";
            for (int v : pair.second) {
                cout << v << " ";
            }
            cout << endl;
        }
    }
};

int main() {
    Graph g;
    g.addEdge(0, 1, false);
    g.addEdge(0, 4, false);
    g.addEdge(1, 2, false);
    g.addEdge(1, 3, false);
    g.addEdge(1, 4, false);
    g.addEdge(2, 3, false);
    g.addEdge(3, 4, false);

    g.printGraph();
    return 0;
}
```