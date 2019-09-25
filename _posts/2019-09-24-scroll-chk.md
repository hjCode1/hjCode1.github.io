---
layout: post
title: scroll check
date:   2019-09-24
tag:
- javascript
- jQuery



---

## 스크롤 하단 체크하기, footer에서 멈추기

### 스크롤 이벤트 영역의 마지막 체크하기

```html
<form name="registration">
  <p>
      <textarea id="rules">Lorem ipsum dolor....
      </textarea>
  </p>
  <div>
    <p class="noti">끝까지 읽어주세요</p>
    <input type="checkbox" name="accept" id="agree" disabled>
    <label for="agree">동의합니다</label>
    <input type="submit" id="nextstep" value="다음" disabled>
    </div>
</form>
```

```css
#notice {
  display: inline-block;
  margin-bottom: 12px;
  border-radius: 5px;
  width: 600px;
  padding: 5px;
  border: 2px #7FDF55 solid;
}

#rules {
  width: 600px;
  height: 130px;
  padding: 5px;
  border: #2A9F00 solid 2px;
  border-radius: 5px;
}

.noti {
  margin: 0;
  color: red;
}
```

```js
function read() {
  var box = $('#rules');
  var chkBox = $('#agree');
  var nextBtn = $('#nextstep');
  var noti = $('.noti');
  var boxHeight = box.outerHeight();
  var boxSrcollHeight = box[0].scrollHeight;

  box.on('scroll', function() {
    var scrollTop = $(this).scrollTop();
    //console.log( boxHeight, boxSrcollHeight, scrollTop )
    if ((boxSrcollHeight - scrollTop) < boxHeight) {
      chkBox.removeAttr('disabled');
      nextBtn.removeAttr('disabled');
      noti.text('감사합니다');
    }
  })
}

read();
```


[예제보기](https://jsfiddle.net/hyuckjin/craek5os/)


### 플로팅 배너 footer영역에서 멈추기

```html
<main>
  <div id="content"></div>
  <footer>footer</footer>
  <div id="banner">
    banner
  </div>
</main>
```

```css
* {
  margin:0;
  padding:0;
}

main {
  position:relative;
}

#content {
  height: 1500px;
}

footer {
  background: #333;
  height: 300px;
  font-size: 30px;
  color: #fff;
}

#banner {
  position: fixed;
  right: 20px;
  bottom: 50px;
  width: 50px;
  height: 100px;
  background: salmon;
  box-shadow: 0 0 10px rgba(0, 0, 0, .6);
}

#banner.on {
  position: absolute;
  bottom: 350px;
}

```

```js
$(function() {

  var $w = $(window),
    footerHei = $('footer').outerHeight(),
    $banner = $('#banner');

  $w.on('scroll', function() {

    var sT = $w.scrollTop();
    var val = $(document).height() - $w.height() - footerHei;

    if (sT >= val)
        $banner.addClass('on')
    else
    		$banner.removeClass('on')

  });

});

```

[예제보기](https://jsfiddle.net/hyuckjin/63m04rf9/)

