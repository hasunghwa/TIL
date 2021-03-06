# React

## 1. useIndex

> useState를 사용하여 input의 value설정  
>  validator를 통해 수정여부를 결정할 수 있다.

```jsx
const useInput = (initialValue, validator) => {
  const [value, setValue] = useState(initialValue);
  const onChange = (e) => {
    let willUpdate = true;
    if (typeof validator === "function") {
      willUpdate = validator(e.target.value);
    }
    if (willUpdate) {
      setValue(e.target.value);
    }
  };

  return { value, onChange };
};

export default function App() {
  const validator = (value) => !value.includes("@");
  const name = useInput("", validator);
  return (
    <div className="App">
      <h1>Hello</h1>
      <input placeholder="Name" {...name} />
      <!-- 위와 동일한 코드
      <input placeholder="Name" value={name.value} cnChange={name.onChange} />
      -->
    </div>
  );
}
```

## 2.useClick

> useRef를 사용하여 element를 선택하고 해당 element에 clickevent 설정

```jsx
const useClick = (onClick) => {
  if (typeof onClick !== "function") {
    return;
  }
  const element = useRef();
  useEffect(() => {
    if (element.current) {
      element.current.addEventListener("click", onClick);
    }
    return () => {
      if (element.current) {
        element.current.removeEventListener("click", onClick);
      }
    };
  }, []);

  return element;
};

export default function App() {
  const onClick = () => console.log("say hello");
  const title = useClick(onClick);
  return (
    <div className="App">
      <h1 ref={title}>Hello</h1>
    </div>
  );
}
```

## 3.useConfirm

> confirm()을 활용하여 사용자의 행동에대한 확인및 취소를 응답받음

```jsx
const useConfirm = (message = "", callback, reject) => {
  if (!callback || typeof callback !== "function") {
    return;
  }
  if (reject && typeof reject !== "function") {
    return;
  }
  const confirmAction = () => {
    if (confirm(message)) {
      callback();
    } else {
      reject();
    }
  };
  return confirmAction;
};

export default function App() {
  const deleteWorld = () => console.log("delete");
  const rejectProposal = () => console.log("no delete");
  const confirmDelete = useConfirm("r u sure?", deleteWorld, rejectProposal);
  return (
    <div className="App">
      <button onClick={confirmDelete}>Delete the world</button>
    </div>
  );
}
```

## 5.usePreventLeave

> beforeunload이벤트를 등록하여 사용자가 페이지를 떠날 때 정말 떠날 것인지 확인한다.

```jsx
const usePreventLeave = () => {
  const listener = (event) => {
    event.preventDefault();
    event.returnValue = "";
  };
  const prevent = () => {
    window.addEventListener("beforeunload", listener);
  };
  const unprevent = () => {
    window.removeEventListener("beforeunload", listener);
  };
  return { prevent, unprevent };
};

export default function App() {
  const { prevent, unprevent } = usePreventLeave();
  return (
    <div className="App">
      <button onClick={prevent}>prevent</button>
      <button onClick={unprevent}>unprevent</button>
    </div>
  );
}
```

## 6.useBeforeLeave

> mouseleave이벤트를 활용하여 마우스의 y좌표가 0보다 작거나 같으면 전달받은 함수 실행

```jsx
const useBeforeLeave = (onBefore) => {
  if (typeof onBefore !== "function") {
    return;
  }
  const handle = (event) => {
    const { clientY } = event;
    if (clientY <= 0) {
      onBefore();
    }
  };
  useEffect(() => {
    document.addEventListener("mouseleave", handle);
    return () => document.removeEventListener("mouseleave", handle);
  }, []);
};
export default function App() {
  const leave = () => console.log("dont leave");
  useBeforeLeave(leave);
  return <div className="App"></div>;
}
```

## 7.useFadeIn

> useRef를 활용하여 element의 animation 설정

```jsx
const useFadeIn = (duration = 1, delay) => {
  const element = useRef();
  useEffect(() => {
    if (element.current) {
      const { current } = element;
      current.style.transition = `opacity ${duration}s ease-in-out ${delay}s`;
      current.style.opacity = 1;
    }
  });
  return { ref: element, style: { opacity: 0 } };
};

export default function App() {
  const hanimation = useFadeIn(2, 2);
  const panimation = useFadeIn(3, 1);
  return (
    <div className="App">
      <h1 {...hanimation}>Hello</h1>
      <p {...panimation}>Hello</p>
    </div>
  );
}
```

## 8.useNetwork

> online일때와 offline일때 이벤트를 등록하여 on/offline제어

```jsx
const useNetwork = (onChange) => {
  const [status, setStatus] = useState(navigator.onLine);
  const handleChange = () => {
    if (typeof onChange === "function") {
      onChange(navigator.onLine);
    }
    setStatus(navigator.onLine);
  };
  useEffect(() => {
    window.addEventListener("online", handleChange);
    window.addEventListener("offline", handleChange);
    return () => {
      window.removeEventListener("online", handleChange);
      window.removeEventListener("offline", handleChange);
    };
  }, []);
  return status;
};

export default function App() {
  const hanleNChange = (online) => {
    console.log(online ? "online" : "offline");
  };
  const onLine = useNetwork(hanleNChange);
  return (
    <div className="App">
      <h1>{onLine ? "on" : "off"}</h1>
    </div>
  );
}
```

## 9.useScroll

> scroll이벤트를 활용하여 사용자의 스크롤 값에따른 이벤트 제어

```jsx
const useScroll = () => {
  const [state, setState] = useState({ x: 0, y: 0 });
  const onScroll = () => {
    setState({ x: window.scrollX, y: window.scrollY });
  };
  useEffect(() => {
    window.addEventListener("scroll", onScroll);
    return () => window.removeEventListener("scroll", onScroll);
  }, []);
  return state;
};

export default function App() {
  const state = useScroll();
  return (
    <div className="App" style={{ height: "1000vh", width: "1000vw" }}>
      <h1 style={{ position: "fixed", color: state.y > 100 ? "red" : "blue" }}>
        hi
      </h1>
    </div>
  );
}
```

## 10.useFullscreen

> useRef를 통해 element를 가져오고 requestFullscreen를 통해 element를 전체화면으로 설정

```jsx
const useFullscreen = (callback) => {
  const element = useRef();
  if (callback && typeof callback !== "function") {
    return;
  }
  const triggerFull = () => {
    if (element.current) {
      element.current.requestFullscreen();
      callback(true);
    }
  };
  const exitFull = () => {
    document.exitFullscreen();
    callback(false);
  };
  return { element, triggerFull, exitFull };
};

export default function App() {
  const onFullS = (isFull) => {
    console.log(isFull ? "full" : "small");
  };
  const { element, triggerFull, exitFull } = useFullscreen(onFullS);
  return (
    <div className="App">
      <div ref={element}>
        <img src="https://i.ibb.co/R6RwNxx/grape.jpg" />
        <button onClick={exitFull}>exit full screen</button>
      </div>
      <button onClick={triggerFull}>full screen</button>
    </div>
  );
}
```
