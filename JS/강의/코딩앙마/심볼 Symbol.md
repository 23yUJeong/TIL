# 심볼 Symbol

# Symbol : 유일성 보장

# 유일한 식별자

```jsx
const id = Symbol("id");
const id2 = Symbol("id");

console.log(id); // Symbol(id)
console.log(id2); // Symbol(id)
console.log(id == id2); // false
```

# property key : 심볼형

```jsx
const id = Symbol("id");

const user = {
  name: "Mike",
  age: 30,
  [id]: "myId",
};

console.log(user); // {name: 'Mike', age: 30, Symbol(id): 'myId'}
console.log(user[id]); // "myId"
```

# But

```jsx
console.log(Object.keys(user)); // ['name', 'age']
console.log(Object.values(user)); // ['Mike', 30]
console.log(Object.entries(user)); // [['name', 'Mike'], ['age', 30]]

for (key in arr) {
  console.log(key, arr[key]); // ['name', 'Mike'] // ['age', 30]
}
```

- Object.keys, values, entries 키가 Symbol형인 프로퍼티는 건너뜀
- 마찬가지로 for … in문도 건너뜀

# 어떻게 활용함?

특정 객체에 원본 데이터를 건드리지 않고 속성을 추가할 수 있음

```jsx
const student = {
  name: "Mike",
  age: 18,
};
const id = Symbol("J");
student[id] = id;

for (key in student) {
  console.log(key, student[key]); // "name" "Mike" // "age" 18
}
```

# 2. Symbol.for() : 전역 심볼

- 하나의 심볼만 보장받을 수 있음 / 없으면 만들고, 있으면 가져오기 때문임
- Symbol 함수는 매번 다른 Symbol 값을 생성하지만,
- Symbol.for은 메소드 하나를 생성한 뒤 키를 통해 같은 Symbol을 공유

```jsx
const id1 = Symbol.for("id");
const id2 = Symbol.for("id");

console.log(id1 == id2); // true
```

## 2-1. 할당값을 알고 싶다면? Symbol.keyFor()

```jsx
const id1 = Symbol.for("id");
const id2 = Symbol.for("id");

console.log(Symbol.keyFor(id1)); // "id"
// Symbol.keyFor({변수 이름}); // "{할당값}"
```

## 2-2. 전역 심볼이 아니라면? {변수 이름}.description

```jsx
const id = Symbol("id입니다.");
console.log(id.description); // "id입니다."
```

# 숨겨진 Symbol key 보는 방법

---

## 1. Object.getOwnPropertySymbols

- Symbol key만 보는 방법

```jsx
const id = Symbol("id");

const user = {
  name: "Mike",
  age: 30,
  [id]: "myId",
};

console.log(Object.getOwnPropertySymbols(user)); // [Symbol(id)];
```

## 2. Reflect.ownKeys({객체 이름})

- Symbol key를 포함한 객체의 모든 키를 보여줌

```jsx
const id = Symbol("id");

const user = {
  name: "Mike",
  age: 30,
  [id]: "myId",
};

console.log(Reflect.ownKeys(user)); // ['name', 'age', Symbol(id)]
```

# 몰랐던 사실?!

```jsx
const user = {
  name: "Mike",
  age: 30,
  sayHello() {
    console.log(`Hi ${this.name}.`);
  },
};

const showName = Symbol("showName");
user[showName] = function () {
  console.log(this.name);
};

user[showName](); // "Mike"
// user.showName()으로 쓰면 오류 발생
user.sayHello(); // "Hi Mike."
// user[sayHello]()으로 쓰면 오류 발생
```
