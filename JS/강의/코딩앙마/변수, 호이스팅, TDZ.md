# 변수, 호이스팅, TDZ

# 호이스팅

스코프 내부 어디서든 변수 선언은 최상위에 선언된 것처럼 행동

# TDZ Temporal Dead Zone

---

## var : 함수 스코프 (function-scoped)

유일하게 벗어날 수 없는 스코프는 함수

```jsx
function add(num1, num2) {
  var result = num1 + num2;
}

add(2, 3);

cosole.log(result); // 오류 발생
```

## let, const : 블록 스코프 (block-scoped)

- 블록?
  함수, if 문, for 문, while 문, try/catch 문 등
