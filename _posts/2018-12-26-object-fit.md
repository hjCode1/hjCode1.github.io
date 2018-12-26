---
layout: post
title:  "img요소에 background-size: cover 효과를 낼 수 있는 object-fit: cover"
date:   2018-12-26
tag:
- blog
- html5
- css3

---

#img요소에 background-size: cover 효과를 낼 수 있는 object-fit: cover

‘object-fit: cover’ 속성은 IE, EDGE 브라우저에서는 적용되지 않는 CSS 속성입니다. 하지만 글 아래부분에 IE, EDGE 브라우저에도 img요소에 background-size: cover 효과를 낼 수 있는 방법을 적어놓았습니다


##object-fit의 속성
```
object-fit: fill;
object-fit: contain;
object-fit: cover;
object-fit: none;
object-fit: scale-down;
```
- object-fit: fill – 이미지가 강제로 늘어나거나 줄어들면서 지정한 넓이, 높이에 꽉 차게 됩니다. 원본 이미지의 비율을 유지하지 않습니다.
- object-fit: contain – 원본 이미지의 비율을 유지하면서 지정한 넓이, 높이안에서 최대한 확대시킵니다. 잘리는 부분이 발생하지 않습니다.
- object-fit: cover – 원본 이미지의 비율을 유지하면서 지정한 넓이, 높이에 꽉 차게 됩니다. 잘리는 부분이 발생합니다.
- object-fit: none – 지정한 넓이, 높이에 상관없이 원본 이미지의 크기를 유지합니다. 원본 이미지 가운데 부분이 보여지게 됩니다.
- object-fit: scale-down – 지정한 넓이, 높이값보다 원본 이미지가 작으면 그대로 두고, 크면 원본이미지 사이즈를 줄여서 보여줍니다.

### IE, EDGE에서 적용하기

```
<script>
// Detect objectFit support
if('objectFit' in document.documentElement.style === false) {
  
  // assign HTMLCollection with parents of images with objectFit to variable
  var container = document.getElementsByClassName('classname'); // img를 감싸고 있는 div의 class name 을 써주세요.
  
  // Loop through HTMLCollection
  for(var i = 0; i < container.length; i++) {
    
    // Asign image source to variable
    var imageSource = container[i].querySelector('img').src;
    
    // Hide image
    container[i].querySelector('img').style.display = 'none';
    
    // Add background-size: cover
    container[i].style.backgroundSize = 'cover';
    
    // Add background-image: and put image source here
    container[i].style.backgroundImage = 'url(' + imageSource + ')';
    
    // Add background-position: center center
    container[i].style.backgroundPosition = 'center center';
  }
}
else {
  // You don't have to worry
  console.log('No worries, your browser supports objectFit')
}
</script>
```

[codepen에서 확인](https://codepen.io/pawelgrzybek/pen/Rrybqg)



* * *
