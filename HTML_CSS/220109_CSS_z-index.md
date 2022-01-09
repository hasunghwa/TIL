### CSS

## z-index

> z-index를 사용하면 속성의 수직 위치 즉 겹치는 element끼리의 순서를 설정할 수 있다.

```css
div {
  z-index: 1;
}
```

z-index는 음, 양수의 값을 가질 수 있다. 숫자가 크면 위로 올라오고 작으면 아래로 내려간다.

```html
<div class="parent">
  <p class="children"></p>
</div>
```

하지만 부모 자식간의 관계에선 예외가 발생한다

```css
.parent {
  position: absolute;
  z-index: 0;
}
.child {
  position: absolute;
  z-index: 100;
}
```

자식요소의 z-index를 부모보다 높게 설정하여도 부모 앞에 나오지 않는다.

## overflow

> overflow를 통해 element의 내용의 요소의 크기를 벗어났을 때 처리하는 방법을 설정할 수 있다.

```css
div {
  overflow: visible | hidden | scroll | auto | initial | inherit;
}
```

- visible : 박스를 넘어가도 내용을 보여줌. (기본값)
- hidden : 박스를 넘어간 부분은 보이지 않음.
- scroll : 박스를 넘어가든 넘어가지 않든 스크롤바 형태로 스크롤링 가능하게 해줌.
- auto : 박스를 넘어갈 때에만 스크롤바 생성.
