# Rollup CSS 번들링 

[시작하기](rollup-01-get-started.md)에 이어서, 이 번에는 CSS를 번들링을 해보자.


## 기본 플러그인 먼저 설치 
CSS와는 관계가 없지만 기본적으로 필요한 플러그인들을 먼저 설치한다. 

먼저, Node.js 모듈의 경로를 파악하는 plugin-node-resolve와 es6로 변환을 위해 commonjs를 설치한다. 

```
npm install -D  @rollup/plugin-node-resolve
npm install -D  @rollup/plugin-commonjs
```
* rollup-plugin-node-resolve:  외부 노드 모듈을 사용시 (node_modules 디렉토리)
* rollup-plugin-commonjs : 외부 노드 모듈이 es6 으로 변환되지 않았을 경우 es6 으로 변환

다음으로 package.json의 설정을 읽을 수 있도록 plugin-json을 설치한다. 
```
npm install -D @rollup/plugin-json
```


## CSS 번들링 지식 

### 전처리기 vs 후처리기 

CSS는 전처리기와 후처리기가 있다.

* 전처리기 : 화면에 보여주기 전에 (렌더링 전에) CSS를 변경해서, 스타일을 보여준다. 
   사용자가 작성하기 쉬운 코드로 작성 → 기본 CSS로 변환 → 렌더링

* 후처리기 : 화면에 보여주고 나서, CSS 변경.
  기본 CSS파일 작성 => 렌더링 → 외부 프로그램 사용해서 스타일 변경


유명한 전,후 처리기들은 다음과 같다. 
* 전처리기 : Scss, Stylus, Less 
* 후처리기 : [PostCSS](https://www.npmjs.com/package/postcss)   


CSS 전,후 처리기를 사용하는 유명한 프레임워크는 다음과 같다. 
* 전처리기: BootStrap 
* 후처리기: Tailwind CSS 



### RollUp에서의 처리기 
RollUp에서 전처리기와 후처리기 플러그인이 모두 존재한다. 그러나 후처리기 플러그인인 PostCss를 사용해서 
처리해도 sass 파일 컴파일이 가능하다. 


## CSS 컴파일을 위한 플러그인 설치 

다음 플러그인 들을 설치한다. 

```
npm install -D  rollup-plugin-postcss
npm install -D  autoprefixer
npm install -D  postcss-import
```


* rollup-plugin-postcss : postcss 도구 지원
* autoprefixer: -webkit- 등의 prefix 없이 스타일을 지정할 수 있게 도와준다.
* postcss-import: CSS @import 룰을 사용할 수 있게 해 준다.로컬 파일,  노드 모듈 또는 web_modules를 사용할 수 있다.


> PostCSS는 자바스크립트 기반의 플러그인을 사용하여 CSS 기능을 자동화하는 소프트웨어 개발 도구이다. PostCSS 자체는 아무 일도 하지 않는다. 다만 다양한 플러그인과, 플러그인을 추가할 수 있는 환경을 제공할 뿐이다. 

**PostCSS의 플러그인들**     
* [Autoprefixer](https://github.com/postcss/autoprefixer):  CSS 규칙에 vendor 접두사를 추가하고 CSS를 파싱하기 위한 플러그인. -webkit- 등의 prefix 없이 스타일을 지정할 수 있게 도와준다.
* [postcss-custom-properties](https://github.com/postcss/postcss-custom-properties):  CSS에서 변수를 사용할 수 있게 해 준다.
* [postcss-simple-vars](https://github.com/postcss/postcss-simple-vars): Sass 형식의 변수 선언을 원한다면, postcss-simple-vars 를 사용한다. 
* [postcss-import](https://github.com/postcss/postcss-import): CSS @import 룰을 사용할 수 있게 해 준다.이 플러그인은 로컬 파일,  노드 모듈 또는 web_modules를 사용할 수 있다. 디폴트로 process.cwd()로 root directory, web_modules, node_modules를 조사할 수 있다. 모듈을 임포트할 때 index.css 또는 package.json에서 참조하는 파일을  찾을 것이다. 







rollup-plugin-postcss는 sass와 sass-loader를 필요로 한다.  sass는 최근에 dart로 만들었다. sass 플러그인을 설치한다. 


```
npm install -D sass
npm install -D sass-loader
```

>  node-saas는 이제 안쓴다. 

## reset-css와 normalize.css 설치 
다음을 실행하여 reset-css와 normalize.css를 설치한다. 
```
npm i -D reset-css normalize.css
```
'웹 브라우저'마다 default 값으로 스타일이 적용되어 있기 때문에 우리는 브라우저마다의 기본 디폴트 스타일 값이 아니라 동일한 CSS 스타일을 보여주기 위해 이런 default 디폴트 값을 초기화 해주어야 한다. 브라우저마다 태그를 렌더링하는 기본 스타일이 다르고, 기본 padding,margin값들 이 적용되어 있는 부분을 초기화 하기위해 style 기본값을 0으로 만들고 list,a태그에 기본적으로 적용된 스타일들의 초기화를 위해 reset css를 해준다.

브라우저마다 각기 다른 기본값을 통일하고 일관된 모양을 표현하기 위해 reset css나 normalize css를 통해 base css 작성하는 방법을 쓴다



모두 설치했으면 package.json은 다음과 같이 보일 것이다. 
```json
{
  "scripts": {
    "build": "rollup -c -w"
  },
  "devDependencies": {
    "@rollup/plugin-commonjs": "^22.0.1",
    "@rollup/plugin-json": "^4.1.0",
    "@rollup/plugin-node-resolve": "^13.3.0",
    "autoprefixer": "^10.4.7",
    "normalize.css": "^8.0.1",
    "postcss-import": "^14.1.0",
    "reset-css": "^5.0.1",
    "rollup": "^2.75.7",
    "rollup-plugin-browsersync": "^1.3.3",
    "rollup-plugin-generate-html-template": "^1.7.0",
    "rollup-plugin-postcss": "^4.0.2",
    "sass": "^1.53.0",
    "sass-loader": "^13.0.2"
  }
}
```

## main.scss 파일 생성
src 디렉터리 아래에 styles를 만들고, 그 아래에 main.scss 파일을 다음과 같이 만든다. 
```scss

@charset "utf-8";
@import "~reset-css";
@import "normalize.css";

// 컴파일 되지 않는 주석
/* 컴파일 되는 주석 */ 

$color: orange;
div {
  @if $color == strawberry {
    color: #FE2E2E;
  } @else if $color == orange {
    color: #FE9A2E;
  } @else if $color == banana {
    color: #FFFF00;
  } @else {
    color: #2A1B0A;
  }
}

.section {
    width: 100%;
    background-color:#FFFF00;
    .list {
      padding: 20px;
      li {
        float: left;
      }
    }
  }
```  

index.js 파일에서 main.scss 파일을 import한다. 
```jsx
import './styles/main.scss';
console.log("Hello World K");
```

## rollup.config.js 
rollup.config.js 파일을 다음과 같이 수정한다. 
```jsx
import browsersync from 'rollup-plugin-browsersync'
import html from 'rollup-plugin-generate-html-template'
import commonjs from '@rollup/plugin-commonjs';
import { nodeResolve } from '@rollup/plugin-node-resolve';
import postcss from "rollup-plugin-postcss";
import autoprefixer from 'autoprefixer';
import cssimport from 'postcss-import';
import json from '@rollup/plugin-json';

      
export default {
   input : 'src/index.js',
   output : {
     file : 'dist/bundle.js',
     format : 'umd'
   },
   plugins : [
     browsersync({
        server : 'dist'
     }),
     html({
       template : 'src/index.html',
       target : 'dist/index.html'
     }),
     json(),   // package.json 파일 읽기 
     nodeResolve(),   // node_modules 폴더의 모듈 찾기 
     commonjs(),  // Common JS 
     postcss({
        includePaths: ['src/styles/'],
        extensions: ['.css', '.scss', '.sass'],
        extract: true, 
        plugins: [cssimport(), autoprefixer()],
      }),
   ]
}
```
다음을 실행한다. 
```
npm run build
```
dist 디렉터리에 bundle.css 파일이 생성된다. 








