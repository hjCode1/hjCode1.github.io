---
layout: post
title:  extend 대신 mixin 사용하기
date:   2019-07-05
tag:
- sass


---

## Sass에서 extend대신 mixin을 사용하자

#### @extend를 언제 사용해야 할까?

@extend가 연관성을 형성한다는 것을 이해해야 한다.
```css
%brand-font {
    font-family: webfont, sans-serif;
    font-weight: 700;
}

h1 {
    @extend %brand-font;
    font-size: 2em;
}

.btn {
    @extend %brand-font;
    display: inline-block;
    padding: 1em;
}

.promo {
    @extend %brand-font;
    background-color: #BADA55;
    color: #fff;
}

.footer-message {
    @extend %brand-font;
    font-size: 0.75em;
}
```
이 코드를 컴파일 하면 아래처럼 된다.
```css
h1, .btn, .promo, .footer-message {
    font-family: webfont, sans-serif;
    font-weight: 700;
}

h1 {
    font-size: 2em;
}

.btn {
    display: inline-block;
    padding: 1em;
}

.promo {
    background-color: #BADA55;
    color: #fff;
}

.footer-message {
    font-size: 0.75em;
}
```

위 코드의 문제점은 연관성없는 규칙들에 강제로 연관성을 부여했다는 점이다. 그리고 반복을 피하려고 작성한 @extend로 인해 파일 용량도 더 커진다.

그렇다면 언제 @extend를 사용해야 할까?

다음은 좋은 예다.

```css
.btn,
%btn {
    display: inline-block;
    padding: 1em;
}

.btn-positive {
    @extend %btn;
    background-color: green;
    color: white;
}

.btn-negative {
    @extend %btn;
    background-color: red;
    color: white;
}

.btn-neutral {
    @extend %btn;
    background-color: lightgray;
    color: black;
}
```

아래는 컴파일한 결과이다.

```css
.btn,
.btn-positive,
.btn-negative,
.btn-neutral {
    display: inline-block;
    padding: 1em;
}

.btn-positive {
    background-color: green;
    color: white;
}

.btn-negative {
    background-color: red;
    color: white;
}

.btn-neutral {
    background-color: lightgray;
    color: black;
}
```

#### @mixin을 사용할 때

프로젝트에서 특정한 글꼴을 사용하고 있다고 생각해 보자. 이 글꼴에는 언제나 font-weight를 정의해야 한다.

```css
.foo {
    font-family: webfont, sans-serif;
    font-weight: 700;
}

.bar {
    font-family: webfont, sans-serif;
    font-weight: 700;
}

.baz {
    font-family: webfont, sans-serif;
    font-weight: 700;
}
```

코드에서 두 선언을 수동으로 한없이 반복하는 것은 아주 지루한 일일 것이다. 게다가 익숙한 regular나 bold가 아니라 700이라는 숫자를 기억해야만 한다.
만약 웹 폰트 종류나 굵기를 변경해야 한다면, 우리는 프로젝트 전체를 훑으면서 위 선언을 전부 찾아내 바꿔야 한다.
이럴 때 @extend를 이용해 강제로 연관성을 부여하는 것은 하면 안 된다는 점을 앞서 다뤘다. 해야 할 일은 믹스인을 사용하는 것이다.

```css
@mixin webfont() {
    font-family: webfont, sans-serif;
    font-weight: 700;
}

.foo {
    @include webfont();
}
```

위 규칙들은 서로 연관성이 없는 규칙들이고, 그래서 연관을 맺게 만들지 않았다는 점을 기억하는 것이 여기서 중요하다.

믹스인은 반복되는 구조를 가진 동적인 값을 생성할 때 정말 정말 유용하다. 인자값이 있는 믹스인 말이다. 그 누구도 이게 별로라고 말하지 못할 것이다.

```css
@mixin truncate($width: 100%) {
    width: $width;
    max-width: 100%;
    display: block;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
}

.foo {
    @include truncate(100px);
}
```

같은 선언을 뱉어 내지만, 경우에 따라 동적으로 width를 설정한다.

이것은 가장 일반적이고 널리 합의된 믹스인 형태고, 모두가 이걸 좋은 방법이라고 생각할 것이다.

#### 요약

같은 주제로 묶여 있을때만 @extend를 사용하자.
그냥 같을 뿐이라면 @mixin을 사용하자.


[출처사이트로 이동](https://mytory.net/2016/12/23/when-to-use-extend-when-to-use-a-mixin.html)