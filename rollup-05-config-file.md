# rollup.config.js 

rollup.config.js에 대해 상세한 내용을 정리한다. 


여러 input으로 CommonJS 모듈과 es 모듈을 위한 번들을 빌드한다. 

```jsx
// rollup.config.js 
export default [
    {
      input: 'src/main.js',
      output: {
        file: 'dist/bundle-cjs.js',
        format: 'cjs'
      }
    },
    {
      input: 'src/main2.js',
      output: [
        {
          file: 'dist/bundle-cjs2.js',
          format: 'cjs'
        },
        {
          file: 'dist/bundle-b2.js',
          format: 'es'
        }
      ]
    }
  ];
```
다음과 같이 빌드한다. 
```
yarn rollup -c 
```

config 파일을 지정하고 싶으면 다음과 같이 한다. 
```
rollup --config rollup.config.js -c
```



## package.json
npm을 사용할 수 있게 package.json을 수정한다. 
```json
{
  "name": "rollup-tutorial",
  "version": "1.0.0",
  "scripts": {
    "build": "rollup -c"
  },
  "devDependencies": {
    "rollup": "^2.75.6"
  }
}
```

이제 다음과 같이 빌드할 수 있다. 
```
npm run build
```


## config 파일예

```jsx
//rollup.config.js
import commonjs from "@rollup/plugin-commonjs";
import typescript from "rollup-plugin-typescript2";
import resolve from "@rollup/plugin-node-resolve";
import svgr from "@svgr/rollup";
import url from "@rollup/plugin-url";
import peerDepsExternal from "rollup-plugin-peer-deps-external";
import babel from "@rollup/plugin-babel";
import pkg from "./package.json";

export default {
  input: "src/index.ts", // 어떤 파일로 부터 불러올것인지 설정
  output: [
    {
      file: pkg.main,// package.json에 설정한 main의 경로로 번들링 진행
      format: "cjs", // commonjs 형태로 번들링
      sourcemap: true,
    },
    {
      file: pkg.module, //번들링한 파일을 저장 할 경로, package.json에 설정한 module의 경로로 번들링
      format: "esm", // es모듈 형태로 번들링
      sourcemap: true,
    },
  ],
  plugins: [
    commonjs(),//commonJS형태로 만들어진 모듈도 불러와서 사용 할 수 있게 해줌
    resolve(), //node_modules에서 모듈을 불러올수 있도록 해줌, ts/tsx 파일도 불러올수 있음
    url(), //미디어 파일을 dataURI 형태로 불러와서 사용 할 수 있게 해줌
    svgr(), //svg를 컴포넌트로 사용 할 수 있게 해줌
    peerDepsExternal(), //peerDependencies에 설치된 라이브러리들을 external모듈로 설정하여 번들 결과물에서 제외
    babel({ exclude: "node_modules/**" }), //babel을 사용 할 수 있게 해줌
    typescript({ useTsconfigDeclarationDir: true }), //typescript 플러그인
  ],
};
```