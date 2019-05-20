---
layout: post
title:  이벤트 중단 방법
date:   2019-05-20
tag:
- javascript


---

## javascript에서 이벤트 중단하는 방법

자바스크립트 이벤트 리스너에서 preventDefault()와 stopPropagation()
그리고 return false는 이벤트 중단을 위해 자주 사용된다.

이벤트 중단에 사용되는 방식은 다음과 같다

#### event.preventDefault()
현재 이벤트의 기본 동작을 중단한다.

#### event.stopPropagation()
현재 이벤트가 상위로 전파되지 않도록 중단한다.

#### event.stopImmediatePropagation()
현재 이벤트가 상위 뿐 아니라 현재 레벨에 걸린 다른 이벤트도 동작하지 않게 중단한다.

#### return false
제이쿼리를 사용할 때는 위의 두개를 모두 사용한 것과 같고,
제이쿼리를 사용하지 않을 때는 event.preventDefault()와 같다.


일반적으로 DOM에서 내가 원하는 이벤트 동작만을 실행하고 싶을 때에는
event.stopPropagation()과 event.preventDefault() 두 코드를 모두 사용해야 한다.
(또는 return false)



