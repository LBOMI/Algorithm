## 해시(Hash)
: 자바스크립트에서 **해시**라는 개념은 *특정 데이터의 키와 값을 효율적으로 저장하고 검색*하는 데 사용된다.
  - 자바스크립트에서 해시를 직접적으로 다루는 기본 자료형은 없지만, '객체(Object)'와 'Map'을 사용해 해시처럼 사용할 수 있다.

### 객체(Object)를 이용한 해시
: js의 객체는 키-값 쌍으로 데이터를 저장할 수 있어 해시처럼 사용할 수 있다.

```js
const hash = {
  key1: "value1",
  key2: "value2",
};

//값 추가
hash.key3 = "value3";

//값 읽기
console.log(hash.key1); //"value1"

//값 삭제
delete hash.key2;
console.log(hash); // { key1: "value1", key3: "value3" }
```
- 키는 문자열 또는 심볼만 허용된다.
- 작은 데이터에서 효율적이다.
- 객체를 해시로 사용할 때, 원하지 않는 속성이 상속될 수 있으므로 `Object.create(null)`을 사용하여 순수 객체를 생성하는 것이 좋다.
```js
const pureHash = Object.create(null);
pureHash.key1 = "value1";
console.log(pureHash); // { key1: "value1" }
```

### Map 객체를 이용한 해시
: ES6에서 추가된 Map 객체는 객체보다 더 강력하고 유연한 해시를 제공한다.

```js
const map = new Map();

// 값 추가
map.set("key1", "value1");
map.set("key2", "value2");

// 값 읽기
console.log(map.get("key1")); // "value1"

// 값 삭제
map.delete("key2");

// 크기 확인
console.log(map.size); // 1
```
- 장점
  - key로 *모든 자료형(문자열, 숫자, 객체 등)*을 사용할 수 있다.
  - 삽입된 순서를 유지한다.
  - 큰 데이터에서 더 효율적이다.
  - `for...of` 또는 `forEach`를 사용하여 순회할 수 있다.
    ```js
    for (const [key, value] of map) {
      console.log(key, value);
    }
    ```

### 해시 함수
: 임의의 데이터를 고정된 길이의 해시 값으로 변환하는 함수이다. Js에서는 암호화 관련 해시를 생성할 때 `crypto`모듈(Node.js) 또는 외부 라이브러리를 사용한다.

* Node.js 예제
  ```js
  const crypto = require("crypto");

  const hash = crypto.createHash("sha256");
  hash.update("Hello, world!");
  console.log(hash.digest("hex")); // 해시 값 출력
  ```

* 브라우저 환경
  ```js
  async function generateHash(message) {
  const msgBuffer = new TextEncoder().encode(message);
  const hashBuffer = await crypto.subtle.digest("SHA-256", msgBuffer);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, "0")).join("");
  }

  generateHash("Hello, world!").then(console.log); // 해시 값 출력
  ```
