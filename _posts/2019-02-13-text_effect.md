---
layout: post
title:  "css text에 반씩 색넣기"
date:   2019-02-13
tag:
- blog
- html
- css3

---

## text에 색을 반반씩 넣는 효과

#### 가상 엘리멘트와 data 속성을 사용

##### html
```html
<p data-split="split text color">split text color</p>

```
##### css
```css
body {
  height: 100vh;
  margin: 0;
  background: linear-gradient(90deg, #3498db 50%, #ffffff 50%);
}

p {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  margin: 0;
  color: #3498db;
  font-size: 7vw;
  font-family: 'Open Sans', sans-serif;
  font-weight: 700;
  text-transform: uppercase;
  white-space: nowrap;
}

p::before {
  position: absolute;
  top: 0;
  left: 0;
  content: attr(data-split);
  width: 50%;
  color: #fff;
  overflow: hidden;
}
```

##### 결과
![text](https://raw.githubusercontent.com/hjCode1/hjCode1.github.io/master/images/20190213.PNG)

[jsfiddle에서 보기](https://jsfiddle.net/hyuckjin/eLrhkyq5/)












