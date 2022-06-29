# plugin 


## Using plugins
지금까지 진입점과 상대 경로를 통해 가져온 모듈에서 간단한 번들을 만들었다. 더 복잡한 번들을 빌드함에 따라 NPM과 함께 설치된 모듈 가져오기, Babel로 코드 컴파일, JSON 파일 작업 등 더 많은 유연성이 필요한 경우가 많다.

이를 위해 번들링 프로세스의 주요 지점에서 롤업의 동작을 변경하는 플러그인 을 사용 한다. 멋진 플러그인 목록은 Rollup Awesome List 에서 관리된다.


이 자습서에서는 @rollup/plugin-json 을 사용하여 Rollup이 JSON 파일에서 데이터를 가져올 수 있도록 한다. 

프로젝트 루트에 파일을 package.json만들고 다음 콘텐츠를 추가한다. 

```json
{
  "name": "rollup-tutorial",
  "version": "1.0.0",
  "scripts": {
    "build": "rollup -c"
  }
}
```

@rollup/plugin-json을 개발 의존성에 설치한다. 
```shell
npm install --save-dev @rollup/plugin-json
```

우리는 코드가 실행될 때 실제로 플러그인에 의존하지 않기 때문에 --save가 아니라 --save-dev를 사용한다.  번들을 빌드할 때만 사용한다. 

src/foo.js 대신에 package.json을 import하기 위해서 src/main.js를 업데이트 한다. 
```jsx
// src/main.js
import { version } from '../package.json';

export default function () {
  console.log('version ' + version);
}
```

JSON 플러그인을 추가하기 위해서 rollup.config.js를 수정한다. 
```jsx
// rollup.config.js
import json from '@rollup/plugin-json';

export default {
  input: 'src/main.js',
  output: {
    file: 'bundle.js',
    format: 'cjs'
  },
  plugins: [json()]
};
```


npm run build로 Rollup을 실행한다. 결과는 다음과 같이 보일 것이다. 

```shell
'use strict';

var version = '1.0.0';

function main() {
  console.log('version ' + version);
}

module.exports = main;
```





## 플러그인 설정

rollup 에 확장할 기능은 플러그인으로 추가할 수 있다. 그 중에 웹 개발에 필요한 몇 가지 도구를 설치하고 설정하는 작업을 진행한다.

* rollup-plugin-node-resolve : 외부 노드 모듈을 사용시 (node_modules 디렉토리)
* rollup-plugin-commonjs : 외부 노드 모듈이 es6 으로 변환되지 않았을 경우 es6 으로 변환
* rollup-plugin-browsersync : 번들 디렉토리의 변경사항을 웹브라우저에 반영
* rollup-plugin-generate-html-template : index.html에 번들 스크립트 추가하여 생성
* rollup-plugin-babel : babel 변환 지원
* rollup-plugin-postcss : postcss 도구 지원
* rollup-plugin-eslint : 코드 스타일 검사
* rollup-plugin-uglify : 번들 파일 난독화

### 빌드 플러그인

플러그인을 설치한다.

```
npm i rollup-plugin-browsersync rollup-plugin-generate-html-template
```

rollup.config.js에 플러그인 설정을 추가한다.

```javascript
import browsersync from 'rollup-plugin-browsersync'
import html from 'rollup-plugin-generate-html-template'

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
     })
   ]
}
```

index.html을 생성한다.

```markup
<!doctype html>
<html lang="ko">
<head><meta charset="utf-8"><title>hello rollup</title></head>
<body>
</body>
</html>
```

빌드 후 'hello rollup'이 브라우저에 출력되는지 확인한다.

```
npm run build
```

index.js 수정한 후 저장할 때마다 브라우저에 수정 사항이 반영되는지 확인한다.

### 외부 모듈 변환 플러그인

플러그인을 설치한다.

```
npm i rollup-plugin-node-resolve rollup-plugin-commonjs
```

위 두 개 deprecated 되었다고 함. 다음을 사용한다. 
```
@rollup/plugin-node-resolve
@rollup/plugin-commonjs
```






플러그인 설정을 추가한다.

```javascript
import resolve from 'rollup-plugin-node-resolve';
import commonjs from 'rollup-plugin-commonjs';
default export {
 ...
    plugins : [
     ...
        resolve(),
        commonjs({
            include : 'node_modules/**'
        }),
}
```

### Babel 변환 플러그인

플러그인과 babel7을 설치한다.

```
$ npm i @babel/core @babel/cli @babel/preset-env
$ npm i @babel/plugin-transform-runtime regenerator-runtime
$ npm i rollup-plugin-babel
```

babel 설정을 추가한다. .babelrc 파일을 생성한 다음에 다음을 추가한다.

```javascript
{
    "presets" : [
        [ "@babel/env", {
            modules : false,
            useBuiltIns : "usage",
            corejs : 3
        }]
    ]
}
```

rollup 플러그인 설정을 추가한다.

```javascript
import babel from 'rollup-plugin-babel';
default export {
 ...
    plugins : [
     ...
     babel({
            exclude : 'node_modules/**'
        }),
}
```

테스트용 index.js을 다시 작성한다.

```javascript
const text  = 'rollup';
async function say() {
    return `Hello ${text} async`;
}
const main = async () => {
    const message = await say();
    document.body.textContent = message;
    console.log(message);
}
main().catch(console.error)
```

빌드 후 ‘Hello rollup async’이 브라우저에 출력되는지 확인한다..
