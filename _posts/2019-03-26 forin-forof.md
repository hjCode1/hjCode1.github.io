---
layout: post
title:  "for in 과 for of"
date:   2019-03-26
tag:
- javascript
- es6

---

## for in과 for of

for in문과 for of문은 비슷하지만 차이점이 있습니다.

- for in : 객체 의 열거 가능한 속성을 반복
- for of : 객체 의 속성값 을 반복

for in문은 객체의 속성들을 반복하여 작업할 수 있습니다.
다음은 for in 문을 이용하여 객체의 프로퍼티명과 프로퍼티값을 열거하는 코드입니다.

```js
var obj = {
	x:1,
    y:true,
    z:'hello'
}
for (let k in obj) {
    console.log(k + " : " + obj[k]);
}

//콘솔 출력값
//x : 1
//y : true
//z : hello
```

for of는 es6에 추가된 구문입니다. 이 구문을 사용하기 위해서는
객체가 이터레이터 속성을 가지고 있어야 합니다.

```js
let str = "test";
let arr = [1,3,5];

for (let i of str){
	console.log(i)
}
//콘솔 값 t,e,s,t
for (let i of arr){
	console.log(i)
}
//콘솔 값 1,3,5
```



##### 참조

[참조사이트](https://mailchi.mp/webtoolsweekly/web-tools-230?e=b2c0f00eca)












