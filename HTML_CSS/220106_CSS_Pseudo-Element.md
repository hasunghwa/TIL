# CSS

## Pseudo-Element(가상요소)란?

> 선택자에 추가하는 키워드로, 선택한 요소의 지정된 부분에 스타일을 입힐 수 있다.  
> HTML 콘텐츠 내용을 변경하지 않고도 선택한 요소의 앞 뒤에 새 콘텐츠를 추가할 수 있다.

```css
선택자::의사요소이름 {
  속성: 속성값;
}
```

## ::before ::after

● ::before : 실제 내용 바로 앞에서 생성되는 자식요소  
● ::after : 실제 내용 바로 뒤에서 생성되는 자식요소

> before 와 after는 content앞 뒤에 삽입하기 때문에 content라는 속성이 필요하다.

### content란?

→ HTML에 포함되지 않은 요소를 CSS에서 새롭게 생성시켜주는 가짜 속성

```css
p::after {
  content: normal | string | image | counte | none | attr;
}
```

normal : 아무것도 표시하지 않는 기본값  
string : 문자열 생성  
image : 이미지, 비디오(크기 조절 불가)  
counte : 순서  
none : 표시 X  
attr : 해당속성의 속성값 표시

## ::first-line ::first-letter

● ::first-line : 텍스트의 첫 라인만을 선택  
● ::first-letter : 텍스트의 첫 글자만을 선택

> 블록 타입 요소에만 적용 가능.  
>  사용할 수 있는 속성 한정적(font, color, background, margin, padding, border등)

```css
/* 첫글자만 하얀색으로  */
p::first-letter {
  color: white;
}
```

## ::marker

> 목록 항목의 마커를 선택

```css
/* 마커의 색상을 빨간색으로 */
::marker {
  color: red;
}
```
