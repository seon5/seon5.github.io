---
title: React Create 기능
date: 2023-07-09 22:45:00 +09:00
categories: [study, react]
tags:
  [
    react, 생활코딩
  ]
---

> CRUD의 C에 해당하는 Create 기능 구현에 관한 내용이다.   


구현 내용은 다음과 같다.

create 링크를 클릭하면 App 컴포넌트의 mode가 ‘create’로 변경되고, Content 컴포넌트 부분에 폼이 출력된다. 그리고 제출 버튼을 클릭하면 작성한 내용이 TOC 컴포넌트에 추가된다.

![image](/assets/posts/230709_create.png)
![image](/assets/posts/230709_create2.png)
![image](/assets/posts/230709_create3.png)   

<br><br><br>

구현 과정 중 state.contents 배열에 데이터를 추가하는 방법에 대한 설명만 작성하겠다.
<br><br><br>

**배열에 데이터를 추가하는 방법**은 다음이 있다.

1. push
2. concat

push를 통해 배열에 값을 추가하면 원본 배열의 값이 변경되고,

concat을 통해 추가하면 원본은 그대로이고, 새로운 복제본을 만들어 사용한다.

즉, **배열의 불변성**을 유지하는 것이다.

state의 값을 바꿀 때는 원본을 변경하지 않도록 **concat**을 사용하라고 한다.
<br><br><br>

state.contents 배열에 데이터를 추가하기 위한 전체 코드이다.

```jsx
else if(this.state.mode === 'create'){
      _article=<CreateContent onSubmit={function(_title, _desc){
        this.max_content_id=this.max_content_id+1;
        var _contents = this.state.contents.concat(
          {id:this.max_content_id, title:_title, desc:_desc}
        );
        this.setState({
          contents:_contents
        });
        console.log(_title, _desc);
      }.bind(this)}></CreateContent>
    }
```
<br><br><br>

concat 함수를 사용해 새로운 데이터를 추가하고, _contents 변수에 저장한다.

```jsx
var _contents = this.state.contents.concat(
          {id:this.max_content_id, title:_title, desc:_desc}
        );
```
<br><br><br>

그리고 **setState** 함수를 사용해 리액트가 알도록 contents state를 변경한다.

```jsx
this.setState({
          contents:_contents
        });
```
