# 번들 파일 분할 



하나의 번들 파일을 만들면 너무 커서 부담이 될 수 있다. 동적 임포트를 사용하는 경우에 필요할 때만 불러오도록 번들 파일을 여러개로 나눌 수 있다.  

> 코드 분할은 실제로 동적 가져 오기의 멋진 이름입니다. Rollup을 사용하여 수행하는 방법은 다음과 같습니다 (이 과정에서 엄청난 트리 흔들림이 발생합니다!).

코드에서는 동적 임포트를 다음과 같이 할 수 있다. 
```
import('./Foo.svelte').then(module => {
  const cmp = module.default
  console.log(module.myNamedExport)
})
```

**동적 가져 오기는 일반 가져 오기와 같은 기본 ES 기능**입니다. 즉, 구식이 아닌 브라우저에서 기본적으로 지원됩니다.

롤업은 한동안 "동적 가져 오기에서 코드 분할"을 지원했습니다 ( docs 참조 ).

따라서 프로젝트에서 코드 분할을 원하는 경우 주로 동적 가져 오기를 청크하도록 롤업을 구성하는 것이 중요합니다 (다른 옵션은이를 해결하고 인라인하는 것이므로 코드 분할이 발생하지 않음).

* output.foramt에 es 
* output.file이 아니라 output.dir (예. public/build)
* \<script\> 에 태그 type="module"
* 동적 가져오기로 코드 작성

**rollup.config.js** 
```jsx
  input: 'src/main.js', // not changed
  output: {
    format: 'es',
    dir: 'public/build/',
  },
```
**index.html**   
```html
    <script defer type="module" src="/build/main.js"></script>
```
**동적가져오기 코드 작성**  
```jsx
import('./Foo.svelte')
  .then(module => module.default)
  .then(Foo => { /* do something with Foo */ })
  .catch(err => console.error(err)
```  



## 엔트리 파일 나누기 

output.entryFileNemas를 사용한다. inlineDynamicImports와 같이 사용한다. 
```jsx
    output: {
        sourcemap: true,
        format: 'iife',
        // minify할 것인지 여부, 개발 시에는 false
        compact: false, 
        //format: 'esm',
        // 동적으로 컴포넌트를 로드하고 번들 파일을 분리할 때 사용한다.
        inlineDynamicImports: true, 
        name: 'app',
        // file은 동적 컴포넌트 로드일때는 사용하지 못하고 dir을 사용한다. 
        //file: 'public/build/bundle.js',
        dir: 'public/build',
        entryFileNames: '[name]-[format]-[hash].js',
    },
```    

> 진입점에서 생성된 청크에 사용할 패턴 또는 이러한 패턴을 반환하기 위해 진입 청크별로 호출되는 함수입니다. 패턴은 다음 자리 표시자를 지원합니다.

* placeholder
  * name: entrypoint의 파일이름(확장자 없는). 다른 이름을 지정할 수 있다. 
  * format:  output 옵션에서 정의한 format 
  * hash: entrypoint의 컨텐트를 기준으로한 hash  

npm run build 하면 format이 iife일 때  다음과 같은 파일이 생성된다.

```
main-iife.ad3bd7e8.js
main-iife.ad3bd7e8.js.map 
```

## 청크파일 나누기 

chunkFileNames는 다음과 같이 설명이 되어 있다. 

 Name pattern for emitted secondary chunks

첫번재 파일은 entry 파일이름이고, 두번째 분할된 파일의 이름 패턴인 것 같은데.....

> 공유청크의 의미를 아직 명확히 파악하지 못했다. 

코드 분할 시 생성된 공유 청크의 이름을 지정하는 데 사용할 패턴 또는 이러한 패턴을 반환하기 위해 청크별로 호출되는 함수입니다. 패턴은 다음 자리 표시자를 지원합니다.




