---
layout: post
title:  Rendering
date:   2019-04-17
tag:
- Rendering


---

## 브라우저 렌더링 과정

1. 불러오기
로더(Loader)가 서버로부터 전달 받는 리소스 스트림을 읽는 과정.
읽으면서 어떤 파일인지, 데이터인지 파일을 다운로드할 것인지 등을 결정한다.

2. 파싱 (Phasing)
웹 엔진이 가지고 있는 HTML/XML 파서가 문서를 파싱해서 DOM Tree를 만든다.

3. 렌더링 트리 만들기
DOM Tree는 내용을 저장하는 트리로 자바스크립트에서 접근하는 DOM객체를 쓸 때 이용하는 것이고 별도로 그리기 위한 트리가 만들어져야 하는데 그것이 렌더링 트리다. (그릴 때 필요없는 head, title, body태그등이 없음 + display:none 처럼 DOM에는 있지만 화면에서는 걸러내야할 것들을 걸러냄)

4. CSS 결정
CSS는 선택자에 따라서 적용되는 태그가 다르기 때문에 모든 CSS 스타일을 분석해 태그에 스타일 규칙이 적용되게 결정한다.

5. 레이아웃
렌더링 트리에서 위치나 크기를 가지고 있지 않기 때문에 객체들에게 위치와 크기를 정해주는 과정을 레이아웃이라고 함.

6. 그리기
렌더링 트리를 탐색하면서 그리기.
참고로 렌더링 엔진은 가능하면 HTML문서가 파싱될 때까지 기다리지 않고, 배치와 그리기 과정을 시작한다.

### CSS와 Script 위치
웹브라우저의 렌더링 순서를 이해하면 이해가 가는 말이다.

문서를 파싱해서 DOM Tree를 만들어도 스타일 규칙이 없으면 렌더링 할 수가 없다.

즉, 최대한 빨리 스타일 규칙을 알아야 렌더링트리가 완전히 만들어지므로 스타일시트 파일을 모두 다운로드시키기 위해 <head></head>태그 사이에 놓는 것이다.

자바스크립트는 왜 아래에 놓아야 성능이 좋아질까?

자바스크립트는 DOM객체를 이용해서 컴포넌트들을 조작하는데 <head></head>태그 사이 처럼 상단에 놓게 되면 HTML파서가 파싱을 멈추고 스크립트파일을 읽기 때문이다.

파싱을 멈추고 읽기 때문에 위에서 스크립트파일이 많거나 파일이 크면 읽는 시간이 오래걸려 사용자 입장에서 웹페이지가 느리게 보이게 되므로 느리다고 느낄 수 있다.

심지어 잘 못 코딩했을 경우 HTML 파싱보다 자바스크립트 파일이 먼저 실행되서 적용이 안되는 모습도 볼 수 있다.

따라서 일반적으로 </body>태그 위에 스크립트를 모아둔다.

이렇게 하다보면 자바스크립트 애니메이션같은 것이 늦게 적용되서 처음 웹페이지를 들어갔을 때 아주 잠깐 다른 웹페이지가 보이다가 애니메이션이 적용되는 것을 볼 수 있는데, 이런 부분은 감안하는 방법이 있고, 애니메이션 관련된 부분만 <head></head>태그 사이로 올려서 적용하는 방법이 있다.

### 간단한 최적화 팁

- 애니메이션이 들어간 노드는 positon:fixed 또는 position:absolute로 지정한다.
애니메이션은 엄청난 Layout 비용이 들어간다. 이 때 absolute나 fixed로 전체 레이아웃과 분리해주면 애니메이션이 필요한 노드만 계산하게 된다.
그렇지 않을 경우 무든 노드들을 재계산 해야하기 때문에 아주 많은 비용이 들어 느려지게 된다.

- 동일 요소에 스타일 변경은 가급적 한번에 처리한다.

```js
function changeDivStyle(){
    var sampleEl = document.getElementById("sample");
        sampleEl.style.cssText = 'background:blue; width:200px;height:50px;';
}
changeDivStyle();
```


[참고사이트](https://jeong-pro.tistory.com/90)
https://jeong-pro.tistory.com/90
