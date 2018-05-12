# assert

## assert 모듈이 지원하는 함수 목록 (node REPL 에서 실행, ctrl+D: exit)
```
$node
> require('assert')
{ [Function: ok]
  fail: [Function: fail],
  AssertionError: [Function: AssertionError],
  ok: [Circular],
  equal: [Function: equal],
  notEqual: [Function: notEqual],
  deepEqual: [Function: deepEqual],
  deepStrictEqual: [Function: deepStrictEqual],
  notDeepEqual: [Function: notDeepEqual],
  notDeepStrictEqual: [Function: notDeepStrictEqual],
  strictEqual: [Function: strictEqual],
  notStrictEqual: [Function: notStrictEqual],
  throws: [Function: throws],
  doesNotThrow: [Function: doesNotThrow],
  ifError: [Function: ifError] }
```
## 기본예제
```
assert.equal(1,2) // 1, 2는 다르므로 에러
AssertionError [ERR_ASSERTION]: 1 == 2

assert.ok(0) // 0은 Falsy 하므로 에러
AssertionError [ERR_ASSERTION]: 0 == true
```

## 심화예제
```
mkdir assert

cd assert

vi file.txt
[i] // 아래 text 입력
one
two
three
[esc -> :wq] // 저장 후 닫기

vi test.js
[i] // 아래 text 입력

  1 var assert = require('assert')
  2 var fs = require('fs')
  3
  4 assert.equal(1+2) // 오류 발생 예상 지점1
  5 countLines(function (err, n) {
  6   assert.ifError(err)
  7   assert.equal(n, 3) // 오류 발생 예상 지점2
  8 })
  9
 10 function countLines (cb) {
 11   fs.readFile('file.txt', 'utf8',  function (err, src) {
 12     if (err) cb(err)
 13     else cb(null, src.split('\n').length+100) // // 오류 발생 예상 지점3
 14   })
 15 }

[esc -> :wq] // 저장 후 닫기
```

## 심화예제 - 실행
(본 예제에서는 실패하는 코드를 의도적으로 숨겨놓음으로서 테스트 실패와 성공 시의 차이점을 알아본다.)
```
$node test.js
assert.js:42
  throw new errors.AssertionError({
  ^

AssertionError [ERR_ASSERTION]: 3 == undefined
```

### 첫 번째 오류 발생

```
4 assert.equal(1+2) // equal에 두 번째 파라미터가 지정되지 않아 발생.
4 assert.equal(1+2, 3) // 다음과 같이 수정 후 다시 실행
```

### 두 번째 오류 발생
```
assert.js:42
  throw new errors.AssertionError({
  ^

AssertionError [ERR_ASSERTION]: 104 == 3
```

### 오류 발생 지점
```
  5 countLines(function (err, n) {
  6   assert.ifError(err)
  7   assert.equal(n, 3) <-- 오류 발생 지점.
  8 })
  ..

  else cb(null, src.split('\n').length+100) // 의도적으로 100을 더하였기 때문. + 100을 없애고 다시 실행해보자.
```

### 세 번째 오류 발생
```
assert.js:42
  throw new errors.AssertionError({
  ^

AssertionError [ERR_ASSERTION]: 4 == 3
```

### 오류 발생 지점
```
$node
> require('fs').readFileSync('file.txt', 'utf8')
'one\ntwo\nthree\n'

// 문서 끝에 빈문자열을 제거한다.
13     else cb(null, src.trim().split('\n').length)
```

### 수정 후 다시 실행
테스트 성공. 하지만 아무런 메세지가 없다.

```
$node test.js
$$echo $? // exit code. 0일 경우 성공. 1일 경우 실패
0
```

## assert의 문제점
- exception 이 발생할 경우 실행을 멈춤. (13번째 줄 제거 후 성공으로 처리되는 문제)
- 테스트 블록이 실행되지 않을 경우에도 성공한 것처럼 보여짐.





