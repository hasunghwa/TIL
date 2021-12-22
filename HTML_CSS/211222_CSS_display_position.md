# CSS

## CSS 위치 속성

## 1. 디스플레이 (display)

> 대부분의 HTML 요소는 display 속성의 기본값으로 block과 inline 두 가지 중 하나의 값

- 블록
  - 언제나 새로운 라인(line)에서 시작하며, 해당 라인의 모든 너비를 차지
  - 대표적인 블록(block) 요소: \<div>, \<h1>, \<p>, \<ul>, \<ol>, \<form>
  ```css
  <style>
      li { display: block; }
  </style>
  ```
- 인라인
  - 새로운 라인(line)에서 시작하지 않는다.
  - 또한, 요소의 너비도 해당 라인 전체가 아닌 해당 HTML 요소의 내용(content)만큼만 차지
  - 대표적인 인라인(inline) 요소: \<span>, \<a>, \<img>
  ```css
  <style>
      li { display: inline; }
  </style>
  ```
- 인라인-블록

  - 해당 요소 자체는 인라인(inline) 요소처럼 동작
  - 해당 요소 내부에서는 블록(block) 요소처럼 동작

  ```css
    <style>
      .inline-block { display: inline-block; }
    </style>
  ```

  인라인 요소처럼 한 줄로 늘어서지만 블록 요소처럼 너비와 높이를 설정할 수 있게 된다.  
  웹 사이트의 메뉴나 내비게이션 바를 만들 때 자주 사용

## 2. 포지션 (position)

> HTML 요소가 위치를 결정하는 방식 설정

- 정적 위치(static) 지정 방식
  > 기본값으로서 top, right, bottom, left 속성값에 영향을 받지 않는다.
  ```css
  <style>
      div { position: static; }
  </style>
  ```
- 상대 위치(relative) 지정 방식
  > static위치에서 top, right, bottom, left 속성값에 영향을 받는다.
  ```css
  <style>
    div.relative { position: relative; left: 30px; }
  </style>
  ```
- 고정 위치(fixed) 지정 방식
  > 뷰포트를 기준으로 위치 설정, 웹 페이지 스크롤 되어도 고정된 위치.
  ```css
  <style>
    div.fixed { position: fixed; top: 0; right: 0; }
  </style>
  ```
- 절대 위치(absolute) 지정 방식
  > 조상요소를 기준으로 위치 설정, 조상요소가 없다면 body 요소를 기준으로 위치 설정.
  ```css
  <style>
      div.absolute { position: absolute; top: 50px; right: 0; }
  </style>
  ```
- CSS position 속성
  | 속성 | 설명 |
  | --- | --- |
  | position | HTML 요소의 위치를 결정하는 방식을 설정함. |
  | top | 위치가 설정된 조상 요소의 위로부터의 여백을 설정함. |
  | right | 위치가 설정된 조상 요소의 오른쪽으로부터의 여백을 설정함. |
  | bottom | 위치가 설정된 조상 요소의 아래로부터의 여백을 설정함. |
  | left | 위치가 설정된 조상 요소의 왼쪽으로부터의 여백을 설정함. |
  | z-index | 겹쳐지는 요소들이 쌓이는 스택(stack)의 순서를 설정함. |
  | clip | 절대 위치(absolute position) 지정 방식으로 위치한 요소를 자름. |
  | cursor | 표시되는 마우스 커서의 모양을 설정함. |
  | overflow | 내용(content)의 크기가 해당 요소의 박스(box)를 넘어갈 때 어떻게 처리할지를 설정함. |
  | overflow-x | 내용(content)의 크기가 해당 요소의 수평 방향으로 박스(box)를 넘어갈 때 어떻게 처리할지를 설정함. |
  | overflow-y | 내용(content)의 크기가 해당 요소의 수직 방향으로 박스(box)를 넘어갈 때 어떻게 처리할지를 설정함. |
