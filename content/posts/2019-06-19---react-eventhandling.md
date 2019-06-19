---
title: "[React] Event Handle, state 상태관리, jsx for문 "
date: "2019-06-19T21:00:11.121Z"
template: "post"
draft: false
slug: "/posts/react-event/"
category: "React"
tags:
 - "React"
description: "리액트 event"
---

### 리액트 이벤트 핸들러

1. 트윗메인화면에 트윗을 입력하고 버튼 누르면 아래에 트윗 리스트 나오게 한다.
2. 트윗메인화면에서 textarea는 TweetRightBox라는 컴포넌트로 불러와서 메인화면에 조립했다.

##### 트윗메인화면 
```
...(생략)
<TweetRightBox onChange={this.handleChange} onClick={this.handleClick} value={this.state.inputMessage}/>
```
TweetRightBox에서 이벤트값을 props로 넘겨서 트윗메인 화면에서 받은 다음, 이벤트 구현하였다.

onChange는 textarea 내에서 값이 변화하면 브라우져가 인식한다. 최종적으로 넘길데이터는 

유저이름, 메시지내용, 프로필사진, 트윗생성날짜이다(유저가 정한다.)

```
 handleChange =(e) => {
     this.setState({
         username : this.props.username,   //다른 컴포넌트에서 값을 불러왔음.
         inputMessage : e.target.value,    // onChange의 e(이벤트)값으로 현재 입력값 추출
         propfilePhoto : "😻",
         created_at : this.dateFunc(),
     });
 }
```
#### 트윗메인 화면의 state

```
state = {
      TweetList : [],    // 결국 이 배열안에 내용을 랜더링 
      username : "",
      inputMessage :"",
      propfilePhoto : "", 
      created_at : ""       
  }
```
state 값은 통상 위와 같은 패턴으로 작성하고, 데이터만 관리한다.  

리스트에 생성될 HTML은 render()안에 return에서 생성해준다.  

#### 입력 후 버튼 클릭시 이벤트

버튼클릭시 이벤트는 유저이름, 메시지, 사진, 생성날짜가 트윗으로 들어가야한다.

# 리액트에서 가장 주의해야할점!
  1. setState안에 배열값은 직접적으로 변경하면 안된다. 
  2. 그럼 어떻게 ?? 기존값을 복사해서 저장한다.

```
 handleClick =(e)=>{
    const {username,inputMessage,propfilePhoto,created_at} = this.state 
    
    //1.입력하면 들어오는 값을 새로 newTweet이라는 객체에 담아서
    const newTweet ={
        username : username,
        inputMessage : inputMessage,
        propfilePhoto : propfilePhoto,
        created_at : created_at
    }
    //2. newTweets라는 배열에 넣는다.
    const newTweets = [newTweet, ...this.state.TweetList]  //이렇게 넣으면 가장 최신 트윗이 위로온다. 
                      //this.state.TweetList => 위에 state안에 있는 배열임. 
                      // ...[배열]은 배열의 복사를 의미.                                

    //3. textarea 값 초기화 및 리스트유지.     
    this.setState({
        inputMessage : "",
        TweetList : newTweets
    })
 }
```  
#### HTML생성 => map 이용(패턴)
    1. jsx문법으로 html양식을 생성하고, state의 데이터값을 입력한다.
    2. jsx에서 for문을 돌릴때는 key값이 반드시 필수. index로 키값하는 것은 좋지 않다. 유니크한 값이 좋다.

```
<ul id="list-root">
   {
      this.state.TweetList ? this.state.TweetList.map((tweet, i) => {  //맵에 대한 키값 i
          return(
             <div class="tweet-wrap-list">
             <div class="user-photo">{tweet.propfilePhoto}</div>
             <div class="wrap-name-and-comment-and-times">
               <div class="user-name">{tweet.username}</div>
               <div class="user-comment">{tweet.inputMessage}             
               </div>
               <span class="written-times">{tweet.created_at}</span>
             </div>          
           </div>  
          );
      }) : "" 
   }
 </ul> 
```

### 기억할점!
   1. 리액트 state는 클래스로 선언된 곳에서 상태관리로 사용한다. 함수형은 No!
   2. state 상태관리는 데이터만 관리! 그리고 그 데이터 부분을 랜더링하게 해주는 배열 필요!
      (데이터와 배열)
   3. jsx에서 for문 돌릴때 키값이 필요하다. 
   4. 화면에 자료 뿌리는 것은 html부분은 통상 for나 map을 이용해서 뿌리고, 그사이에 데이터를 넣어준다. 