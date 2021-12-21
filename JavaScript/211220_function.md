# Java Script
## 5. 함수
> 하나의 함수 하나의 일, 함수 이름은 동사로
function is object

```jsx
function name(param1, param2) { body ... return; }
```
default parameters 매개변수에 디폴트값을 설정할 수 있다.

```jsx
function showMessage(message, from = 'unknown'){
  console.log(`${message} by ${from}`);
}
```

rest parameters (...args 배열)

```jsx
function printAll(...args){
  for(let i = 0; i< args.length; i++)
    console.log(args[i]);

  for(const arg of args)
    console.log(arg);

  args.forEach((arg) => console.log(arg));
}
printAll('A', 'B', 'C');
```

early return, early exit(블록안에서 코드 많이 작성하면 가독성 떨어짐→ 조건이 맞지 않으면 함수 종료)

```jsx
function upgradeUser(user){
  if(user.point > 10){
  }

  if(user.point <= 10){
    return;
  }
}
```

## 6. 클래스
### class
```jsx
class Person{
  constructor(name, age){ // 생성자
    this.name = name;
    this.age = age;
  }
  speak(){
    console.log(`${this.name}: hello!`); // 메소드
  }
}

const sunghwa = new Person('sunghwa', '25');
sunghwa.speak();
```
### getter and setters
> 입력값의 오류를 사전에 막기위함

```jsx
class User{
  constructor(firstName, lastName, age){
    this.firstName = firstName;
    this.lastName = lastName;
    this.age = age;
  }

  get age(){
    return this._age;
  }

  set age(value){
    this._age = value < 0 ? 0: value; // value가 음수면 0으로
  }
}
```

get과 set을 선언하는 순간 this는 get을 =는 set을 호출하게 된다
그렇기 때문에 set에서 this.age = value를 사용하면 set함수를 무한호출하게 됨 _age를 사용하여 예방
### Static
>object에 생관없이 class에서 사용하기위해

```jsx
class Speaker {
  static str = 'Hello World';
  constructor(number) {
    this.number = number;
  }

  static printHello() {
    console.log(Speaker.str);
  }
}

const speak1 = new Speaker(1);
const speak2 = new Speaker(2);
console.log(speak1.str); // object에 없음
console.log(Speaker.str); // static은 클래스자체에 있음
Speaker.printHello();
```
### 상속, 다형성

```jsx
class Shape {
  constructor(width, height, color){
    this.width = width;
    this.height = height;
    this.color = color;
  }

  draw(){
    console.log(`drawing ${this.color} color of`);
  }

  getArea(){
    return this.width * this.height;
  }
}

class Rectangle extends Shape{}
class Triangle extends Shape{
	draw(){
		super.draw();
		console.log('🔺');
	}
	getArea(){
		return (this.width * this.height) / 2;
	}
}

const rectangle = new Rectangle(20, 20, 'blue');
rectangle.draw();
console.log(rectangle.getArea()); // 400
const triangle = new Triangle(20, 20, 'blue'); // 200
triangle.draw();
console.log(triangle.getArea());
```

### instanceof
> 왼쪽의 object가 오른쪽 class 인스턴스인지 확인(true, false)
```jsx
rectangle instanceof Rectangle; // true
triangle instanceof Rectangle; // false
triangle instanceof Triangle; // true
triangle instanceof Shape; // true
triangle instanceof Object; // true
```
## 7. object
> object = { key : value };

```jsx
const obj1 = {}; // 'object literal'
const obj2 = new Object(); // 'object constructor'

const sunghwa = { name: 'sunghwa', age: 4 };
sunghwa.hasJob = true; // 추가, 코딩하는 순간 key에 해당하는 값 받아오고 싶을 때
sunghwa['hasJob'] = true; // 추가, 어떤 key가 필요한지 모를 때 -> 런타임에서 결정될때
delete sunghwa.hasJob; // 삭제

function printValue(obj, key) {
  console.log(obj.key); // error
  console.log(obj[key]);
}
```
### constructor function
```jsx
const person1 = { name: 'bob', age: 2 };
const person2 = { name: 'steve', age: 3 };
const person3 = new Person('sunghwa', 25);
function Person(name, age) { // constructor function
  this.name = name;
  this.age = age;
}
```
### in
> key가 object안에 있는지 확인

```jsx
'name' in sunghwa;
'age' in sunghwa;
'phone' in sunghwa;
```
### for
```jsx
for (let key in sunghwa) {
  console.log(sunghwa[key]);
}

```
### for of
```jsx
const array = [1, 2, 3, 4];
for (let value of array){
  console.log(value);
}
```
### cloning
```jsx
const user = { name: 'sunghwa', age: '20' };
const user2 = Object.assign({}, user);

const fruit1 = { color: 'red' };
const fruit1 = { color: 'blue', size: 'big' };
const mixed = Object.assign({}, fruit1, fruit2); // color: 'blue', size:'big'
```
