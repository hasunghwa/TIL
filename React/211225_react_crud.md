# React

## 컴포넌트 CRUD구현

## 1. Create

```jsx
// App.js
const[content, setContent] = useState([
      {id:1, title:'HTML', desc:'HTML is ...'},
      {id:2, title:'CSS', desc:'CSS is ...'},
      {id:3, title:'JavaScripte', desc:'JavaScripte is ...'}
    ]);

function getContent() {
  if(mode === 'create') {
    _article = <CreateContent onSubmit = { function(_title, _desc) {
      let _contests = content.concat({ id: content.length+1, title: _title, desc: _desc });
      setContent(_contests);
      setMode('read');
      setContentid(content.length);
    }
  }></CreateContent>
  return _article;
```

```jsx
// CreateContent.js
const CreateContent = (props) => {
  return (
    <article>
      <h2>Create</h2>
      <form
        action="/create_process"
        method="post"
        onSubmit={function (e) {
          e.preventDefault();
          props.onSubmit(e.target.title.value, e.target.desc.value);
          alert("submit");
        }}
      >
        <p>
          <input type="text" name="title" placeholder="title"></input>
        </p>
        <p>
          <textarea name="desc" placeholder="description"></textarea>
        </p>
        <p>
          <input type="submit"></input>
        </p>
      </form>
    </article>
  );
};

export default CreateContent;
```

기존의 content에 CreateContent.js에서 onSubmit을 통해 전달받은 데이터로 새로운 content를 추가하여 컴포넌트를 생성하였다.

concat함수를 사용하여 새로운 변수에 기존의 값과 새로 추가된 값을 연결하였고, setContent함수로 content의 값을 업데이트 하였다.

## 2. UPDATE(READ, CREATE)

```jsx
// App.js
function getContent() {
  if(mode === 'update') {
    _article = <UpdateContent
      id={contentid}
      title={content[contentid].title}
      desc={content[contentid].desc}
      onSubmit={function(newContent){
        let _content = Array.from(content);
        _content[Number(newContent.content.id)] =
          { id: Number(newContent.content.id)+1,
            title: newContent.content.title,
            desc: newContent.content.desc
          };
        setContent(_content);
        setMode('read');
      }
    }></UpdateContent>
  return _article;
}
```

```jsx
// UpdateContent.js
import { useState } from "react/cjs/react.development";

const UpdateContent = (props) => {
  const [content, setContent] = useState({
    id: props.id,
    title: props.title,
    desc: props.desc,
  });

  function inputFormHandler(e) {
    let newContent = Object.assign({}, content);
    newContent[e.target.name] = e.target.value;
    setContent(newContent);
  }

  return (
    <article>
      <h2>Update</h2>
      <form
        action="/create_process"
        method="post"
        onSubmit={function (e) {
          e.preventDefault();
          props.onSubmit({ content });
          alert("submit");
        }}
      >
        <input type="hidden" namd="id" value={content.id}></input>
        <p>
          <input
            type="text"
            name="title"
            placeholder="title"
            value={content.title}
            onChange={inputFormHandler}
          ></input>
        </p>
        <p>
          <textarea
            onChange={inputFormHandler}
            name="desc"
            placeholder="description"
            value={content.desc}
          ></textarea>
        </p>
        <p>
          <input type="submit"></input>
        </p>
      </form>
    </article>
  );
};

export default UpdateContent;
```

title과 description을 수정하는 코드를 작성 하였다.  
props는 readonly기 때문에 값을 변경할 수 없기 때문에 새로운 state를 생성하여 데이터를 수정하였다.  
onChange속성을 통해 값이 변경되면 inputFormHandler을 통해 해당하는 state를 변경하였다.  
수정된 값이 onSubmit을 통해 넘어오고 해당하는 id값의 content를 수정하였다.

## 3. DELETE

```jsx
//Control.js
<li>
  <input
    onClick={function (e) {
      e.preventDefault();
      props.onChangeMode("delete");
    }}
    type="button"
    value="delete"
  ></input>
</li>
```

```jsx
// App.js
<Control
  onChangeMode={function (_mode) {
    if (_mode === "delete") {
      if (window.confirm("really?")) {
        let _content = Array.from(content);
        _content.splice(contentid, 1);
        setMode("welcome");
        setContent(_content);
      }
      alert("delete!");
    } else {
      setMode(_mode);
    }
  }}
></Control>
```

delete버튼을 클릭하면 mode를 delete로 수정하고 splice를 통해 해당하는 content를 삭제하였다.
