# CSS

## media query

> 미디어 쿼리를 사용하면 단말기의 유형과, 크기에 따라 CSS스타일을 변경할 수 있다.

```css
@media (max-width: 600px) {
  background-color: green;
}

@media (max-width: 500px) {
  background-color: red;
}

@media (min-width: 601px) {
  background-color: blue;
}
```

max-width를 500을 주면 최대 화면이 500px일때까지 해당 CSS를 적용한다는 의미이고,  
min-width를 601을 주면 최소 화면이 601px 즉 601px 이후부터 해당 CSS를 적용한다는 의미이다.  
위의 코드를 해석하면 0부터 500px까지는 배경색을 red, 501부터 600까지는 green, 601이후부터는 blue로 한다는 뜻이다.

## CSS 접두어

## Filter

> filter 속성을 사용하면 흐림 효과나 색상 변형등 그래픽 효과를 적용할 수 있다.

```css
filter: blur(px);
filter: grayscale(%);
filter: contrast(%);
filter: invert(%);
filter: drop-shadow(x y blur 색상)
filter: opacity(%)
```

- blur: 주어진 이미지에 가우시안 블러를 적용  
  값이 클수록 흐려지고, 기본값은 0
- grayscale: 이미지를 회색조로 변환  
  값이 클수록 흑백화, 최대 100% 기본값은 0%
- contrast: 이미지의 대비를 조정  
  기본값은 100%, 0%는 검게 변환
- invert: 이미지 색상 반전  
  기본값은 0%, 최대 100%
- drop-shadow: 이미지에 그림자 효과 지정  
  x,y는 그림자의 위치좌표, blur는 흐림의 정도, 색상은 그림자의 색상 설정
- opacity: 이미지의 투명도 조정
  기본값은 100%, 최대 100%

## Blend

> blend-mode는 요소가 겹칠 경우 색상이 어떻게 나타나는지 정의한다. background-blend-mode 와 mix-blend-mode 속성에서 사용한다.

```css
background-blend-mode: normal | multiply | screen | overlay | darken | lighten |
  color-dodge | color-burn | hard-light | soft-light | difference | exclusion |
  hue | saturation | color | luminosity;
```

```css
mix-blend-mode: normal | multiply | screen | overlay | darken | lighten |
  color-dodge | color-burn | hard-light | soft-light | difference | exclusion |
  hue | saturation | color | luminosity;
```

## Transform

> 요소에 회전, 크기 조절, 기울기, 이동 효과를 부여할 수 있다. orgin속성을 사용하여 효과를 적용하는 중심위치를 설정할 수 있다.

```css
transform: translate(x, y);
transform: scale(x, y);
transform: rotate(angle);
transform-origin: center | top left | 50px 50px;
```

- translate: 요소의 위치를 X축으로 x만큼, Y축으로 y만큼 이동
- scale: 요소의 크기를 X축으로 x배, Y축으로 y배 확대 or 축소
- rotate: 요소를 angle만큼 회전

## Transition

> 트랜지션을 통해 CSS 속성을 변경할 때 애니메이션 속도를 조절할 수 있다.

```css
transition-property: all;
transition-duration: 1s;
transition-delay: 1s;
transition-timing-function: ease;
transition: property timing-function duration delay | initial | inherit;
```

- property: 트랜지션을 적용하는 속성 명시, 명시된 속성에만 트랜지션 적용
- duration: 트랜지션이 일어나는 총시간 설정
- delay: 속성이 변하기전에 지연시간 설정
- timing-function: 트랜지션의 진행속도 조절
- transition: 위의 속성들을 한번에 정의
