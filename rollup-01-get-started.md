# 시작하기 

간단히 번들링하고 테스트해보자. 


## 프로젝트 구조
전체 구조는 다음과 같다. 
```
📁project_root
  📁dist
  📁src
    📄index.html
    📄index.js
  📄.gitignore
  📄package.json
  📄rollup.config.js 
```  


## 플러그인 설치 

다음 두 가지 플러그인을 설치한다. 

```
npm install -D rollup-plugin-browsersync 
npm install -D rollup-plugin-generate-html-template
```

* rollup-plugin-browsersync: 번들 디렉토리의 변경사항을 웹브라우저에 반영
* rollup-plugin-generate-html-template: index.html에 번들 스크립트 추가하여 생성


## index.html 생성 

index.html을 생성한다. 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>hello</h1>
</body>
</html>
```

## index.js 생성 
index.js를 생성한다. 
```jsx
console.log("Hello World K");
```

rollup.config.js 파일을 다음과 같이 작성한다. 
```jsx
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

## package.json 수정 

다음과 같이 package.json에 scripts를 추가한다. 
```json
{
  "scripts": {
    "build": "rollup -c -w"
  },
  "devDependencies": {
    "rollup": "^2.75.7",
    "rollup-plugin-browsersync": "^1.3.3",
    "rollup-plugin-generate-html-template": "^1.7.0",
  }
}
```
## 테스트 
다음과 같이 실행한다. 
```
npm run build
```
이제 index.js를 수정할 때 마다 브라우저에서 변경된 내용을 볼 수 있다. 


