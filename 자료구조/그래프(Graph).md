## 그래프란?
: **정점(Vertex)**과 **간선(Edge)**으로 구성된 자료구조로, 각 정점은 객체나 값 등을 나타내고, 간선은 정점들 간의 관계를 나타낸다. 예를 들어 소셜 네트워크에서 사람들 간의 관계나 지도에서 도시 간의 경로 등이 그래프로 모델링될 수 있다.

* **방향 그래프(Directional Graph)**: 간선에 방향이 있음 (ex: A → B)
* **무방향 그래프(Undirected Graph)**: 간선에 방향이 없음 (ex: A ↔ B)

### 그래프 구현 방법
JavaScript에서 그래프는 일반적으로 *인접 리스트(Adjacency List)* 또는 *인접 행렬(Adjacency Matrix)*로 구현된다.

**1. 인접 리스트 (Adjacency List)**
 각 정점에 연결된 다른 정점들을 리스트로 저장하는 방식이다. 이 방식은 메모리 효율적이며, 주로 정점 수가 많고 간선이 적은 경우에 유리하다.
```js
class Graph {
  constructor() {
    this.adjacencyList = {};
  }

  // 정점 추가
  addVertex(vertex) {
    if (!this.adjacencyList[vertex]) {
      this.adjacencyList[vertex] = [];
    }
  }

  // 간선 추가 (무방향 그래프)
  addEdge(vertex1, vertex2) {
    if (this.adjacencyList[vertex1]) {
      this.adjacencyList[vertex1].push(vertex2);
    }
    if (this.adjacencyList[vertex2]) {
      this.adjacencyList[vertex2].push(vertex1);
    }
  }

  // 간선 추가 (방향 그래프)
  addDirectedEdge(vertex1, vertex2) {
    if (this.adjacencyList[vertex1]) {
      this.adjacencyList[vertex1].push(vertex2);
    }
  }

  // 그래프 출력
  printGraph() {
    for (let vertex in this.adjacencyList) {
      console.log(`${vertex} -> ${this.adjacencyList[vertex].join(", ")}`);
    }
  }
}

const graph = new Graph();
graph.addVertex("A");
graph.addVertex("B");
graph.addVertex("C");
graph.addEdge("A", "B");
graph.addEdge("B", "C");
graph.printGraph();
```

**2. 인접 행렬 (Adjacency Matrix)**
 정점 간의 관계를 2D 배열로 표현하는 방식이다. 각 행과 열은 정점에 해당하며, 배열의 각 요소는 해당하는 두 정점 간에 간선이 있는지 여부를 나타낸다. 이 방식은 메모리 사용이 많지만, 간선의 존재 여부를 빠르게 확인할 수 있다.

```js
class GraphMatrix {
  constructor(size) {
    this.size = size;
    this.adjacencyMatrix = Array(size).fill().map(() => Array(size).fill(0));
  }

  // 정점 간에 간선 추가
  addEdge(vertex1, vertex2) {
    this.adjacencyMatrix[vertex1][vertex2] = 1;
    this.adjacencyMatrix[vertex2][vertex1] = 1; // 무방향 그래프
  }

  // 간선 확인
  hasEdge(vertex1, vertex2) {
    return this.adjacencyMatrix[vertex1][vertex2] === 1;
  }

  printMatrix() {
    console.log(this.adjacencyMatrix);
  }
}

const graphMatrix = new GraphMatrix(3);
graphMatrix.addEdge(0, 1);
graphMatrix.addEdge(1, 2);
graphMatrix.printMatrix();
```

### 그래프 탐색
**1. 깊이 우선 탐색 (DFS)**
: 가능한 한 깊이 들어가면서 탐색을 진행하고, 더 이상 갈 수 없으면 뒤로 돌아가 다른 경로를 탐색하는 방식이다.
```js
class GraphDFS {
  constructor() {
    this.adjacencyList = {};
  }

  addVertex(vertex) {
    if (!this.adjacencyList[vertex]) {
      this.adjacencyList[vertex] = [];
    }
  }

  addEdge(vertex1, vertex2) {
    this.adjacencyList[vertex1].push(vertex2);
    this.adjacencyList[vertex2].push(vertex1); // 무방향 그래프
  }

  dfs(start) {
    const visited = new Set();
    this._dfsHelper(start, visited);
  }

  _dfsHelper(vertex, visited) {
    if (!visited.has(vertex)) {
      console.log(vertex);
      visited.add(vertex);
      this.adjacencyList[vertex].forEach(neighbor => this._dfsHelper(neighbor, visited));
    }
  }
}

const graphDFS = new GraphDFS();
graphDFS.addVertex("A");
graphDFS.addVertex("B");
graphDFS.addVertex("C");
graphDFS.addEdge("A", "B");
graphDFS.addEdge("B", "C");
graphDFS.dfs("A");
```
**2. 너비 우선 탐색 (BFS)**
: 가까운 정점부터 차례대로 탐색하며, 큐를 사용하여 탐색한다.
```js
class GraphBFS {
  constructor() {
    this.adjacencyList = {};
  }

  addVertex(vertex) {
    if (!this.adjacencyList[vertex]) {
      this.adjacencyList[vertex] = [];
    }
  }

  addEdge(vertex1, vertex2) {
    this.adjacencyList[vertex1].push(vertex2);
    this.adjacencyList[vertex2].push(vertex1); // 무방향 그래프
  }

  bfs(start) {
    const visited = new Set();
    const queue = [start];
    visited.add(start);

    while (queue.length > 0) {
      const vertex = queue.shift();
      console.log(vertex);

      this.adjacencyList[vertex].forEach(neighbor => {
        if (!visited.has(neighbor)) {
          visited.add(neighbor);
          queue.push(neighbor);
        }
      });
    }
  }
}

const graphBFS = new GraphBFS();
graphBFS.addVertex("A");
graphBFS.addVertex("B");
graphBFS.addVertex("C");
graphBFS.addEdge("A", "B");
graphBFS.addEdge("B", "C");
graphBFS.bfs("A");
```
