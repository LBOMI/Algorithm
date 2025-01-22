## `String.prototype.localeCompare()` 메서드
: `localeCompare()`는 JavaScript에서 두 문자열을 비교하여 문자열 정렬 순서를 결정할 때 사용된다. 언어 및 지역(locale) 정보를 고려하여 문자열을 비교할 수 있으며, 사전순 정렬 및 언어별 정렬 규칙을 지원한다.
```js
referenceString.localeCompare(compareString[, locales[, options]])
```
* `referenceString` : 기준 문자열
* `compareString` : 비교할 문자열
* `locales`(선택 사항)
  * 문자열 비교에 사용할 언어 및 지역 설정을 나타낸다. ex) `"en"`, `"ko"`, `"fr"`, `"de"` 등
  * 지정하지 않으면 기본 브라우저 설정에 따라 동작한다.
* `options` (선택 사항)
  * 비교의 세부 동작을 지정하는 옵션 객체이다.
    * `sensitivity` : 대소문자나 악센트 등을 구분할지 여부를 설정한다.
      * `"base"` : 기본 문자 비교 (악센트, 대소문자 무시)
      * `"accent"` : 악센트 비교 (대소문자 무시)
      * `"case"` : 대소문자 비교 (악센트 무시)
      * `"variant"` : 모든 요소를 비교 (기본값)
    * `ignorePunctuation` : 문장부호를 무시할지 여부 (`true` 또는 `false`).
   
### 반환값
* `-1` : `referenceString`이 `compareString`보다 앞에 있음.
* `0` : 두 문자열이 같음.
* `1` : `referenceString`이 `compareString`보다 뒤에 있음.

### 사용 예제
* 기본 비교
  ```js
  console.log("apple".localeCompare("banana")); // -1 (apple < banana)
  console.log("grape".localeCompare("grape")); // 0 (같음)
  console.log("peach".localeCompare("apple")); // 1 (peach > apple)
  ```

* 언어 설정 (locales)
  ```js
  // 독일어에서 'ä'와 'z' 비교
  console.log("ä".localeCompare("z", "de")); // -1 ('ä'는 'z'보다 앞섬)

  // 스웨덴어에서 'ä'와 'z' 비교
  console.log("ä".localeCompare("z", "sv")); // 1 ('ä'는 'z'보다 뒤)
  ```

* 대소문자 구분 (sensitivity)
  ```js
  console.log("a".localeCompare("A", "en", { sensitivity: "base" })); // 0 (대소문자 무시)
  console.log("a".localeCompare("A", "en", { sensitivity: "case" })); // 1 ('a' > 'A')
  ```

* 문장부호 무시
  ```js
  console.log("a.b".localeCompare("ab", "en", { ignorePunctuation: true })); // 0 (문장부호 무시)
  console.log("a.b".localeCompare("ab", "en", { ignorePunctuation: false })); // -1 (문장부호 비교)
  ```

### 활용 예시 : 문자열 정렬
* 사전순 정렬
  ```js
  const fruits = ["apple", "orange", "banana", "grape"];
  fruits.sort((a,b) => a.localeCompare(b));
  console.log(fruits); // ["apple", "banana", "grape", "orange"]
  ```

* 지역별 정렬
  ```js
  const words = ["résumé", "resume", "resumé"];
  words.sort((a, b) => a.localeCompare(b, "fr", {sensitivity: "base"}));
  console.log(words); // ["resume", "resumé", "résumé"]
  ```

### 주의사항
* 브라우저별 구현 차이: 기본 동작은 브라우저나 운영 체제에 따라 다를 수 있다. 특정 지역 설정을 지정하는 것이 더 일관된 결과를 제공한다.
* 비교 성능: `localeCompare()`는 언어별 정렬 규칙을 적용하기 때문에 단순한 ASCII 비교보다 더 많은 리소스를 소모한다. 성능이 중요한 경우 ASCII 비교 (`<`, `>`)를 사용하는 것이 유리할 수 있다.

### 결론
-> `localeCompare()`는 다양한 언어와 지역을 지원하는 정렬과 비교를 구현하는 데 매우 유용한 메서드이다. 특히 다국어 애플리케이션을 개발할 때 큰 도움이 된다.
