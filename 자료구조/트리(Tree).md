## 트리(Tree)
: 계층적 구조를 표현하는 비선형 자료구조로, 루트 노드에서 시작하여 자식 노드들로 뻗어나가는 방식으로 구성된다. 이는 JSON 구조나 DOM(Document Object Model) 등 여러 곳에서 활용되며, 데이터를 계층적으로 관리하거나 탐색하는 데 유용하다.

### 트리의 주요 개념
1. **노드(Node)**
   * 트리의 각 요소를 의미한다.
2. **루트 노드(Root Node)**
   * 트리의 최상단 노드, 부모가 없는 노드이며 트리의 시작점이다.
3. **부모 노드(Parent Node)**
   * 자식 노드를 가진 노드이다.
4. **자식 노드(Child Node)**
   * 특정 부모 노드로부터 직접 연결된 노드이다.
5. **리프 노드(Leaf Node)**
   * 자식이 없는 노드이다.
6. **간선(Edge)**
   * 노드 간의 연결을 나타낸다.
7. **서브트리(Subtree)**
   * 트리의 일부로, 특정 노드와 그 자식들을 포함하는 부분 구조이다.
8. **레벨(Level)**
   * 루트에서 특정 노드까지의 깊이를 의미한다.
  
### 트리의 종류
* **이진 트리(Binary Tree)**
  * 각 노드가 최대 2개의 자식 노드를 가지는 트리
  * 종류:
    * 완전 이진 트리(Complete Binary Tree): 모든 레벨이 꽉 차 있거나, 마지막 레벨만 왼쪽부터 채워짐.
    * 포화 이진 트리(Full Binary Tree): 모든 노드가 0개 혹은 2개의 자식 노드를 가짐.
    * 균형 이진 트리(Balanced Binary Tree): 왼쪽과 오른쪽 서브트리의 높이 차이가 일정한 트리
* **이진 탐색 트리(Binary Search Tree, BST)**
  * 왼쪽 서브트리에는 작은 값, 오른쪽 서브트리에는 큰 값이 저장되는 트리
* **N진 트리(N-ary Tree)**
  * 각 노드가 최대 N개의 자식을 가질 수 있는 트리
* **힙(Heap)**
  * 최대 힙(Max-Heap): 부모 노드가 자식 노드보다 크거나 같음
  * 최소 힙(Min-Heap): 부모 노드가 자식 노드보다 작거나 같음
* **트라이(Trie)**
  * 문자열 탐색 및 저장에 특화된 트리
 
### JavaScript로 트리 구현
* 노드 클래스
```js
class TreeNode {
  constructor(value) {
    this.value = value; //노드의 값
    this.children = []; //자식 노드 리스트
  }
}
```

* 트리 클래스
```js
class Tree {
  constructor() {
    this.root = null; // 루트 노드
  }

  addNode(value, parentValue = null) {
    const newNode = new TreeNode(value);
    if (!this.root) {
      this.root = newNode; // 루트가 없으면 새 노드를 루트로 설정
    } else {
      this._addNodeRecursively(this.root, newNode, parentValue);
    }
  }

  _addNodeRecursively(currentNode, newNode, parentValue) {
    if (currentNode.value === parentValue) {
      currentNode.children.push(newNode);
    } else {
      currentNode.children.forEach(child => {
        this._addNodeRecursively(child, newNode, parentValue);
      });
    }
  }

  //트리 출력
  print(node = this.root, level = 0) {
    if (!node) return;
    console.log(" ".repeat(level * 2) + node.value);
    node.children.forEach(child => this.print(child, level + 1));
  }
}
```

* 트리 생성 및 사용
```js
const tree = new Tree();
tree.addNode("Root"); // 루트 노드 추가
tree.addNode("Child 1", "Root"); // 자식 노드 추가
tree.addNode("Child 2", "Root");
tree.addNode("Child 1.1", "Child 1");
tree.addNode("Child 1.2", "Child 1");
tree.addNode("Child 2.1", "Child 2");

tree.print(); //트리 구조 출력
```
출력 결과:
```
Root
  Child 1
    Child 1.1
    Child 1.2
  Child 2
    Child 2.1

```

### 트리의 활용 사례
* DOM 구조 탐색: HTML DOM 트리는 트리 구조로 이루어져 있다.
* 파일 시스템: 디렉터리와 파일의 계층 구조를 표현
* 자동 완성: 트라이(Trie) 자료구조로 구현
* 게임 AI: 미니맥스 알고리즘 등에서 트리를 활용
* 이진 탐색 트리: 데이터 검색, 삽입, 삭제 최적화

