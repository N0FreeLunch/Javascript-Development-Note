## '웹펙'이란 무엇인가?
- 웹 브라우저에서 실행되는 JS 파일을 만들기 위한 nodejs 컴파일러
- 웹펙의 컴파일을 트랜스파일이라고 부른다.

## '트랜스파일'이란?
- 노드 JS에서 작성한 자바스크립트를 웹브라우저에서 동작하는 자바스크립트로 바꿔준다.

## 왜 컴파일 방식을 사용할까?
- 작성한 코드를 여러 툴들로 변형해서 퍼블리싱을 해야 할 경우
- 브라우저에서 지원이 미비한 최신 ECMA 표준을 사용해서 개발한 코드를 대부분의 브라우저에서 문제 없이 동작 시키기 위해서

### 하나의 파일로 빌드
- 가독성을 위해 여러 자바스크립트 파일에 코드를 분리하는 경우가 많다.
- 여러 자바스크립트 파일을 사용하면 통신을 여러 번 하게 되기 때문에 스크립트 다운로드 속도가 늦어진다.
- 웹펙을 사용하면 분할 된 자바스크립트 파일을 하나로 합쳐 준다.
- 전송 시 통신 횟수를 줄이기 때문에 초기 로딩 속도를 향상 시킬 수 있다.

### 실시간 빌드
- 웹펙의 watch 모드를 사용하면 코드 하나를 수정하고 저장을 할 때마다 새롭게 파일이 빌드된다.
- 이전의 babel과 같은 도구는 ES6 이상의 문법을 ES5 문법으로 바꿔주는 역할을 했지만 CLI 명령어를 사용해서 변경을 해야 했다. 하지만 웹펙을 사용하면 실시간으로 이런 변경이 가능하다. 구버전 브라우저에서 바로바로 변환 결과를 확인할 수 있다.
- 조금 수정을 한 후 CLI 명령어를 사용하여 빌드할 필요가 없으며, 빌드 된 상태에서의 결과를 확인할 수 있도록 만들어 준다.

### 전역 공간 오염 방지
- 전역 공간의 변수 충돌을 방지할 수 있다. (다른 자바스크립트 파일과의 전역 선언된 변수와의 충돌을 방지할 수 있다.)

### 플러그인 사용가능
- 코드 난독화
- 코드 압축
- ES6 이상의 문법을 ES5 문법으로 바꿔주는 babel 플러그인
- CSS, SASS 파일을 자바스크립트에서(import require 키워드로) 로딩할 수 있게 해 주는 플러그인
- 리액트를 사용할 때 JSX 문법을 자바스크립트 코드로 바꿔주는 플러그인 등등

### 패키지 관리
#### 다른 자바스크립트 패키지를 사용하여 개발되는 라이브러리
- 라이브러리 자체도 다른 라이브러리의 기능들을 사용하여 개발되는 경우가 많다.
- 여러 라이브러리를 로딩한다고 할 때, 사용하는 여러 라이브러리들이 중복되는 라이브러리를 사용하여 개발 된 경우 웹펙을 사용하지 않는다면 따로 로딩을 해야 한다.
- 웹펙을 사용하면 동일한 버전의 패키지의 경우 중복으로 로딩을 하지 않도록 웹펙이 조정해 준다. 하나의 패키지의 하나의 소스를 여러 라이브러리에서 이용할 수 있도록 조정하는 기능을 한다.

#### 패키지 버전 관리
- 자바스크립트 라이브러리는 대개 용량이 큰 경우가 많다.
- 이렇게 패키지의 크기가 큰 이유는 다양한 라이브러리들을 끌어와서 사용하여 개발한 경우가 많기 때문이다.
- 하나의 패키지는 다양한 버전으로 존재한다. 패키지의 개발자는 지속적으로 패키지 버전을 업데이트 한다. 버그가 픽스될 수도 있고 새로운 기능이 추가 될 수도 있으며 기존 기능을 사용하지 못하는 경우도 생긴다. 사용하는 패키지의 버전을 명시해서 버전별로 다운받아 호환성 문제를 최소화 한다.

## commonJS
- commonJS란 노드JS가 개발되었을 때 처음 사용된 개념으로 import, require 등의 키워드를 통해서 다른 js 파일을 불러 올 수 있도록 하는 기능이다.
- 예전 브라우저에서는 import, require 등의 문법을 지원하지 않았기 때문에 다른 자바스크립트 라이브러리를 전역적으로 로드할 수 밖에 없었으며 각 라이브러리의 하나의 기능만 사용을 하려고 해도 라이브러리 전체를 로딩하거나 쓰는 파일만 로드 해야 하는 등의 불편함이 있었다.
- 최신 브라우저에서는 import, require 등의 문법을 지원하기 때문에 이런 불편함이 줄어들었지만, 이는 도입된지 몇 년 되지 않은 문법이다. (https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Modules)
- wepback을 사용하면 오래된 버전의 브라우저에 대해서도 import, require 등의 문법을 사용한 개발을 할 수 있다.

### commonJS를 사용해야 하는 이유
#### 의존성 트리 쉐이킹
- https://webpack.kr/guides/tree-shaking/
```
export function square(x) {
  return x * x;
}

export function cube(x) {
  return x * x * x;
}
```
- ./math.js 파일


```
import { cube } from './math.js'

```
- 위 코드를 사용해서 cube만 사용하고 square을 사용하지 않을 경우
- 웹펙으로 빌드한 파일에는 cube 코드만 들어간다.
- 라이브러리에서 필요하지 않은 모듈을 로딩하지 않는 방식을 통해 웹펙 번들의 용량을 줄일 수 있다.
- 하지만 브라우저에서 사용을 하게 되면 코드 일부가 아닌 파일을 로드하게 되므로 완전한 commonJS 기능을 사용할 수 없어서 웹펙보다 효율적이지 못하다.


## 웹펙을 사용하고 있는 분야
- Laravel의 mix
- React create app 명령어를 통한 설치
- Vue CLI를 통한 설치


## 웹펙 설치
- https://webpack.kr/guides/getting-started/
1. nodejs version 10 이상 필요
2. 터미널에서 웹펙을 설치하고자 하는 경로로 이동한다.
3. `npm init -y`
4. `npm install webpack webpack-cli --save-dev`
5. `mkdir src`
6. `touch src/index.js`
7. `npx webpack`
- src 폴더 내에 index.js가 웹펙으로 빌드되어 dist 폴더의 main.js 파일로 번들링된다.

## 웹펙 세팅하기
- https://webpack.kr/configuration/
### webpack.config.js 파일 만들기
- https://webpack.kr/configuration/#options 에서 webpack.config.js의 설정을 복사한다.
- 프로젝트 폴더에 webpack.config.js 파일을 만들어 복사한 내용을 붙여 넣는다.

### 손쉬운 세팅
- 웹펙을 설정할 때 이것저것 패키지를 설정하는 것이 어려울 수 있기 때문에 기본적인 패키지를 자동으로 설치해 주는 명령어가 존재한다. `npm install @webpack-cli/generators --save-dev`
- 자동 설치 명령어`npx webpack-cli init`를 실행하면 다음 플러그인 및 설정들이 자동으로 만들어진다.
```
? Which of the following JS solutions do you want to use? ES6
? Do you want to use webpack-dev-server? Yes
? Do you want to simplify the creation of HTML files for your bundle? Yes
? Do you want to add PWA support? Yes
? Which of the following CSS solutions do you want to use? SASS
? Will you be using CSS styles along with SASS in your project? Yes
? Will you be using PostCSS in your project? No
? Do you want to extract CSS for every file? No
? Do you like to install prettier to format generated configuration? Yes
```
- `npm run build`로 설치에 문제가 없는지 확인하기

## webpack.config.js 파일 세팅하기
- https://webpack.kr/concepts/

### 빌드할 파일 선택하기
```
const config = {
    entry: './src/index.js',
    output: {
        path: path.resolve(__dirname, 'dist'),
    },
    ...
```
- `./src/index.js` 경로의 파일을 dist 폴더에 동일 이름의 파일으로 빌드한다는 의미
- [entry](https://webpack.kr/concepts/#entry) 작성한 자바스크립트 파일이 위치하는 곳, [output](https://webpack.kr/concepts/#entry)은 빌드된 자바스크립트 파일이 위치하는 곳

### watch 명령어로 개발하기
```
npm run watch
```


## 여러 파일 세팅하기
```
entry: {
  "index" : "./src/index.js",
  "test" : "./src/test.js"
},
```
- key는 아웃풋 파일 이름, value는 작성한 자바스크립트 코드
