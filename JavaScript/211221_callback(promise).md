# Java Script
## 10-1. callback
### 동기 비동기
> 동기: 정해진 순서에 맞게 코드 실행
비동기: 언제 코드가 실행될지 예측할 수 없음

```jsx
// 비동기 1 -> 3 -> 2
console.log('1');
setTimeout(() => console.log('2'), 1000);
console.log('3');

// 동기 콜백 (즉각적으로 호출)
function printImmediately(print){
  print();
}
printImmediately(() => console.log('hello'))

// 비동기 콜백 (언제호출할지 모름)
function printWithDelay(print, timeout){
  setTimeout(print, timeout);
}
printWithDelay(() => console.log('async callback'), 2000);
```
### 콜백 지옥
```jsx
class UserInfo{
  loginUser(id, password, onSuccess, onError) { // 로그인
    setTimeout(()=> {
      if (id === 'sunghwa' && password === 'ha') {
        onSuccess(id);
      } else {
        onError(new Error('not found'));
      }
    },2000);
  }

  getRoles(user, onSuccess, onError) { // 사용자 역할 얻기
    setTimeout(() => {
      if (user === 'sunghwa') {
        onSuccess({name: 'sunghwa', role: 'admin'});
      } else {
        onError(new onError('no access'));
      }
    }, 1000);
  }
}

const userInfo = new UserInfo();
const id = prompt('enter your id');
const password = prompt('enter your password');
userInfo.loginUser(
  id,
  password,
  user => {
    userInfo.getRoles(
      user,
      userWithRole => {
        alert(`Hello ${userWithRole.anme}, you have a ${userWithRole.role}`);
      },
      error => console.log(error);
    );
  },
  error => console.log(error)
);
```
## 10-2. promise
>state: pending(수행중) -> fullfilled(완료) or rejected(오류)
producer vs consumer

### 1. producer
```jsx
// promise 생성 시 자동 실행
const promise = new Promise((resolve, reject) =>{
  console.log('doing something...');
  setTimeout(() => {
    //resolve('sunghwa');
    reject(new Error('no network'))
  }, 2000);
});
```
Promise를 등록하여 함수가 성공적으로 동작하면 resolve를 그렇지 않다면 rejct를 콜백
### 2. Consumers: then, catch, finally
```jsx
promise
  .then((value) => { // Promise 성공
    console.log(value);
  })
  .catch((error) => { // Promise 실패
    console.log(error);
  })
  .finally(() => { // Promise 마지막에 무조건 실행
    console.log('finally')
  });
```
promise에서 resolve를 전달 받았다면 then, reject를 전달 받았다면 catch를 통해 작업 수행
### 3. chaining
```jsx
const fetchNumber = new Promise((resolve, reject) =>{
  setTimeout(() => resolve(1), 1000);
});

fetchNumber
  .then(num => num * 2) // 1*2= 2
  .then(num => num * 3) // 2*3= 6
  .then(num => {
    return new Promise((resolve, reject) => {
      setTimeout(() => resolve(num - 1), 1000); // 6-1= 5
    });
  })
  .then(num => console.log(num));
```
then에서 값을 전달해도 되고 또 다른 promise를 전달해도 된다.
### 4. error handling
```jsx
const getHen = () =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve('🐓'), 1000);
  });
const getEgg = hen =>
  new Promise((resolve, reject) => {
    setTimeout(() => reject(new Error(`error! ${hen} => 🥚`)), 1000);
  });
const cook = egg =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve(`${egg} => 🍰`), 1000);
  });

getHen()
  .then(hen => getEgg(hen))
  .catch(error => { // 계란을 받아올 때 문제가 생기면
    return '🥪';
  })
  .then(egg => cook(egg))
  .then(meal => console.log(meal));
```

### 5. 콜백지옥 → promise
```jsx
class UserInfo{
  loginUser(id, password) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        if(id === 'sunghwa' && password === 'ha')
          resolve(id)
        else
          reject(new Error('not found'));
      }, 2000);
    });

  }
  getRoles(user) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        if(user === 'sunghwa')
          resolve({name: 'sunghwa', role: 'admin'});
        else
          reject(new onError('no access'));
      }, 1000);
    });
  }
}

const userInfo = new UserInfo();
const id = prompt('enter your id');
const password = prompt('enter your password');

userInfo
  .loginUser(id, password)
  .then(userInfo.getRoles)
  .then(user => alert(`${user.name}, ${user.role}`))
  .catch(console.log)
```
## 10-3. async await
### 1. async
```jsx
function fetchUser(){
 return new Promise((resolve, reject) =>{
   return resolve('ellie');
 });
}
```
위아래 같은 동작
```jsx
async function fetchUser(){ // promise로 만들어줌
  return 'ellie';
}
```
```jsx
const user = fetchUser();
user.then(console.log);
console.log(user);
```
### 2. await
```jsx
function delay(ms){
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function getPizza(){
  await delay(1000); // 기다림
  return '🍕';
}

// async로 만든 getHamburger
async function getHamburger(){
  await delay(1000);
  throw 'error'; // 에러 발생시
  return '🍔';
}

// promise로 만든 getHamburger
function getHamburger(){
  return delay(1000).then(()=> '🍔');
}

// promise로 만든 pickFoods
function pickFoods(){
  return getPizza()
  .then(Pizza => {
    return getHamburger()
    .then(Hamburger => `${Pizza} + ${Hamburger}`);
  });
}

// async로 만든 pickFoods
async function pickFruits(){
  const apple = await getApple(); // 미리 받아옴
  const banana = await getBanana();
  return `${apple} + ${banana}`;
}
```
### 3. promise apis
> 병렬 promise

##### .all (promise 배열 전달하여 모두 받아옴)
```jsx
function pickAllFruits(){
  return Promise.all([getApple(), getBanana()]) // 모든 프로미스 병렬처리
    .then(fruits => fruits.join(' + '));
}
pickAllFruits().then(console.log);
```
##### .race (promise 배열 전달하여 가장먼저 값을 리턴하는 하나만 받아옴)
```jsx
function pickOnlyOne(){
  return Promise.race([getApple(), getBanana()]); // 가장먼저 리턴하는 하나만
}
pickOnlyOne().then(console.log);
```
