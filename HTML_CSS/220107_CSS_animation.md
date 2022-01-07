# CSS

## animation

애니메이션은 요소에 적용되는 CSS스타일을 다른 스타일로 부드럽게 전환시켜 준다.  
트랜지션보다 훨씬 규모가 크고 복잡하며 다양한 기능을 가지고 있어 세밀한 효과를 구현할 수 있다.

## animation 속성

### ● animation-name

> name속성을 통해 애니메이션의 이름을 설정할 수 있다.  
> 이름을 정의해야 애니메이션을 호출할 수 있다.

```css
div {
  animation-name: big;
}
```

### ● animation-duration

> duration속성을 통해 애니메이션을 한 번 재생하는 데 걸리는 시간을 설정할 수 있다.

```css
div {
  animation-duration: 2s;
}
```

### ● animation-delay

> delay속성을 통해 애니메이션 시작전 지연시간(대기시간)을 설정할 수 있다.

```css
div {
  animation-delay: 2s;
}
```

### ● animation-direction

> direction속성을 통해 애니메이션의 재생 방향을 설정할 수 있다.

```css
div {
  animation-direction: normal | alternate | reverse | alternate-reverse;
}
```

nomal : 애니메이션을 순방향으로 재생.  
alternate : 순방향으로 시작해 역방향과 순방향으로 번갈아 에니메이션 재생.  
reverse : 애니메이션을 역방향으로 재생.  
alternate-reverse : 역방향으로 시작하여 순방향과 역방향으로 번갈아 애니메이션 재생.

### ● animation-play-state

> play-state를 통해 애니메이션을 재생하고 멈출 수 있다.

```css
div {
  animation-play-state: running | paused;
}
```

### ● animation-timing-function

> timing-function을 통해 키프레임 사이의 재생속도를 조정할 수 있다.  
> transition의 timing-function과 유사하다

```css
div {
  animation-play-state: ease-in-out | ease;
}
```

## @keyframes

> 애니메이션을 재생할 각 프레임의 스타일을 정의한다.  
> from(0%) 속성부터 시작하여 to(100%) 속성에 설정한 스타일로 바뀐다.

```css
@keyframes animationName {
  from {
    css-styles;
  }
  to {
    css-styles;
  }
}
/* 0%와 100% 사이에 여러 개의 중간 값(%)을 설정해 프레임을 작성할 수 있다. */
@keyframes animationName {
  0% {
    css-styles;
  }
  50% {
    css-styles;
  }
  100% {
    css-styles;
  }
}
```

## transition VS animation 차이

transition 속성과 animation 속성은 자바스크립트의 도움 없이 요소에 직접 애니메이션 효과를 적용하는 속성이다.

transition 속성과 animation 속성의 가장 큰 차이는 transition 속성은 요소의 상태가 바뀌어야 바뀌는 상태를 애니메이션으로 표현하지만, animation 속성은 요소의 상태 변화와 상관 없이 애니메이션을 실행한다.
