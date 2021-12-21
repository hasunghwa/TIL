# Java Script
## 2. 데이터 타입

### 변수
> immutable(변경x): premitive types, frozen objects(i.e. object.freeze())
mutable: all objects by default are mutable in JS

1. let(mutable)
    ```jsx
    let name = 'sunghwa';
    ```
2. var
    ```jsx
    {
      var name = 'sunghwa';
    }
    console.log(name); // 가능
    ```
    - 선언하기전에 값 사용가능(var hoisting 젤위로 선언을 끌어 올려 줌)
    - 블록 무시

### 상수
1. constant(immutable) -> read only
    ```jsx
      const days
    ```
    - const(보안, 안전한 스레드, 실수를 줄임)

### 변수형

#### 1. primitive: number, string, boolean, null, undefined, symbol
- number
  ```jsx
    const count = 26 // number
    const size = 26.5 // number
    const infinity = 1 / 0; // Infinity
    const negativeInfinity = -1 / 0; // -Infinity
    const nAn = 'not a number' / 2; // NaN
    const bigInt = 123456789012345678901234567890n // bigInt
  ```
- string
  ```jsx
    const char = 'c';
    const str = 'world';
    const greeting = 'hello' + str;
    const helloWorld = `hello ${str}!`; // template literals
  ```
- boolean
  > false: 0, null, undefined, NaN, ''
true: 나머지

  ```jsx
    const canClick = true;
    const test = 3 < 1; // false
  ```
- null vs undefined
  ```jsx
    let nothing = null; // 텅텅빈 값(null로 할당)
    let x; // 선언은 했지만 값이 없음
  ```
- symbol
  > 고유 식별자 필요시 사용  

  ```jsx
    // 주어진 String에 상관없이 고유한 식별자만듦
    const symbol1 = Symbol('id');
    const symbol2 = Symbol('id');
    console.log(symbol1 === symbol2); // false
    // 주어진 String에 맞는 심볼 생성
    const pSymbol1 = Symbol.for('id');
    const pSymbol2 = Symbol.for('id');
    console.log(pSymbol1 === pSymbol2); // true
    // description을 통해 String으로 변환하여 출력해야
    console.log(`${symbol1.description}`)
  ```
- Dynamic typing
  ```jsx
    let text = 'hello'; // String
    text.charAt(0) // h
    text = 1; // number
    text = '7' + 5; // String(75)
    text = '8' / '2'; // Number(4)
    text.charAt(0) // error
  ```
#### 2. object, box container
- object (object를 가리키는 reference가 저장)
  ```jsx
    const sunghwa = { name: 'sunghwa', age: '25'};
    sungwha.age = 23; // .을 통해 접근
  ```
#### 3. function, first-class function
- 변수에 할당됨
- 함수의 파라매터로 전달됨
- 리턴값으로도 전달됨
##### 함수 선언, 표현
```jsx
print() // 가능 -> 함수 선언 hoisting
function print(){ // 함수 선언
  console.log('print');
}

print1(); // error hoisting(x)
const print1 = function() { // 함수 표현, anonymous function(이름없는 함수)
  console.log('print');
}
print1();
const printAgain = print1;
printAgain();
```
##### callback(함수를 매개변수로 전달하여 함수호출)
```jsx
function randomQuiz(answer, printYes, printNo){
  if (answer === 'love you'){
    printYes();
  } else {
    printNo();
  }
}
```
##### arrow function
```jsx
const add = function (a, b) { // expression
  return a + b;
};
// 위 코드와 동일하게 동작
const add = (a, b) => a + b; // arrow
const simpleMultiply = (a, b) => { return a * b; };
```

##### IIFE(선언과 동시에 호출)

```jsx
(function hello() {
	console.log('IIFE');
})();
```
