# UMD bundle 빌드하기 

Rollup으로 UMD bundle을 빌드하는 방법에 대해서 정리한다. 


## OUtput Format 
제공하는 Output 포맷은 다음과 같다. 

| Output Format | Environment |
|----|-----|
| iife | Browser |
| cjs  | Node.js |
| umd | Browser + Node.js |


먼저 index.js 파일을 하나 만든다. src 아래에 둔다. 

```jsx
export default 'Hello, world!'
```


## UMD 
export name으로 MyModuleName을 갖는 UMD 번들을 만들기 위해서 다음과 같이 번들링한다. 

```
npx rollup src/index.js --file dist/bundle.js --format umd --name 'MyModuleName'
```

bundle.js는 다음과 같이 생성된다. 
```jsx
(function (global, factory) {
	typeof exports === 'object' && typeof module !== 'undefined' ? module.exports = factory() :
	typeof define === 'function' && define.amd ? define(factory) :
	(global = typeof globalThis !== 'undefined' ? globalThis : global || self, global.MyModuleName = factory());
})(this, (function () { 'use strict';

	var index = 'Hello, world!';

	return index;

}));
```



### 스크립트 로드하기 
```html
<!-- script.html -->
<script src="dist/bundle.js"></script>
<script>
  console.log(window.MyModuleName);
</script>
```

### AMD로 로드하기 
AMD를 사용하여 브라우저에서 모듈을 로드하기 위해서는 다음과 같이 한다. 
```html
<!-- amd.html -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.3.6/require.min.js"></script>
<script>
  window.requirejs(['dist/bundle'], function (MyModuleName) {
    console.log(MyModuleName);
  });
</script>
```
### COmmonJS
CommonJS를 사용하여 Node.js에서 모듈을 로드하기 위해서는 다음과 같이 한다. 
```
node
> const MyModuleName = require('./dist/bundle');
> console.log(MyModuleName);
Hello, world!
```

## 설정하기 
rollup.config.js 파일을 만들고 다음과 같이 작성한다. 
```jsx
// rollup.config.js
const config = {
  input: 'index.js',
  output: {
    file: 'dist/bundle.js',
    format: 'umd',
    name: 'MyModuleName',
  },
};

export default config;
```






## References 
[Build Rollup UMD bundle for CommonJS](https://remarkablemark.org/blog/2019/07/12/rollup-commonjs-umd/)     





