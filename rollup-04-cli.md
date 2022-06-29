# Command Line Interface

설정파일을 만들어 빌드하는 방법을 살펴본다. 


루트에 rollup.config.js 설정파일을 만든다. 

```
📂project_root
  📂src
    📄foo.js
    📄main.js
📄rollup.config.js 
```

```jsx
export default {
  input: 'src/main.js',
  output: {
    file: 'bundle.js',
    format: 'cjs'
  }
};
```


다음을 입력하여 번들링한다. 

```
yarn rollup -c 
```


프로젝트 루트에 다음과 같이 bundle.js 파일이 만듣어 진다. 
```
'use strict';

var foo = 'hello world';

function main () {
    console.log(foo);
}

module.exports = main;
```