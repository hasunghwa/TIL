# React

## Framer

framer-motion은 리액트를 위한 웹 애니메이션, 제스처 오픈소스 라이브러리입니다.

```cmd
//install
npm install framer-motion
```

```jsx
import { motion } from "framer-motion";

export const MyComponent = () => <motion.div animate={{ opacity: 1 }} />;
```

### motion.(element)

> motion을 사용하여 element를 생성하고 animate를 통해 간단하게 animation을 등록할 수 있다.

```jsx
<motion.div
  initial={{ opacity: 0 }}
  animate={{ opacity: 1 }}
  transition={{ duration: 3 }}
/>
```

> initial
> 을 통해 애니메이션 초기값을 지정할 수 있고,  
> transition을 통해 delay, duration같은 애니메이션 방식을 정의할 수 있다.

```jsx
const variants = {
  visible: { opacity: 1 },
  hidden: {
    opacity: 0,
    transition: { duration: 3 },
  },
};

<motion.div initial="hidden" animate="visible" variants={variants} />;
```

### variants

> variants를 이용하면 애니메이션 상태를 정의하고 이름별로 구성할 수 있다.

> delayChildren 및 staggerChildren 같은 트랜지션 옵션을 사용하면 부모 애니메이션을 기준으로 자신 애니메이션이 재생되는 시기를 조정할 수 있다.

> delayChildren: 지정한 시간 후 하위 애니메이션 시작  
> staggerChildren: 하위 애니메이션간의 delay 지정

## Gestures

제스처 인식을 통한 이벤트 리스터를 사용할 수 있다.  
호버, 탭, 드래그 제스처 감지등을 지원한다.

> Hover: 요소 위로 마우스를 가져가거나 떠날 때를 감지  
> Tab: 버튼을 누르거나, 터치했을 때 발생하는 이벤트

```jsx
<motion.button
  whileHover={{
    scale: 1.2,
    transition: { duration: 1 },
  }}
  whileTap={{ scale: 0.9 }}
/>
```

### drag

```jsx
<motion.div darg /> // x and y
<motion.div drag="x"|"y" /> // x or y
```

drag를 사용하면 간편하게 드래그로 element를 x, y축으로 이동 할 수 있다.

```jsx
<motion.div whileDrag={{ scale: 1.2 }} />
```

drag 제스처가 인식되는 동안의 애니메이션을 설정할 수 있다.

```jsx
<motion.div drag="x" dragConstraints={{ left: 0, right: 300 }} />
```

dragConstraints를 통해 드래그 허용가능 영역에 제약을 줄 수 있다.

```jsx
const MyComponent = () => {
  const constraintsRef = useRef(null);

  return (
    <motion.div ref={constraintsRef}>
      <motion.div drag dragConstraints={constraintsRef} />
    </motion.div>
  );
};
```

useRef를 활용하여 해당 element 안에서만 움직이도록 할수도 있다.

```jsx
<motion.div
  drag
  dragConstraints={{ left: 0, right: 300 }}
  dragSnapToOrigin
  dragElastic={0.2}
/>
```

dragSnapToOrigin가 true이면 드래그한 element를 놓았을 때 원점으로 다시 되돌린다.  
dragElastic을 통해 제약조건에서 허용되는 이동 정도를 설정할 수 있다.  
0 = 움직임 없음, 1 = 전체 움직임. 기본 값은 0.5이다.

### MotionValue

MotionValue를 사용하여 애니메이션 값의 상태와 속도를 추적할 수 있다.

```jsx
import { motion, useMotionValue } from "framer-motion";

export function MyComponent() {
  const x = useMotionValue(0);
  return <motion.div style={{ x }} />;
}
```

useTransform을 활용하면 수동으로 값을 변형하여 요소에 활용할 수 있다.  
React의 렌더링 주기를 트리거하지 않고 시각적 속성을 업데이트한다.

```jsx
const x = useMotionValue(0);
const input = [-200, 0, 200];
const output = [0, 1, 0];
const opacity = useTransform(x, input, output);

return <motion.div drag="x" style={{ x, opacity }} />;
```

x좌표값이 -200일때 0, 0일때 1, 200일때 0값을 반환한다.  
x좌표값이 -200을 기준으로 출력은 0, 0에 가까워질 수록 출력값이 점점 커지다가, 0일때 1이된 후 x좌표값이 0보다 커지면 출력은 다시 작아져 x좌표가 200일때 0이 된다.

### useViewportScroll

뷰포트가 스크롤될 때 업데이트되는 MotionValues를 반환한다.

```jsx
export const MyComponent = () => {
  const { scrollYProgress } = useViewportScroll();
  return <motion.div style={{ scaleX: scrollYProgress }} />;
};
```

### AnimatePresence

React 트리에서 컴포넌트가 제거될 때의 애니메이션을 처리한다.  
AnimatePresence컴포넌트 안에는 조건문이 필요하며,
exit를 통해 제거될때 에니메이션을 설정할 수 있다.

```jsx
import { AnimatePresence, motion } from "framer-motion";

export const MyComponent = ({ isVisible }) => {
  return (
    <AnimatePresence>
      {isVisible && (
        <motion.div
          initial={{ opacity: 0 }}
          animate={{ opacity: 1 }}
          exit={{ opacity: 0 }}
        />
      )}
    </AnimatePresence>
  );
};
```

### layoutId

layoutId를 통해 요소를 연결할 수 있다. layoutId로 연결된 요소는 React 트리에서 제거된 다음 다른 곳에 추가되면 이전 구성 요소가 최신 애니메이션 값으로 자동으로 애니메이션 된다.

```jsx
{
  items.map((item) => (
    <motion.li layout>
      {item.name}
      {item.isSelected && <motion.div layoutId="underline" />}
    </motion.li>
  ));
}
```

### pathLength

```jsx
const svg = {
  start: { pathLength: 0, fill: "rgba(255, 255, 255, 0)" },
  end: {
    fill: "rgba(255, 255, 255 , 1)",
    pathLength: 1,
  },
};
```

pathLength를 통해 간편하게 선 그리기 애니메이션을 생성할 수 있다. 0과 1사이 값을 가지며 1은 모든 경로의 측정길이이다.
