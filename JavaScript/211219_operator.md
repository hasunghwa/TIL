# Java Script
## 3. 연산자(Operator)
### 문자열 연산
```jsx
let str = 'my' + 'cat'; // my cat
let str2 = '1' + 2; // 12
let str3 = `string literals: 1 + 2 = ${1 + 2}`; // 1 + 2 = 3
```
### 숫자 연산
```jsx
let a = 1 + 1; // add 2
let b = 1 - 1; // sub 0
let c = 1 / 1; // div 1
let d = 1 * 1; // mul 1
let e = 5 % 2; // mod 1
let f = 2 ** 3; // exponentiation 8
```
### 증감 연산자
```jsx
let counter = 2;
const preIncrement = ++counter; // 전위
const preDecrement = --counter;
const postIncrement = counter++; // 후위
const postDecrement = counter--;
```
### 할당 연산자
```jsx
let x = 2;
let y = 5;
x += y; // x = x + y;
x -= y;
x *= y;
x /= y;
```
### 비교 연산자
```jsx
10 < 6 // false
10 <= 6 // false
10 > 6 // true
10 >= 6 // true
```
### 논리 연산자
- || (OR)
```jsx
if(value1 || value2 || check())
```
>or에서 첫 번째 값이 true이면 뒤에있는 값 상관없이 true이므로 뒤에 값이나 함수 계산할 필요없다.
그래서 계산이 필요한 함수는 뒤쪽으로 두는 것이 좋음

- && (AND)
```jsx
if(value1 && value2 && check())
```
> and도 첫 번재 값이 false이면 전체구문이 false이므로 계산이 필요한 함수 뒤쪽에

- nullableObject
```jsx
if(nullobject != nulll){
	nullobject.something;
}
```
- ! (NOT)
```jsx
const value = true;
!value // false;
```
### 등위 연산자
- == vs ===
>=== strict equality(**타입을 신경씀**), no type conversion

```jsx
const strFive = '5';
const numFive = 5;
strFive == numFive; // true
strFive != numFive; // fasle
strFive === numFive; // false
strFive !== numFive; // true
```
- object
```jsx
const sunghwa1 = { name: 'sunghwa' };
const sunghwa2 = { name: 'sunghwa' };
const sunghwa3 = sunghwa1;
sunghwa1 == sunghwa2; //  false
sunghwa1 === sunghwa2; // false
sunghwa1 === sunghwa3; // true
```
- 문제
```jsx
0 == false; // true 0은 false이다
0 === false; // false 0은 number false는 boolean
'' == false; // true ``은 false이다
'' === false; // false ``은 string false는 boolean
null == undefined; // true null은 undefined이다
null === undefined; // false null은 object
```
## 4. 조건문
### if
```jsx
const name = 'kildong';
if (name === 'sunghwa'){ // 이름이 sunghwa면
  console.log(`hello ${name}`);
} else if(name === 'kildong'){ // 이름이 kildong이면
  console.log(`where r u {name}`);
} else { // sunghwa, kildong 둘다 아니면
  console.log('unkwnon');
}
```
### 삼항 연산자
```jsx
// 이름이 성화가 맞으면 yes 아니면 no
name === 'sunghwa' ? 'yes' : 'no';
```
### switch
```jsx
const char = 'A';
switch (char) {
  case 'A': // char이 A일 때
    console.log('A');
    break;
  case 'B':
  case 'b': // case 겹쳐서 사용 가능
    console.log('B');
    break;
  default: // 해당하는 case가 없을 때
    console.log('unknown');
    break;
}
```
## 5. 반복문
### while
> while구문 참일때 실행

```jsx
let i = 3;
while (i > 0) {
  console.log(i); // 3 -> 2 -> 1
  i--;
}
```
### do while
> do구문 실행 후 참 확인

```jsx
do {
  console.log(i); 3 -> 2 -> 1 -> 0
  i--;
} while (i > 0);
```
### for
> for( 시작; 종료; 스탭 )

```jsx
for (let i = 3; i > 0; i--) { // 3부터 시작해서 1씩감소 i가 0보다 작거나 같으면 종료
  console.log(i); 3 -> 2 -> 1
}

// 2중 for문
for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    console.log(i, j); // 0 0 -> 0 1 -> ... 2 2
  }
}
```
### break, continue
> 반복문 종료 break, 구문 실행하지 않고 다음 루프로 continue

```jsx
for (let i = 0; i <= 5; i++) {
  if ( i === 4 ) // i가 4일때 종료
    break;
  else if ( i === 2) // i가 2일때 3으로
    continue;
  console.log(i); 0 -> 1 -> 3
}
```
