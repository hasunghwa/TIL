# CSS

## Flexbox

### 1. container

- display
  > HTML 요소에 대한 박스의 타입을 명시함.  
  > display: flex를 통해 flex로 변환
  ```css
  <style>
    .container { display: flex; }
  </style>
  ```
- flex-direction

  > 플렉스 컨테이너(flex container)안의 플렉스 요소(flex item)가 위치할 방향을 설정함.  
  > 1\. row : 기본 설정, 왼쪽에서 오른쪽으로, 위쪽에서 아래쪽으로 배치.  
  > 2\. row-reverse : 오른쪽에서 왼쪽으로 배치.  
  > 3\. column : 수직 방향으로 위쪽에서 아래쪽으로 배치.  
  > 4\. column-reverse : 수직 방향으로 아래쪽에서 위쪽으로 배치.

  ```css
  <style>
    .container { display: flex; flex-direction: row; }
  </style>
  ```

- flex-wrap
  > 플렉스 라인에 더 이상의 여유 공간이 없을 때, 플렉스 요소의 위치를 다음 줄로 넘길지를 설정함.  
  > 1\. nowrap : 기본 설정, 플렉스 요소가 다음 줄로 넘어가지 않고, 너비를 줄여서 한 줄에 모두 배치.  
  > 2\. wrap : 여유 공간이 없으면 다음 줄로 넘어가서 배치.  
  > 3\. wrap-reverse : 여유 공간이 없으면 다음 줄로 넘어가서 배치된다. 단, wrap과 반대로.
  ```css
  <style>
   .container { display: flex; flex-wrap: wrap; }
  </style>
  ```
- flex-flow
  > flex-direction 속성과 flex-wrap 속성을 이용한 스타일을 한 줄에 설정할 수 있음.
  ```css
  <style>
   .container { display: flex; flex-flow: column nowrap;}
  </style>
  ```
- justify-content
  > 플렉스 요소의 수평 방향 정렬 방식을 설정함. **중심 축**  
  > 1\. flex-start : 기본 설정, 컨테이너의 앞쪽에서부터 배치.  
  > 2\. flex-end : 컨테이너의 뒤쪽에서부터 배치. \*\*순서유지  
  > 3\. **center** : 컨테이너의 가운데에서부터 배치.  
  > 4\. space-between : 요소들 사이에만 여유 공간을 두고 배치.  
  > 5\. **space-around** : 앞, 뒤, 그리고 요소들 사이에도 모두 여유 공간을 두고 배치.
  ```css
  <style>
   .container { display: flex; justify-content: space-around; }
  </style>
  ```
- align-items
  > 플렉스 요소의 수직 방향 정렬 방식을 설정함.  
  > 1\. stretch : 기본 설정, 플렉스 요소의 높이가 플렉스 컨테이너의 높이와 같게 변경된 뒤 연이어 배치.  
  > 2\. flex-start : 컨테이너의 위쪽에 배치.  
  > 3\. flex-end : 컨테이너의 아래쪽에 배치.  
  > 4\. **center** : 컨테이너의 가운데에 배치.  
  > 5\. baseline : 컨테이너의 기준선(baseline)에 배치.
  ```css
  <style>
   .container { display: flex; align-items: center; }
  </style>
  ```
- align-content
  > flex-wrap 속성의 동작을 변경할 수 있음, 플렉스 라인을 정렬함. **보조 축**  
  > 1\. stretch : 기본 설정, 플렉스 라인의 높이가 남는 공간 차지.  
  > 2\. flex-start : 플렉스 라인은 플렉스 컨테이너의 앞쪽에.  
  > 3\. flex-end : 플렉스 라인은 플렉스 컨테이너의 뒤쪽에.  
  > 4\. center : 플렉스 라인은 플렉스 컨테이너의 가운데에.  
  > 5\. space-between : 플렉스 라인은 플렉스 컨테이너에 고르게 분포.  
  > 6\. space-around : 플렉스 라인은 플렉스 컨테이너에 고르게 분포. 단, 양쪽 끝에 약간의 공간.
  ```css
  <style>
   .container { display: flex; align-content: space-between; }
  </style>
  ```

### 2. item

- order
  > 플렉스 컨테이너 안에 있는 플렉스 요소들의 순서를 설정함.
  ```css
  <style>
   .item1 { display: flex; order: 1; }
   .item2 { display: flex; order: 3; }
   .item3 { display: flex; order: 2; }
  </style>
  ```
- flex(flex-grow, flex-shrink, flex-basis)

  > 같은 플렉스 컨테이너 안에 있는 플렉스 요소의 너비를 상대적으로 설정함.

  ```css
  <style>
    /* 2:1:1 비율로 늘어 남, 1:1:1 비율로 줄어듬 */
   .item1 { display: flex; grow: 2; shrink: 1; }
   .item2 { display: flex; grow: 1; shrink: 1; }
   .item3 { display: flex; grow: 1; shrink: 1; }
  </style>
  ```

  ```css
  <style>
    /* 6:3:1 비율로 늘어나고 줄어듬 */
   .item1 { display: flex; flex-basis: 60%; }
   .item2 { display: flex; flex-basis: 30%; }
   .item3 { display: flex; flex-basis: 10%; }
  </style>
  ```

  ```css
  <style>
    /* grow, shrink, basis 묶어서 flex 하나로 사용 */
   .item1 { display: flex; flex: 2 1 auto; }
   .item2 { display: flex; flex: 1 1 auto; }
   .item3 { display: flex; flex: 1 1 auto; }
  </style>
  ```

- align-self
  > 컨테이너의 align-items 속성보다 우선 적용, 플렉스 요소마다 서로 다른 align 속성값을 설정함.
  ```css
  <style>
   .container { display: flex; align-self: center; }
  </style>
  ```
