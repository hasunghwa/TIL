# React

## State 활용

## 1. 선언

```jsx
function MinutesToHours() {
  const [amount, setAmount] = React.useState("");
  const [flipped, setFlipped] = React.useState(false);
}
```

Functional Component에서 state는 useState를 사용하여 선언할 수 있다.  
useState는 선언하는 값과 그 값을 바꾸는 함수를 리턴한다.

## 2. 변경

```jsx
const onChange = (event) => {
  setAmount(event.target.value);
};

<input
  value={amount}
  id="minutes"
  placeholder="Minutes"
  type="number"
  onChange={onChange}
  disabled={flipped}
/>;
```

웹에서 입력받은 input값을 state로 넘겨주기 위해선 onChange함수를 사용하여 input태그안의 변경이 일어났을 때 변경된 값을 넘겨받아 setAmount함수를 통해 state를 변경 해야한다.  
→ 그렇게하지 않으면 페이지 렌더링이 이루어지지 않아 변경된 값이 화면에 표시되지 않음.

## 3. Memo

```jsx
function Btn({ text, onClick }){
  return <button onClick={onClick}>{text}</button>
}
const MemoBtn = memo(Btn)
function App() {
  const [value, setValue] = useState("one");
  const ChangeValue = () => setValue("two");
  return (
    <MemoBtn text={value} onClick={ChangeValue}/>
    <MemoBtn text="two" />
  );
}
```

부모 state 변경시 모든 자식컴포넌트 re-rander → 성능이슈  
memo를 사용하면 변경된 자식에 대해서만 re-rander

## 4. Effects, Cleanup

useEffect 라는 Hook 을 사용하여 컴포넌트 생성, 삭제, 업데이트 될 때 특정 작업을 처리할 수 있다.

```jsx
function Hello() {
  useEffect(() => {
    console.log("컴포넌트가 화면에 나타남");
    return () => {
      console.log("컴포넌트가 화면에서 사라짐");
    };
  }, []);
  return <h1>hello, </h1>;
}
```

Hello컴포넌트가 생성되면 useEffect에 등록된 함수가 실행된다.  
useEffect에서는 함수를 반환 할 수 있는데 이를 Clenup함수라고 칭한다.  
Hello 컴포넌트가 삭제되면 Clenup함수가 실행된다.

```jsx
useEffect(() => {
  console.log("user 값이 설정됨");
  console.log(user);
  return () => {
    console.log("user 가 바뀌기 전..");
    console.log(user);
  };
}, [user]);
```

useEffect의 두번째 인자 deps 에 특정 값을 넣게되면, 컴포넌트가 처음 마운트 될 때, 지정한 값이 바뀔 때 useEffect 실행
