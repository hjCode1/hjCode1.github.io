---
layout: post
title:  "javascript 정규식 없이 함수로 replaceAll"
date:   2019-01-21
tag:
- blog
- javascript
- replace

---

## replaceAll 함수

JavaScript에서의 replace는 처음 문자열만 대체합니다. replaceAll의 효과를
볼 수 있는 함수를 구글링을 통해 찾았습니다.


**코드**
```js
function replaceAll(str,searchStr,replaceStr){
  return str.split(searchStr).join(replaceStr);
}
// str = 문자열 대체를 처리할 원 문자열
// searchStr = 대체할 문자
// replaceStr = 대체될 문자

var test = replaceAll('가나다라 가나 가가','가','하');
// 출력값 = '하나다라 하나 하하'
```










