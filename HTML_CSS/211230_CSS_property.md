# CSS

## CSS 속성

### 타이포그래피(Typography)

- font-size
  단위 (px: 고정, rem: 가변)  
  html의 font-size가 16px이라면 1rem=16px

  ```css
  font-size: 1rem;
  ```

- color

  ```css
  color: red; /* color name */
  color: rgb(255, 0, 0); /* rgb */
  color: #ff0000; /* hex */
  ```

- text-align(정렬)  
  center, right, left, justify....

  ```css
  text-align: center;
  ```

- font

  > 입력된 우선순위에 따라 해당폰트가 없다면 다음 폰트로 출력

  Sans-serif(장식x) vs Serif
  ![image6](./image/image6.png)

  font-weight → 폰트 굵기(normal, bold)  
  line-height → 폭의 간격(2를 쓰면 폰트크기의 2배)

  ```css
  font-size: 5rem;
  font-family: arial, verdana, "Helevetica Neue", serif;
  font-weight: bold;
  line-height: 2;
  ```

  > 위의 모든 폰트 속성을 font를 사용하면 하나의 속성으로 작성가능

  ```css
  font: bold 5rem/2, arial, verdana, "Helevetica Neue", serif;
  ```

- web font

  > 웹에서 다운받아서 사용하는 폰트(폰트 용량 이슈)  
  > 구글 웹폰트 사이트 https://fonts.google.com/

  ```html
  <link
    href="https://fonts.googleapis.com/css2?family=Open+Sans&display=swap"
    rel="stylesheet"
  />
  ```

  ```css
  font-family: "Open Sans", sans-serif;
  ```

  사용하고싶은 폰트를 선택하여 link tag를 통해 다운받고 css에서 font-family를 통해 적용

- font-face  
  font-face는 자신이 가지고 있는 폰트를 사용할 수 있게 해준다.  
  font-face generator를 통해 자신의 폰트를 변형하여 다운받고 font-face를 통해 폰트를 정의한다.

```html
@font-face {
  font-family: <a-remote-font-name>;
  src: <source> [,<source>]*;
  [font-weight: <weight>];
  [font-style: <style>];
}
```
