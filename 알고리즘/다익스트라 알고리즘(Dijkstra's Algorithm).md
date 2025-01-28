## 다익스트라 알고리즘(Dijkstra's Algorithm) 
* 다이나믹 프로그래밍을 활용한 대표적인 최단 경로 탐색 알고리즘이다.
* 가중치가 있는 그래프에서 작동하며, 모든 간선의 가중치가 음수가 아니어야 한다(즉, 0이상이어야 함).
* 네트워크 경로 최적화, 지도 서비스, 데이터 라우팅 등에 사용된다.

### 동작 원리
1. 시작 정점 초기화
   * 시작 정점에서 각 정점까지의 거리를 무한대(∞)로 설정한다. 시작 정점의 거리를 0으로 초기화한다.
   * 시작 정점을 방문하지 않은 상태로 추가한다.

2. 최단 거리 계산
   * 현재 방문하지 않은 정점들 중 최단 거리 값을 가진 정점을 선택한다.
   * 선택한 정점의 인접한 정점들의 거리를 업데이트한다.
     * 새로운 거리 = 현재 정점까지의 거리 + 현재 정점에서 인접 정점으로 가는 거리
     * 계산된 새로운 거리가 기존 값보다 작으면 업데이트한다.

3. 방문 처리
   * 선택한 정점을 방문 처리하고, 이 과정을 모든 정점이 방문될 때까지 반복한다.
  
4. 종료
   * 모든 정점을 방문하면, 시작 정점에서 각 정점까지의 최단 경로가 계산된다.
  
### javaScript 구현 예제
```js
class PriorityQueue {
  constructor() {
    this.values = [];
  }

  enqueue(val, priority) {
    this.values.push({ val, priority });
    this.sort();
  }

  dequeue() {
    return this.values.shift();
  }

  sort() {
    this.values.sort((a, b) => a.priority - b.priority);
  }
}

function dijkstra(graph, start) {
  const distances = {};
  const pq = new PriorityQueue();
  const previous = {};
  const result = [];

  // 초기화
  for (let vertex in graph) {
    if (vertex === start) {
      distances[vertex] = 0;
      pq.enqueue(vertex, 0);
    } else {
      distances[vertex] = Infinity;
    }
    previous[vertex] = null;
  }

  // 알고리즘 실행
  while (pq.values.length) {
    const current = pq.dequeue().val;

    if (current) {
      for (let neighbor in graph[current]) {
        const distance = distances[current] + graph[current][neighbor];

        if (distance < distances[neighbor]) {
          distances[neighbor] = distance;
          previous[neighbor] = current;
          pq.enqueue(neighbor, distance);
        }
      }
    }
  }

  return distances;
}

// 그래프 정의 및 실행
const graph = {
  A: { B: 4, C: 2 },
  B: { A: 4, C: 1, D: 5 },
  C: { A: 2, B: 1, D: 8, E: 10 },
  D: { B: 5, C: 8, E: 2 },
  E: { C: 10, D: 2 }
};

console.log(dijkstra(graph, "A")); 
```

#### 코드 설명
1. **PriorityQueue**: 우선순위 큐를 구현하여 거리 값이 작은 정점을 먼저 처리
2. **Graph**: 그래프는 객체 형태로 표현하며, 각 정점은 연결된 정점과 가중치를 포함
3. **dijkstra 함수**: 다익스트라 알고리즘을 실행하여 시작 정점으로부터 모든 정점까지의 최단 거리를 계산

### 특징
* 시간 복잡도 -> 인접 리스트와 우선순위 큐를 사용하면 O((V+E)logV)로 효율적이다.
* 단점 -> 가중치가 음수인 경우 잘못된 결과를 반환할 수 있다.
  
