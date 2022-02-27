# Lazy Loading
- 지연 로딩은 여러 개념으로 사용된다. 그 중에서도 웹 프로그래밍에서 지연 로딩은 서버의 ORM에서의 지연로딩과 프론트앤드의 HTML에서 호출하는 여러 파일에 대한 로딩을 가리킨다.

## 백앤드에서의 지연 로딩
- 주로 백앤드에서는 ORM을 사용할 때 eager loading과 lazy loading을 구분해서 쿼리의 결과 리스트를 가져올 때, 리스트의 일부 또는 단일 결과값에 연관된 데이터에 대한 쿼리를 한 번 더 날리기 위해 lazy loading을 사용한다. lazy loading은 쿼리의 결과 리스트 하나하나에 대해 쿼리를 날리는 방식이고 eager loading은 미리 결과 리스트에 대한 연관 데이터를 모두 한꺼번에 가져오는 방식이다. 가져와야 할 결과 리스트의 크기가 크다면 eager loading 보다는 lazy loading을 사용하는 것이 DB의 리소스에 부담을 적게 주고 백앤드 애플리케이션의 메모리 절감을 할 수 있는 전략이다. 물론 데이터의 크기가 작다면 한꺼번에 빠르게 데이터를 가져올 수 있고 여러번 나눠서 쿼리를 날리는 것 보다 단일 또는 소수의 쿼리로 데이터를 가져오는 eager loading이 더 나을 때도 있다.

## 프론트앤드에서의 지연 로딩
- 프론트엔드에서 보통 lazy loading이라고 하면 브라우저가 초기 랜더링 될 때가 아니라, 랜더링 된 이후 브라우저의 이벤트 발생을 통해서 로딩을 한다는 의미이다.
- 보통 프론트앤드에서 로딩이라고 하면 통신을 통해서 가져오는 데이터의 lazy loading을 의미한다. 물론 Lazy Loading의 개념에는 자바스크립트 자체의 갑작스런 리소스 소모를 줄이기 위해서 코드의 실행을 나중에 실행한다는 개념도 포함한다.
- lazy loading의 대상은 이미지 뿐만 아니라, CSS 파일, 자바스크립트 파일 등 파일 로딩 뿐만 아니라 자바스크립트 코드까지 포함될 수 있다.

## Lazy Loading을 사용하는 이유
- 예를 들어 웹 페이지에 사진이 엄청 많이 로딩 된다고 하자. 페이지 상단에 보여 줄 이미지를 로딩을 하는데, 페이지 하단의 이미지를 로딩하기 위해서 페이지 상단의 이미지 로딩이 지연된다고 생각해 보자. 유저 경험(UX)적인 측면에서 불편함을 주게 된다. 그래서 페이지의 이미지를 로딩할 때 페이지 상단의 이미지부터 로딩 될 수 있도록 하는 편이 좋고, 가능하다면 맨 윗 라인 부터 차례로 로딩되게 하는 것이 좋다.

### HTTP와 HTTP2
- 서버에서 클라이언트와 HTTP로 통신하는 프로토콜은 크게 2가지 방식이 있다. 하나는 HTTP이고 다른 하나는 HTTP2이다.
- 일단 서버와 클라이언트 간의 커넥션은 1개라는 사실에 유념하자. TCP 통신 베이스의 1 커넥션이다.
- HTTP 방식의 경우 통신이 동기 방식이다. 하나의 요청이 서버로 보내졌을 때 서버가 클라이언트에 리스폰스를 주기 전까지 다른 요청들은 블락된다. 따라서 페이지 아래쪽에 있는 이미지가 먼저 로딩이 되어 버리면 페이지 윗쪽의 이미지는 계속 요청이 지연되고 리스폰스가 늦어지게 된다. 이는 서버와 클라이언트 간의 커넥션이 하나이기 때문에 발생한다.
- HTTP2 방식의 경우는 통신이 비동기 방식이다. 서버와 클라이언트 간의 커넥션이 하나라도 여러 요청이 서버로 보내졌을 때 서버는 동시에 이 요청들을 처리한다. 페이지 아래쪽의 이미지가 먼저 로딩이 된다고 하더라도 페이지 위쪽 이미지도 동시에 로딩이 될 수 있기 때문에 특별한 문제가 되지 않는다. 하지만 서버의 트레픽은 제한되어 있는 경우가 있고, 트레픽 제한이 있는 서버에서는 HTTP2 방식을 쓴다고 하더라도 리스폰스의 지연이 생기는 경우가 있다. 이런 트레픽 제한의 문제를 해결하기 위해 CDN 서버를 사용할 때도 있다.
- 또한 서버의 페이지에 로딩되는 추가 파일들 이미지, CSS, JS 파일이 Nginx, Apache 등에서 static 컨텐츠 설정이 되어 있지 않다면 웹 애플리케이션(WAS)에서 데이터를 보내줘야 하기 때문에 지연이 일어날 수 있다. WAS가 동시에 처리할 수 있는 양은 제한 되어 있고 이 제한 때문에 다수의 사용자가 한 꺼번에 많은 컨텐츠를 요청하면 WAS에 무리가 갈 수 있다. 물론 비동기 서버인 NodeJS 같은 경우에는 빠르게 처리할 수도 있을 것 같다.

## 바인딩
- 바인딩 된다는 말은 마치 원본 문맥에 들어 있는 것 처럼 집어 넣는다는 의미이다.
- HTML 문서를 브라우저에서 실행할 때 바인딩 된다는 말은 말 그대로 HTML 문서를 실행할 때 마치 HTML 문서에 존재하는 텍스트인 것처럼 실행하여 로딩 된다는 것이며
- JS 코드를 실행할 때 바인딩 된다는 말은 원본 JS 파일에 들어 있는 코드를 실행하는 것 처럼 외부에서 코드를 받아와서 실행한다는 의미이다.

#### 문자열 바인딩
`"select * from sampleTable where id = ?".replace("?", "1")`이란 코드를 보자. ?에 1을 집어 넣게 되면 `"select * from sampleTable where id = ?"`라는 문자열이 `"select * from sampleTable where id = 1"`이란 문자열로 변한다. 원본의 특성을 그대로 유지하면서 안의 컨텐츠만 외부의 다른 것으로 바꾸거나 추가하는 것을 바인딩이라고 한다.

#### 자바스크립트 태그 바인딩
- 자바스크립트 태그는 HTML 문서를 실행할 때 외부 자바스크립트를 브라우저의 HTML 실행 컨텍스트 안에 집어 넣는 것을 의미한다. 곧 스크립트 태그는 HTML 실행 컨텍스트 내에서 바인딩된다.

#### Import를 통한 바인딩
- 자바스크립트 코드에서 외부의 자바스크립트를 실행 컨텍스트안에 집어 넣어서 실행한다. 곧 외부 자바스크립트 코드는 JS 실행 컨텍스트 내에서 바인딩된다.

## 정적로딩과 동적로딩
- static loading 이란 말은 항상 로딩한다는 의미이다. 때와 상황에 관계 없이 페이지에서 항상 로딩 되는 자바스크립트를 정적 로딩되는 자바스크립트라고 한다. 이와 반대로 조건에 따라 스크립트가 로딩되고 로딩되지 않을 경우를 정해서 로딩되는 것을 동적로딩이라고 한다.

### 정적로딩
- 일반적으로 import를 통해서 외부 JS 코드를 실행하는 것은 정적로딩으로 이뤄진다. 정적 로딩에서는 import로 불러온 자바스크립트 파일의 모든 코드가 평가(실행)된다.
- 로드하는 모듈의 크기가 크고 모듈의 양이 많아질수록 코드의 로딩이 느려지고 메모리 사용량이 증가한다. 

### 동적로딩
- 로드하는 모듈이 초기 로딩 후 바로 사용하는 것이 아니라면 바로 로딩할 필요가 없다. 나중에 사용할 때 로딩하여 초기 로딩의 부담을 경감하는 방식으로 사용한다.
- 모듈의 존재 유무가 확실하지 않을 때 또는 모듈에 문제가 있을 가능성이 있는 경우에 이에 대한 예외 처리를 하기 위한 방식으로 동적으로 구현할 수 있다.

### 동적로딩은 필요할 때만 사용하자.
- 정적 로딩을 해야 정적 분석 도구를 사용하기 쉽고 트리 쉐이킹의 이점을 얻기 쉽다. 동적 로딩을 사용하면 이런 이점을 누릴 수 없음 (참고로 정적 분석 도구로는 eslint가 유명함)
- 트리쉐이킹은 동일 모듈을 사용하는 서로 다른 모듈을 로딩하는 경우, 로딩하는 서로 다른 두 모듈에서 공통으로 사용하고 있는 모듈의 중복 로딩을 줄여주는 기능을 한다.

## Lazy Loading의 구현
### 이미지 및 iframe
```
<img src="image.jpg" alt="..." loading="lazy">
<iframe src="video-player.html" title="..." loading="lazy"></iframe>
```
- 태그에 loading 어트리뷰트에 lazy 프로퍼티를 설정할 때 브라우저의 스크롤이 대상 태그에 가까이 갔을 때 브라우저가 알아서 lazy 로딩 처리를 해 준다. 곧 화면 밖에 있는 대상이 아직 읽히지 않았을 경우 이 태그를 적용한 대상은 레이지 로딩이 된다.
- 지연 로딩의 경우 이미지가 이벤트 발생 시점에서 로딩되기 때문에 늦어지는 경우가 생길 수 있다. 따라서 레이지 로딩을 하는 순간에 잠시 데이터를 받아오는 시간 때문에 이미지나 iframe이 보이지 않을 수도 있다. 로딩 여부를 브라우저로 체크하기 위해서는 [`htmlImageElement.complete;`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/complete) 구문을 사용하자.
- 브라우저의 지원 사항은 다음을 참고하자. 구버전의 브라우저의 경우 지원하지 않을 수 있다. (지원 여부 : https://caniuse.com/loading-lazy-attr) 이 경우 다음 자바스크립트 [lazy loading 폴리필](https://github.com/mfranzke/loading-attribute-polyfill)을 사용하여 구 버전 브라우저에 폴리필을 지원할 수 있다. 폴리필을 사용하는 것이 표준이므로 라이브러리 보다는 공식 폴리필을 사용하도록 하자.
- 브라우저 지원 여부가 문제라면 자바스크립트를 사용해서 지연 로딩이 되도록 lazy 로딩 시점이 되었을 때 브라우저 이벤트 안에 스크립트로 이미지 태그를 만들어 집어 넣는 방식을 사용할 수도 있다.

### CSS의 경우
```html
<link href="style.css"    rel="stylesheet" media="all">
<link href="portrait.css" rel="stylesheet" media="orientation:portrait">
<link href="print.css"    rel="stylesheet" media="print">
```
- CSS의 경우 기본적으로 브라우저에서 지원하는 lazy loading은 CSS 파일을 불러오는 link 태그의 media 속성 부분에 정의할 수 있는 이벤트 종류이다.
- `media="orientation:portrait"`의 경우 화면의 방향이 세로일 경우에만 적용되는 CSS 이며, `media="print"`의 경우는 브라우저에서 'ctrl + p' 등으로 프린터 옵션을 사용할 때 적용되는 CSS이다.
- media 어트리뷰트에 지정할 수 있는 이벤트가 발생했을 때 실행되도록 동작시킬 수 있다.

#### JS로 CSS로딩하기
```js
var dynamicLoadCss = function (cssPath) {
  var cssElement = document.createElement('link');
  cssElement.setAttribute('href', cssPath);
  cssElement.setAttribute('rel', 'stylesheet');
  cssElement.setAttribute('type', "text/css");
  document.head.appendChild(cssElement);
})
```
- 자바스크립트로 태그를 로딩하면 자바스크립트로 태그를 브라우저에 로딩한 시점에서 내부의 태그의 실행이 결정된다.
- 굳이 head 태그에 넣지 않아도 CSS 태그는 동작한다.

### JS의 경우
#### 엔트리 포인트 분리 (Entry point splitting)
- 페이지 마다 로딩되는 것을 방지하고, 한번 로딩된 자바스크립트나 CSS 파일을 캐싱하여 여러 페이지에서 사용하기 위해 여러 페이지에서 쓰이는 자바스크립트 또는 CSS 파일을 하나의 파일에 정의하는 방식으로 사용할 수도 있다. 이 경우 페이지 별로 파일을 다운로드 받지 않고 캐싱된 것을 이용하기 때문에 웹 사이트의 어떤 페이지에서의 초기 로딩 속도는 늦지만 다른 페이지의 로딩속도는 향상되는 효과를 얻을 수 있다.
- 하지만 이 경우 초기 로딩에서 필요 없는 자바스크립트 파일도 받기 때문에 초기 로딩 속도가 굉장히 느려지는 문제가 발생하게 된다. 따라서 페이지 별로 필요한 자바스크립트 파일을 분리하는 방식을 사용하도록 한다.

#### 스크립트 동적 로딩
- 자바스크립트 태그를 동적으로 로딩하는 방식이다.
```js
var loadJs = function (jsPath) {
  var jsElement = document.createElement('script');
  jsElement.setAttrubute('src', jsPath);
  return jsElement;
}

targetElmenet.appendChild(loadJs('js path or url'));
```
- 특정 조건일 때 JS 파일을 로드할 때 사용한다. JS 태그를 브라우저의 노드에 넣는 시점에서 동적으로 로드된 JS 파일이 실행된다. 이는 비동기적 스트립트 실행으로 스크립트가 로딩 되는 즉시 실행이 된다.
- 단, 이때 innerHTML 또는 outerHTML를 사용하면 스크립트가 실행되지 않는다.
- 태그를 자바스크립트로 동적으로 집어 넣으면 태그에 async 옵션을 넣은 것과 같은 효과를 가진다.
```
<script src="JS path or url" async>
</script>
```
- async 태그를 스크립트에 쓰면 스크립트가 로딩 되는 즉시 실행이 되는데 이것과 동일한 역할을 스크립트 태그를 js로 만들어 브라우저에 넣을 때 적용된다.
- 브라우저는 HTML 문서를 먼저 파싱을 한 뒤, 파싱된 형태의 코드를 순차적으로 읽는 방식으로 실행한다. async 속성은 HTML 문서가 모두 브라우저에 의해 파싱 되고 나서 스크립트를 실행하는 것이 아닌, 파싱 되는 시점에서 코드를 실행한다.

#### 다이나믹 import를 사용한다.
```js
(async () => {
  if (somethingIsTrue) {
    // import module for side effects
    await import('/modules/my-module.js');
  }
})();
```
```js
(async () => {
  if (somethingIsTrue) {
    const { default: myDefault, foo, bar } = await import('/modules/my-module.js');
  }
})();
```
```js
import('/modules/my-module.js')
  .then((module) => {
    // Do something with the module.
  });
```
```js
let module = await import('/modules/my-module.js');
```
- 다이나믹 import는 promise 타입을 사용하기 때문에 promise에 대한 지식이 필요하다.
- import 문법을 사용하기 위해서는 로드하는 자바스크립트 파일이 `module` 문법을 사용한 모듈 형태의 구성이 되어야 한다.
- dynamic import에 대한 지원은 오래된 브라우저에서 동작하지 않을 수 있으므로 확인이 필요하다. (https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/import)

### 웹펙의 경우
- 웹펙 설정의 [dynamic-entry](https://webpack.kr/configuration/entry-context#dynamic-entry) 부분을 참고한다.
```js
entry: () => new Promise((resolve) => resolve(['./demo', './demo2'])),
```
```js
entry: () => './demo',
```
```js
module.exports = {
  entry() {
    return fetchPathsFromSomeExternalSource(); // ['src/main-layout.js', 'src/admin-layout.js']와 같이 해석할 promise를 반환합니다.
  },
};
```
- 웹펙의 경우도 내부적으로 import 구문을 사용하기 때문에 구형 브라우저에서 사용하기 위해서는 import 폴리필을 웹펙에 설치해 줘야 한다. import 폴리필은 브라우저에서 직접 지원하는 것은 없는 것 같고, webpack을 통해서 실행할 수 있는 패키지는 있는 것 같다.

### react, angular, vue
- 각각 프레임워크에서 권장하는 방식이 있다.
- react : https://reactjs.org/docs/code-splitting.html
- vue : https://vuedose.tips/dynamic-imports-in-vue-js-for-better-performance
- angular : https://angular.io/guide/router#milestone-6-asynchronous-routing or https://medium.com/@var_bin/angularjs-webpack-lazyload-bb7977f390dd

## Reference
- https://developer.mozilla.org/en-US/docs/Web/Performance/Lazy_loading
- https://webpack.js.org/guides/lazy-loading/
- https://webpack.kr/guides/lazy-loading/
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import
- https://webpack.kr/configuration/entry-context#dynamic-entry
- https://developer.mozilla.org/en-US/docs/Web/API/HTMLScriptElement#dynamically_importing_scripts
