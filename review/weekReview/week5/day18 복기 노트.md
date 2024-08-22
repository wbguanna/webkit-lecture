
오늘 한 것은 \[ Node.js \]

### Node.js 에서 쓰면 스크립트 태그에서 쓰는거랑 뭐가 다를까?

브라우저에서 쓰던 js 와 다른점은 어떤 점이 있을까?
기본적으로 node js는 DOM 요소와 Window 객체를 모른다
v8엔진으로 js만 사용하기 때문이다

https://medium.com/@jonbiro/browser-engines-chromium-v8-blink-gecko-webkit-98d6b0490968

![[Pasted image 20240822011742.png]]
그림 용어에 대한 간략 설명
- Chromium : 
	- 오픈소스 웹 브라우저 및 운영체제 계열 프로젝트라고 한다. 
	- 웨일이나 삼성인터넷도 포함
- Blink : 
	- chromium 의 렌더링 엔진이라 한다. 
	- 웹 표준에 맞춰 DOM, CSS, Web IDL(?) 등을 적용시킨다고 한다. 
	- js 엔진도 이용한다. (전에는 webkit, 지금은 v8 엔진을 쓴다한다.)
	- 렌더링(style, layout 적용)이니 만큼 HTML, CSS 각 문서를 파싱한다
	- 번역이 바로 안돼 못 읽었지만 관심이 있다면 아래 페이지를 읽어도 좋을 것 같다
	- https://docs.google.com/document/d/1aitSOucL0VHZa9Z2vbRJSyAIsAz24kX8LFByQ5xQnUg/edit
	- 외에 Gecko, Webkit, 트라이던트?,
- webkit : 
	- apple 에서 발표한 브라우저 엔진(js 엔진)
	- KHTML 엔진에서 파생되었다고 한다
	- 앞서 말한 크로미움도 블링크로 분기하기 전에 사용했다고 한다
	- https://namu.wiki/w/WebKit#s-2
- v8 :
	- 구글에서 c++기반으로 개발한 오픈소스 js 엔진(인터프리터)
	- Node.js 와 Deno Electron 프레임워크, 크롬+edge+opera 등 브라우저에 사용 된다고한다.

Node.js 는 v8 + libuv(비동기 이벤트 처리 라이브러리?) 라고 한다. 

그래서 Node.js 의 특징을 살펴보면서 어떤 건지 알아보자

### Promise 와 node.js 실행순서
수업에서의 Promise 예제를 보자
``` js 
/ex01_promise.js
function task1(fulfill, reject) {
  console.log("1. Task1 시작");
  let num = 0;
  setTimeout(function () {
    num = 1004;
    fulfill("Task1 결과", num);
  }, 300);
  console.log("2. Task1 끝", num);
}

function fullfilled(result, num) {
  console.log("fullfilled 함수", result, num);
}

function rejected(err) {
  console.log("rejected : ", err);
}

new Promise(task1).then(fullfilled, rejected);

```
보통 생각하는 호출 스택대로 