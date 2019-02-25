---
layout: post
title:  "아이폰 버튼 효과"
date:   2019-02-25
tag:
- blog
- css3
- html5

---

## 아이폰 버튼 효과

아이폰에서 볼 수 있는 버튼효과입니다.

##### html
```html
<div class="btn_wrap">
  <input type="checkbox" name="agree" id="aa">
  <label for="aa">동의<span class="btn"></span></label>
  <input type="checkbox" name="agree" id="bb">
  <label for="bb">거부<span class="btn"></span></label>
</div>
```

#### css
```css
.btn_wrap {
  padding: 50px;
}

.btn_wrap label {
  font-size: 30px;
}

.btn {
  display: inline-block;
  position: relative;
  background: #b2b2b2;
  border-radius: 30px;
  width: 100px;
  height: 50px;
  cursor: pointer;
  vertical-align: middle;
  transition: all 0.3s;
}

.btn:after {
  content: "";
  display: block;
  position: absolute;
  left: 0;
  top: 0;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  background: #fff;
  border: 1px solid #eee;
  transition: all 0.3s;
}

input[type="checkbox"] {
  display: none;
}

input[type="checkbox"]:checked+label .btn {
  background: #18e46e;
}

input[type="checkbox"]:checked+label .btn:after {
  left: 50px;
}

```



##### 결과

![](https://github.com/hjCode1/hjCode1.github.io/blob/master/images/apple_btn.gif?raw=true)

[jsfiddle에서 보기](https://jsfiddle.net/hyuckjin/rvj8cn32/)












