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


## Rollup.js Options and Flags
명령줄 옵션 중 중요한 것만. 

* -c, --congif: 이 config file 사용한다. 이 아규먼트가 사용되고 값이 제공되지 않으면,rollup.config.js를 사용한다. 
* -w, --watch: bundle에서 파일이 변화를 지켜보고, 변경시 리빌드한다.
* --help (or -h): display Rollup.js help
* --version (or -v): display the Rollup.js version number
* --input <filename> (or -i): specify the entry script. This is not necessary because the file is usually defined as the first option.
* --file <output> (or -o): the bundled file name. When omitted, the bundle is output to stdout.
* --format <type> (or -f): the JavaScript bundle format:
* --environment <values>: set one or more comma-separated environment variables, e.g. --environment NODE_ENV:development,VAR1,VAR2:abc which sets NODE_ENV to development, VAR1 to true, and VAR2 to abc.
* --sourcemap: create a source map so you can reference the original source files in browser DevTools. The bundled file will link to a .map file in build folder, e.g. build/bundle.js.map.Use --sourcemap inline to define an inline source map within the bundle.
* --watch (or -w): watch for source file changes during development and bundle automatically.The screen clears when a change triggers a re-build but you can disable this with --no-watch.clearScreen




## 참고 
[The Ultimate Guide to Getting Started with the Rollup.js JavaScript Bundler](https://blog.openreplay.com/the-ultimate-guide-to-getting-started-with-the-rollup-js-javascript-bundler)      

