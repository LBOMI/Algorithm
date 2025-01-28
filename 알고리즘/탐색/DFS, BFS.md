## DFS:Depth-First Search(깊이 우선 탐색)
 - 깊이 있게 파고 드는 알고리즘
 - 현재 정점과 연결된 정점들을 갈 수 있는지 하나씩 검사하고, 특정 정점으로 갈 수 있다면 그 정점에 가서 같은 행위를 반복한다. 이때 방문한 지점은 다시 방문하지 않기 위해 표시를 해둔다.

 #### 장점
 - 코드가 직관적이고, 구현하기 쉽다.
 #### 단점
 - 깊이가 깊어지면, 메모리 비용을 예측하기 어렵다.
   - 깊이에 따라 함수가 하나씩 쌓이는 구조이다. 이 때문에 깊이가 엄청 깊어진다면 스택 메모리가 지나치게 커질 수 있다.
 - 최단 경로를 알 수 없다.

 #### JavaScript에서 DFS의 원리
 1. 큐에 시작 정점을 넣는다.
 2. 큐에서 가장 오래 있던 것을 뽑아낸다(shift). 그와 관련된 것을 큐의 앞에 넣는다.
 3. 큐의 앞에 있는 정점을 뽑아내면서 또 위와 같은 과정을 반복한다.
 4. 큐가 빌때까지 계속 반복한다.

 #### DFS 구현 함수
 ```js
 const graph = {
    A: ['B', 'C'],
    B: ['A', 'D', 'E'],
    C: ['A', 'F'],
    D: ['B'],
    E: ['B', 'F'],
    F: ['C', 'E']
};

  const DFS = (graph, startNode) => {
    const visited = []; // 탐색을 마친 노드들
    const needVisit = []; // 탐색해야할 노드들

    needVisit.push(startNode); // 노드 탐색 시작

    while (needVisit.length !== 0) { // 탐색해야할 노드가 남아있다면
       const node = needVisit.shift(); // queue이기 때문에 선입선출, shift()를 사용
       if (!visited.includes(node)) { // 해당 노드가 탐색된 적이 없다면
          visited.push(node);
          needVisit = [...graph[node], ...needVisit];
        }
    }
    return visited;
};
 ```

## BFS:Breadth-First Search(너비 우선 탐색)
 - 한 정점에서 시작하여 인접한 모든 정점을 우선적으로 탐색한 뒤, 다음 단계로 넘어가면서 탐색을 진행하는 알고리즘
 - 즉, 넓이를 우선적으로 탐색
 - 큐(Queue)를 사용하여 구현

 #### 특징
 1. 탐색 순서
    - 시작 정점에서 가까운 노드를 먼저 방문한 뒤, 점차 멀리 있는 노드 방문
    - 깊이보다는 레벨(level) 단위로 탐색
 2. 큐(Queue) 활용
    - 방문할 노드를 저장하고, 순차적으로 탐색하기 위해 FIFO(First-In-First-Out) 구조인 큐 사용
 3. 최단 경로 탐색
    - BFS는 무가중치 그래프에서 시작 노드로부터 다른 노드까지의 최단 경로를 탐색할 때 유용

 #### 동작 원리
 1. 초기화
    - 시작 노드를 큐에 삽입한다.
    - 방문한 노드를 기록하기 위한 리스트 or 배열을 생성한다.
 2. 탐색 반복
    - 큐에서 노드를 꺼내고, 해당 노드의 인접 노드를 확인한다.
    - 아직 방문하지 않은 인접 노드를 큐에 추가하고, 방문한 리스트에 추가한다.
 3. 종료
    - 큐가 비어 있을 때까지 반복한다.

 #### 장점
  - 비교적 효율적인 운영이 가능하고, 시간/공간 복잡도 측면에서 안정적이다.
  - 최단 경로를 구할 수 있다.
 #### 단점
  - 구현이 비교적 까다롭다.
  - 모든 지점을 탐색한다는 가정하에 큐에 메모리가 어느정도 준비되어 있어야 한다.

 #### 구현(JavaScript)
 ```js
   const graph = {
      A: ['B', 'C'],
      B: ['A', 'D', 'E'],
      C: ['A', 'F'],
      D: ['B'],
      E: ['B', 'F'],
      F: ['C', 'E']
  };

  const BFS = (graph, startNode) => {
    const visited = []; //방문한 노드를 기록
    const queue = [] //탐색을 위한 큐

    queue.push(startNode); // 시작 노드를 큐에 추가

    while (queue.length !== 0) { // 큐가 빌 때까지 반복
    const node = queue.shift(); // 큐의 첫 번째 노드를 꺼냄

    if (!visited.includes(node)) { // 아직 방문하지 않았다면
      visited.push(node);          // 방문 처리
      queue.push(...graph[node]);  // 인접 노드를 큐에 추가
    }
  }
  return visited;
};
 ```

***
#### 참고
https://velog.io/@sean2337/Algorithm-DFS%EC%99%80-BFS%EC%9D%98-%EC%89%AC%EC%9A%B4-%EA%B0%9C%EB%85%90-JavaScript-%EA%B5%AC%ED%98%84-%EB%B0%A9%EB%B2%95#dfs%EC%9D%98-%EC%9E%A5%EB%8B%A8%EC%A0%90
