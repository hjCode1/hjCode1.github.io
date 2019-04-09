---
layout: post
title:  Vue로 Todolist 만들기
date:   2019-04-09
tag:
- Vue
- Todolist


---

## Todolist

##### HTML

```html
<div id="todo">
   <div id="header">
      <h2>Todo list App</h2>
      <input type="text" class="input" id="task" placeholder="입력 후 엔터" v-model.trim="todo" @keyup.enter="addTodo">
      <!-- v-model로 폼 바인딩 .trim으로 공백 제거 -->
      <!-- enter 이벤트 발생 시 addTodo 실행 -->
      <span class="add_btn" @click="addTodo">추 가</span>
   </div>
   <ul id="list">
      <li v-for="a in todolist" v-bind:class="checked(a.done)" @click="doneToggle(a.id)">
      <!-- for문으로 리스트 생성 -->
      <!-- checked 클래스 바인딩 -->
         <span>{{ a.todo }}</span>
         <span v-if="a.done">(완료)</span>
         <span class="close" @click.stop="deleteTodo(a.id)">x</span>
         <!-- click 이벤트 발생 시 deleteTodo 실행 -->
      </li>
   </ul>
</div>
```

##### CSS

```css
* {
   box-sizing: border-box;
}

h2 {
   padding: 0 0 20px;
   font-size: 25px;
}

li {
   position: relative;
   padding: 8px 8px 8px 40px;
   background: #eee;
   font-size: 14px;
   transition: all .2s ease;
   cursor: pointer;
   user-select: none;
}

li:hover {
   background: #ddd;
}

li.checked {
   background: #bbb;
   color: #fff;
   text-decoration: line-through;
}

li.checked::after {
   content: "";
   position: absolute;
   left: 16px;
   top: 10px;
   border-color: #fff;
   border-width: 0 1px 1px 0;
   border-style: solid;
   width: 8px;
   height: 8px;
   transform: rotate(45deg);
}

.close {
   position: absolute;
   right: 0;
   top: 0;
   padding: 8px 16px;
}

.close:hover {
   background: #f44336;
   color: #fff;
}

#header {
   background: purple;
   padding: 30px;
   color: yellow;
   text-align: center;
}

#header::after {
   content: "";
   display: block;
   clear: both;
}

.input {
   float: left;
   padding: 10px;
   border: none;
   width: 75%;
   height: 35px;
   font-size: 16px;
}

.add_btn {
   float: left;
   padding: 10px;
   background: salmon;
   width: 25%;
   height: 35px;
   font-size: 13px;
   color: #fff;
   cursor: pointer;
   transition: all .3s ease;
}

.add_btn:hover {
   background: #bbb;
}

.complete {
   text-decoration: none;
}

```

##### Vue
```js
var vm = new Vue({
	el : '#todo',
  data : {
  	todo : "",
    todolist : [
      { id:1, todo:"영화보기", done:false },
      { id:2, todo:"주말 산책", done:true },
      { id:3, todo:"es6 실습", done:false },
      { id:4, todo:"잠실 야구장", done:false }
    ]
  },
  methods : {
  	checked : function(done){
    	if(done) return { checked:true };
     	else return { checked:false }
    },
    addTodo : function(e){
    	if( this.todo !== "" ){
      	this.todolist.push({ id: new Date().getTime(), todo: this.todo, done:false });
        this.todo = "";
      }
    },
    deleteTodo : function(id){
    	var idx = this.todolist.findIndex(function(item){
      	return item.id === id;
        // todolist의 id들 중 현재 id와 같다면 return
      })
      this.todolist.splice(idx,1);
    },
    doneToggle : function(id){
    	var idx = this.todolist.findIndex(function(item){
      	return item.id === id;
      })
      this.todolist[idx].done = !this.todolist[idx].done;
    }
  }
})
```



참고
[jsfiddle에서 보기](https://jsfiddle.net/hyuckjin/64wfnoaL/)





