---
layout: post
title:  wil-change
date:   2019-04-15
tag:
- css


---

## will-change

`will-change` 는 변화가 예상되는 요소를 브라우저에게 미리 알려줍니다. 브라우저는 실제 요소가 변화되기 전에 적절하게 최적화를 할 수 있습니다. 큰 비용이 드는 변화도 최적화로 인해 페이지의 반응성을 증가시킬 수 있습니다.


### will-change의 지원범위

![](https://github.com/hjCode1/hjCode1.github.io/blob/master/images/wc.PNG?raw=true)


### will-change 속성

``` css
will-change: auto;
will-change: scroll-position;
will-change: contents;
will-change: transform;
will-change: top, left;
```

- auto
 - 기본값으로 브라우저는 별다른 최적화를 실시하지 않습니다.

- scroll-position
 - 스크롤 할 때 엘리먼트의 위치가 변경될 것을 알려줍니다. 이 값을 설정하면 브라우저는 스크롤 가능한 엘리먼트를 미리 최적화 하여 랜더링 합니다. 한 번에 많은 양을 스크롤하거나 빠른 스크롤이 필요한 경우에 사용합니다.

- contents
 - 엘리먼트의 컨텐츠가 변경될 것을 알려줍니다. 브라우저는 보통 엘리먼트의 랜더링 결과를 캐싱합니다. 대부분의 엘리먼트가 변경되지 않고 변경되어도 위치가 바뀌는 정도의 미미한 변경만 발생하기 때문입니다. 하지만 엘리먼트가 계속해서 변경되는 경우 브라우저 캐시는 무의미하게 됩니다. 이 속성을 사용하게 되면 캐시를 하지 않고 변경될 때마다 처음부터 랜더링하게 됩니다.

- custom-ident
 - 변경하고 싶은 속성을 사용할 수 있습니다. 쉼표(,)를 이용하여 두 개 이상의 속성을 사용할 수 있습니다. 크롬에서는 현재 6가지 속성(opacity, transform, top, left, right, bottom)만 적용됩니다


### will-change 사용시 주의할 점

1. 너무 많은 속성과 요소에 will-change 속성을 사용하지 않습니다.
 - 브라우저는 모든 요소에 대해 이미 최적화를 시키려고 시도하고 있습니다. will-change 속성이 사용된 요소는 최적화를 하기 위해 많은 자원을 소모하기 때문입니다.

2. 애니메이션 동작이 끝난 후 기본 상태로 되돌려야 합니다.
 - 브라우저가 변화에 최적화를 시도하면 일반적으로 비용이 발생합니다. 브라우저는 보통 필요한 경우에 최적화를 실시하고 최적화가 필요가 없으면 다시 원래되로 되돌아 옵니다. 하지만 will-change의 경우는 최적화를 길게 유지하게 됩니다. 그러므로 엘리먼트에 변경이 종료되면 반드시 will-change를 삭제해야 합니다. 그러면 will-change에 사용하고 있던 자원을 회수할 수 있습니다.

```js
// 간단한 예제
// 클릭할 때 애니메이션을 재생할 엘리먼트를 선택합니다.
var el = document.getElementById('element');

// 엘리먼트에 마우스 커서가 올라가면 will-change를 설정합니다.
el.addEventListener('mouseenter', hintBrowser);
el.addEventListener('animationEnd', removeHint);

function hintBrowser() {
    // 애니메이션의 키프레임 블럭을 최적화할 수 있는 속성을 사용합니다.
    this.style.willChange = 'transform, opacity';
}

function removeHint() {
    this.style.willChange = 'auto';
}
```
단, 슬라이드처럼 수초 내에 반드시 변화가 일어나거나 마우스 움직임에 따라 변화가 일어나는 경우는 자바스크립트로 will-change로 삭제하지 않고 스타일시트에 바로 선언해도 문제 없습니다.

```css
.slide {
    will-change: transform;
}
```

3. 조금 더 빨리 적용하려고 will-change를 사용해서는 안 됩니다.
 - will-change를 사용하지 않아도 페이지가 잘 작동된다면 will-change를 사용하지 않아도 됩니다. 조금 더 빨리하기 위해 will-change 속성을 추가하면 과도한 메모리 사용과 더 복잡한 렌더링으로 성능이 더 안좋아 질 수 있습니다.

4. 브라우저에게 미리 will-change 사용을 알려주어야 합니다.
 - 변화가 일어날 요소에 will-change를 직접 선언하면 적용이 되지 않습니다.
 - 그러므로 선택자 :hover, 자바스크립트 mouseenter 등을 통하여 미리 알려주어야 합니다.

```css
/* hover를 통해서 will-change를 선언 했으므로 적용 */
.box:hover {
    will-change: transform;
}
.box {
    transition: transform 1s linear;
}
.box:active {
    transform: rotate(180deg);
}
```



