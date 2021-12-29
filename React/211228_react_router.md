# React

## 1. Router

리액트 라우터는 여러 페이지들을 연결시켜준다. 리액트 자체에서 지원하지 않기 때문에 설치가 필요하다.

```cmd
//install
npm i react-router-dom@5.3.0
```

BrowserRouter, HashRouter 2가지 방법을 활용해 라우팅
BrowserRouter: 페이지 자체를 이동
HashRouter: #을 포함시키고 해당 정보에 접근

```jsx
import { BrowserRouter as Router } from "react-router-dom";
function App() {
  return (
    <Router>
      <MainPage />
      <SubPage />
    </Router>
  );
}
```

## 2. Route

Route는 페이지 하나를 통제하며 path, exact, component, render를 다룰 수 있다.

- path: 이동할 경로
- exact: path가 정확하게 일치할 때만 이동 (default = true)
- component: 어떤 페이지인지(컴포넌트 이름)
- render: 커스터마이징이 가능한 함수

```jsx
import { BrowserRouter as Router, Route } from "react-router-dom";
function App() {
  return (
    <Router>
      <Route path="/" component={EnterPage} />
      <Route path="/main" component={MainPage} />
      <Route path="/sub" component={SubPage} />
    </Router>
  );
}
```

## 3.Switch

Switch는 라우트들을 묶어서 선택된 라우트 첫 번째 하나만을 렌더링 하게끔 도와준다.
스위치를 사용하지 않고 /main에 접속하면 EnterPage와 MainPage모두 렌더링 된다.
EnterPage와 MainPage 모두 /를 포함하고 있기 때문이다.
Switch를 사용하면 이를 해결할 수 있다. Switch를 사용하면 제일 상단의 첫 번째 라우트가 랜더링 되기 때문에 EnterPage가 랭더링 된다.

```jsx
import { BrowserRouter as Router, Route, Switch } from "react-router-dom";
function App() {
  return (
    <Router>
      <Switch>
        <Route path="/" component={EnterPage} />
        <Route path="/main" component={MainPage} />
        <Route path="/sub" component={SubPage} />
      <Switch>
    </Router>
  );
}
```

## 4. Link

링크는 a태그와 비슷하지만 a태그는 페이지 이동시 전체 페이지가 재실행되지만 Link를 사용하면 페이지 새로고침 없이 다른 페이지로 이동할 수 있게 해준다.

```jsx
<a href="/home">Home</a>
<Link to ="/home">Home</Link>
```

페이지 전체 재실행
새로고침 없이 유저를 다른 페이지로 이동
