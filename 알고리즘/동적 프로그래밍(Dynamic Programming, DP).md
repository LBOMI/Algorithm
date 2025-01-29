### 📌 개념
 동적 프로그래밍(DP)은 **큰 문제를 작은 문제로 나누고, 그 결과를 저장하여 중복 계산을 줄이는 최적화 기법**이다.
 이를 통해 **시간 복잡도를 획기적으로 줄일 수 있으며,** 주로 **재귀(Top-Down)** 또는 **반복문(Bottom-Up)** 방식으로 구현된다.

#### 🏆 핵심 개념
1. **중복되는 하위 문제(Overlapping Subproblems)**
   * 같은 부분 문제가 여러 번 반복되어 계산됨.
   * ex) 피보나치 수열에서 `fib(5)`를 구할 때 `fib(3)`, `fib(4)`가 여러 번 호출됨.

2. **최적 부분 구조(Optimal Substructure)**
   * 문제의 최적해가 부분 문제의 최적해로 이루어짐.
   * ex) `fib(n) = fin(n-1) + fib(n-2)`, 즉 작은 문제들의 합이 전체 문제의 해결책이 됨.

### 🔥 동적 프로그래밍 vs 분할 정복
| 기법 | 개념 | 예시 |
|:----:|:----:|:----:|
| **동적 프로그래밍** | 문제를 작은 문제로 나누고 **결과를 저장**하여 중복 연산을 제거 | 피보나치 수열, 배낭 문제 |
| **분할 정복** | 문제를 작은 부분 문제로 나눈 후, **독립적으로 해결**하고 조합 | 병합 정렬, 퀵 정렬 |

### 🛠 동적 프로그래밍(DP) 구현 방식
#### 1️⃣ 메모이제이션 (Memoization, Top-Down)
* 재귀 + 저장(cache)
* 한 번 계산한 값을 저장해 중복 계산을 방지 (재귀 호출 시 사용)
```js
function fib(n, memo = {}) {
  if ( n <= 1 ) return n;
  if (memo[n]) return memo[n]; // 이미 계산된 값이 있으면 사용
  return memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
}

console.log(fib(10)); // 출력: 55
```
✔ 시간 복잡도: `O(n)`
✔ 공간 복잡도: `O(n)` (재귀 스택)

#### 2️⃣ 타뷸레이션 (Tabulation, Bottom-Up)
* 반복문 + 배열 저장
* 작은 문제부터 차례로 계산하며 배열에 저장 (재귀 호출 없음)
```js
function fib(n) {
  if ( n <= 1 ) return n;
  let dp = [0,1];

  for (let i = 2; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 1];
  }
  return dp[n];
}

console.log(fib(10)); // 출력: 55
```
✔ 시간 복잡도: `O(n)`
✔ 공간 복잡도: `O(n)`

#### 3️⃣ 공간 최적화 
* 배열을 사용하지 않고 변수 2개만 사용 (이전 두 값만 기억)
* 공간 복잡도: `O(1)` (메모리 절약)
```js
function fib(n) {
  if (n <= 1) return n;
  let a = 0, b = 1, temp;

  for (let i = 2; i <= n; i++) {
    temp = a + b;
    a = b;
    b = temp;
  }
  return b;
}

console.log(fib(10)); // 출력: 55
```
✔ 시간 복잡도: O(n)
✔ 공간 복잡도: O(1) ✅

### 🎯 동적 프로그래밍 활용 예시
#### 1️⃣ 배낭 문제 (Knapsack Problem)
```js
function knapsack(weights, values, capacity) {
  let n = weights.length;
  let dp = Array(n + 1).fill(0).map(() => Array(capacity + 1).fill(0));

  for (let i = 1; i <= n; i++) {
    for (let w = 0; w <= capacity; w++) {
      if (weights[i - 1] <= w) {
        dp[i][w] = Math.max(dp[i - 1][w], values[i - 1] + dp[i - 1][w - weights[i - 1]]);
      } else {
        dp[i][w] = dp[i - 1][w];
      }
    }
  }
  return dp[n][capacity];
}

//예제 실행
console.log(knapsack([2,3,4], [3,4,5], 5)); // 출력: 7
```

#### 2️⃣ 최소 동전 개수 문제 (Coin Change)
```js
function coinChange(coins, amount) {
  let dp = Array(amount + 1).fill(Infinity);
  dp[0] = 0;

  for(let coin of coins) {
    for(let i = coin; i <= amount; i++) {
      dp[i] = Math.min(dp[i], dp[i - coin] + 1);
    }
  }
  return dp[amount] === Infinity ? -1 : dp[amount];
}

//예제 실행
console.log(coinChange([1, 2, 5], 11)); // 출력: 3( 5 + 5 + 1)
```

### 🚀 정리
✅ DP는 **"중복 계산을 줄이기 위해 저장"** 하는 개념
✅ **메모이제이션(Top-Down)**: 재귀 + 저장 (캐싱)
✅ **타뷸레이션(Bottom-Up)**: 반복문 + 배열 저장
✅ **공간 최적화**: 변수만 활용하여 공간 복잡도를 낮춤

📢 **언제 DP를 사용할까?**
* 문제를 **작은 부분 문제로 나눌 수 있는 경우**
* 동일한 **부분 문제를 반복적으로 계산하는 경우**

DP를 잘 활용하면 시간을 획기적으로 줄일 수 있으며, 다양한 문제(*피보나치, 최단 경로, 배낭 문제, 동전 문제*)에 적용할 수 있다. 
