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
