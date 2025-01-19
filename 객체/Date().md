## Date()
: `Date()`객체는 JavaScript에서 날짜와 시간을 다루기 위해 사용되는 내장 객체이다. `Date` 객체를 사용하면 현재 날짜와 시간, 특정 날짜 계산, 시간 차이 측정 등을 할 수 있다.

### 객체 생성
```js
// 1. 현재 날짜와 시간
const now = new Date();
console.log(now); // 현재 날짜와 시간

// 2. 특정 날짜와 시간 (연, 월(0부터 시작), 일, 시, 분, 초, 밀리초)
const specificDate = new Date(2025, 0, 19, 15, 30, 0); // 2025년 1월 19일 15:30:00
console.log(specificDate);

// 3. ISO 8601 문자열
const isoDate = new Date("2025-01-19T15:30:00Z");
console.log(isoDate);

// 4. Unix 타임스탬프 (1970년 1월 1일 00:00:00 UTC부터의 밀리초)
const fromTimestamp = new Date(1674000000000); // 밀리초 단위
console.log(fromTimestamp);

// 5. 문자열
const stringDate = new Date("January 19, 2025 15:30:00");
console.log(stringDate);
```

### Date 메서드
* Getter 메서드(읽기)
```js
const date = new Date();

console.log(date.getFullYear()); //연도
console.log(date.getMonth());    // 월(0부터 시작, 0=1월, 11=12월)
console.log(date.getDate());     // 일 (1부터 시작)
console.log(date.getDay());      // 요일 (0=일요일, 6=토요일)
console.log(date.getHours());    // 시
console.log(date.getMinutes());  // 분
console.log(date.getSeconds());  // 초
console.log(date.getMilliseconds()); // 밀리초
console.log(date.getTime());     // Unix 타임스탬프 (밀리초 단위)
console.log(date.getTimezoneOffset()); // UTC와의 차이 (분 단위)
```

* Setter 메서드(수정)
```js
const date = new Date();

date.setFullYear(2025); //연도 설정
date.setMonth(0);       // 월 설정 (0=1월)
date.setDate(19);       // 일 설정
date.setHours(15);      // 시 설정
date.setMinutes(30);    // 분 설정
date.setSeconds(0);     // 초 설정
console.log(date);
```

* 날짜 계산
```js
const date1 = new Date();
const date2 = new Date("2025-01-19");

// 날짜 차이 계산 (밀리초 단위)
const diff = date2 - date1; // 두 날짜의 차이
const diffDays = diff / (1000 * 60 * 60 * 24); // 일수 계산
console.log(`두 날짜의 차이는 ${diffDays.toFixed(0)}일입니다.`};
```

### 유용한 예제
* 현재 날짜와 시간을 포맷팅
```js
const now = new Date();
console.log(`${now.getFullYear()}-${now.getMonth() + 1}-${now.getDate()}`);
console.log(`${now.getHours()}:${now.getMinutes()}:${now.getSeconds()}`);
```

* 일주일 뒤 날짜 계산
```js
const today = new Date();
today.setDate(today.getDate() + 7); // 현재 날짜에 7일 추가
console.log(today);
```

* 날짜를 UTC 기준으로 설정
```js
const utcDate = new Date(Date.UTC(2025, 0, 19, 15, 30, 0));
console.log(utcDate.toUTCString()); // UTC 기준 문자열
```

### 주의할 점
* 월은 0부터 시작
  * JavaScript에서 `Date`의 `Month`는 0부터 시작한다. (0=1월, 11=12월)
* 시간대(Timezone)
  * `Date` 객체는 기본적으로 시스템의 로컬 시간대를 사용합니다. UTC 기준으로 작업하려면 `toUTCString()`, `getUTCHours()`와 같은 UTC 메서드를 사용해야 한다.
* 날짜 문자열 형식
  * 문자열 형식이 브라우저마다 다르게 해석될 수 있으므로 ISO 8601 형식(`YYYY-MM-DDTHH:mm:ss.sssZ`)을 사용하는 것이 안전하다.
