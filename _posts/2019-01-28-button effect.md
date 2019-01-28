---
layout: post
title:  "css+js를 이용한 버튼 효과"
date:   2019-01-28
tag:
- blog
- css3
- javascript
- jquery

---

## Button effect

mouseEvent 효과로 만드는 버튼 효과입니다.


**html**
```html
<a class="more_btn" href="">cilck<span></span></a>
```

**css**
```css
.more_btn {
  overflow: hidden;
  display: block;
  position: relative;
  width: 160px;
  margin-top: 45px;
  border: 1px solid skyblue;
  font-size: 13px;
  font-weight: 700;
  line-height: 54px;
  text-align: center;
  color: #222;
  -webkit-transition: color .4s;
  transition: color .4s;
  font-family: 'Montserrat'
}

.more_btn span {
  position: absolute;
  z-index: -1;
  display: block;
  width: 0;
  height: 0;
  border-radius: 50%;
  background-color: skyblue;
  -webkit-transition: all .4s ease-in-out;
  transition: all .4s ease-in-out;
  -webkit-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%)
}

.more_btn:hover {
  color: #fff
}

.more_btn:hover span {
  width: 350px;
  height: 350px
}

```

**jquery**
```js
$(function() {
  $('.more_btn')
    .on('mouseenter', function(e) {
      var parentOffset = $(this).offset(),
        relX = e.pageX - parentOffset.left,
        relY = e.pageY - parentOffset.top;
      $(this).find('span').css({
        top: relY,
        left: relX
      })
    })
    .on('mouseout', function(e) {
      var parentOffset = $(this).offset(),
        relX = e.pageX - parentOffset.left,
        relY = e.pageY - parentOffset.top;
      $(this).find('span').css({
        top: relY,
        left: relX
      })
    });
});

```

**결과**


![hover](https://github.com/hjCode1/hjCode1.github.io/blob/master/images/btn_hover.gif?raw=true)

[jsfiddle에서 보기](https://jsfiddle.net/hyuckjin/s2ux63do/)










