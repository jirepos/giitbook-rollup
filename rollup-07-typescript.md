# typescript  번들링



TypeScript 플러그인 설치 

```shell
npm i -D typescript  rollup-plugin-typescript2
```



rollup.config.js 파일 생성한다. 
```jsx
// rollup.config.js

import typescript from 'rollup-plugin-typescript2';

export default {
  input: './src/app.ts',
  output: {
    file: './dist/bundle.js',
    format: 'iife'
  },
  plugins: [
    typescript({
      tsconfig: 'tsconfig.json'
    })
  ]
}
```

tsconfig.json 파일을 다음과 같이 생성한다. 
```json
```

## Options
tsconfig.json
```json
{
  "compilerOptions": {
  
    /* 기본 옵션
     * ------------------------------------------------------------------------------------------------------------------------------------------------ */
    // "incremental": true,                   /* 증분 컴파일 활성화 */ 
    "target": "es5",                          /* ECMAScript 목표 버전 설정: 'ES3'(기본), 'ES5', 'ES2015', 'ES2016', 'ES2017','ES2018', 'ES2019', 'ES2020', or 'ESNEXT'. */
    "module": "esnext",                       /* 생성될 모듈 코드 설정: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', 'es2020', or 'ESNext'. */
    "lib": ["dom", "dom.iterable", "esnext"], /* 컴파일 과정에 사용될 라이브러리 파일 설정 */
    "allowJs": true,                          /* JavaScript 파일 컴파일 허용 */
    // "checkJs": true,                       /* .js 파일 오류 리포트 설정 */
    "jsx": "react",                           /* 생성될 JSX 코드 설정: 'preserve', 'react-native', or 'react'. */
    // "declaration": true,                   /* '.d.ts' 파일 생성 설정 */
    // "declarationMap": true,                /* 해당하는 각 '.d.ts'파일에 대한 소스 맵 생성 */
    // "sourceMap": true,                     /* 소스맵 '.map' 파일 생성 설정 */
    // "outFile": "./",                       /* 복수 파일을 묶어 하나의 파일로 출력 설정 */
    // "outDir": "./dist",                    /* 출력될 디렉토리 설정 */
    // "rootDir": "./",                       /* 입력 파일들의 루트 디렉토리 설정. --outDir 옵션을 사용해 출력 디렉토리 설정이 가능 */
    // "composite": true,                     /* 프로젝트 컴파일 활성화 */
    // "tsBuildInfoFile": "./",               /* 증분 컴파일 정보를 저장할 파일 지정 */
    // "removeComments": true,                /* 출력 시, 주석 제거 설정 */
    "noEmit": true,                           /* 출력 방출(emit) 유무 설정 */
    // "importHelpers": true,                 /* 'tslib'로부터 헬퍼를 호출할 지 설정 */
    // "downlevelIteration": true,            /* 'ES5' 혹은 'ES3' 타겟 설정 시 Iterables 'for-of', 'spread', 'destructuring' 완벽 지원 설정 */
    "isolatedModules": true,                  /* 각 파일을 별도 모듈로 변환 ('ts.transpileModule'과 유사) */

    /* 엄격한 유형 검사 옵션
     * ------------------------------------------------------------------------------------------------------------------------------------------------ */
    "strict": true,                           /* 모든 엄격한 유형 검사 옵션 활성화 */
    // "noImplicitAny": true,                 /* 명시적이지 않은 'any' 유형으로 표현식 및 선언 사용 시 오류 발생 */
    // "strictNullChecks": true,              /* 엄격한 null 검사 사용 */
    // "strictFunctionTypes": true,           /* 엄격한 함수 유형 검사 사용 */
    // "strictBindCallApply": true,           /* 엄격한 'bind', 'call', 'apply' 함수 메서드 사용 */
    // "strictPropertyInitialization": true,  /* 클래스에서 속성 초기화 엄격 검사 사용 */
    // "noImplicitThis": true,                /* 명시적이지 않은 'any'유형으로 'this' 표현식 사용 시 오류 발생 */
    // "alwaysStrict": true,                  /* 엄격모드에서 구문 분석 후, 각 소스 파일에 "use strict" 코드를 출력 */

    /* 추가 검사 옵션
     * ------------------------------------------------------------------------------------------------------------------------------------------------ */
    // "noUnusedLocals": true,                /* 사용되지 않은 로컬이 있을 경우, 오류로 보고 */
    // "noUnusedParameters": true,            /* 사용되지 않은 매개변수가 있을 경우, 오류로 보고 */
    // "noImplicitReturns": true,             /* 함수가 값을 반환하지 않을 경우, 오류로 보고 */
    "noFallthroughCasesInSwitch": true,       /* switch 문 오류 유형에 대한 오류 보고 */
    // "noUncheckedIndexedAccess": true,      /* 인덱스 시그니처 결과에 'undefined' 포함 */

    /* 모듈 분석 옵션
     * ------------------------------------------------------------------------------------------------------------------------------------------------ */
    "moduleResolution": "node",               /* 모듈 분석 방법 설정: 'node' (Node.js) 또는 'classic' (TypeScript pre-1.6). */
    // "baseUrl": "./",                       /* 절대 경로 모듈이 아닌, 모듈이 기본적으로 위치한 디렉토리 설정 (예: './modules-name') */
    // "paths": {},                           /* 'baseUrl'을 기준으로 상대 위치로 가져오기를 다시 매핑하는 항목 설정 */
    // "rootDirs": [],                        /* 런타임 시 프로젝트 구조를 나타내는 로트 디렉토리 목록 */
    // "typeRoots": [],                       /* 유형 정의를 포함할 디렉토리 목록 */
    // "types": [],                           /* 컴파일 시 포함될 유형 선언 파일 입력 */
    "allowSyntheticDefaultImports": true,     /* 기본 출력(default export)이 없는 모듈로부터 기본 호출을 허용 (이 코드는 단지 유형 검사만 수행) */
    "esModuleInterop": true                   /* 모든 가져오기에 대한 네임스페이스 객체 생성을 통해 CommonJS와 ES 모듈 간의 상호 운용성을 제공. 'allowSyntheticDefaultImports' 암시 */
    // "preserveSymlinks": true,              /* symlinks 실제 경로로 결정하지 않음 */
    // "allowUmdGlobalAccess": true,          /* 모듈에서 UMD 글로벌에 접근 허용 */

    /* 소스맵 옵션
     * ------------------------------------------------------------------------------------------------------------------------------------------------ */
    // "sourceRoot": "./",                    /* 디버거(debugger)가 소스 위치 대신 TypeScript 파일을 찾을 위치 설정 */
    // "mapRoot": "./",                       /* 디버거가 생성된 위치 대신 맵 파일을 찾을 위치 설정 */
    // "inlineSourceMap": true,               /* 하나의 인라인 소스맵을 내보내도록 설정 */
    // "inlineSources": true,                 /* 하나의 파일 안에 소스와 소스 코드를 함께 내보내도록 설정. '--inlineSourceMap' 또는 '--sourceMap' 설정이 필요 */

    /* 실험적인 기능 옵션
     * ------------------------------------------------------------------------------------------------------------------------------------------------ */
    // "experimentalDecorators": true,        /* ES7 데코레이터(decorators) 실험 기능 지원 설정 */
    // "emitDecoratorMetadata": true,         /* 데코레이터를 위한 유형 메타데이터 방출 실험 기능 지원 설정 */
    
    /* 고급 옵션
     * ------------------------------------------------------------------------------------------------------------------------------------------------ */
    "skipLibCheck": true,                     /* 선언 파일 유형 검사 스킵 */
    "forceConsistentCasingInFileNames": true  /* 동일한 파일에 대한 일관되지 않은 케이스 참조를 허용하지 않음 */
    
  }
}
```


**target**    
어떤 버전의 자바스크립트로 바꿀지 결정. 
* es5 : es5 버전 
* es2016, esnext 가능 

**module**    
import 문접을 구현할 때 어떤 문벚을 쓸지 정한다. 

* commonjs는 rquire 사용
* es2015, esnext는 import 사용






**outDir**    
저장되는 디렉터리를 outDir을 통해서 지정할 수 있다.    


**outFile**   
모든 파일을 하나의 파일로 합쳐서 출력할 경우 지정하는 파일명이다.



**baseUrl**    
외부 모듈이 아닌 이상 상대 경로로 모듈을 참조해야 한다. baseUrl은 외부 모듈이 아닌 모듈들을 절대 경로 참조할 수 있게 해 준다. 만약 baseUrl을 "src"로 설정하게 되면 src/를 기준으로 절대 경로로 모듈 참조가 가능해진다.


**paths**    
모듈 참조를 baseUrl를 기준으로 다시 매핑시킬 수 있다

```json
{
  "compilerOptions": {
    "baseUrl": "src",
    "paths": {
        "app/*": ["app/*"],
        "config/*": ["app/_config/*"],
        "lib/*": ["lib/*"],
        "tests/*": ["tests/*"]
    },
}
```

"../../../lib/some"과 같이 길고 알아보기 힘든 경로를 "lib/some"과 같이 단순하게 만들 수 있데 된다.



### include / exclude
```json
{
  // 컴파일 포함
  "include": [
    "src/**/*.tsx?"
  ],
  // 컴파일 제외
  "exclude": [
    "node_modules",
    "build",
    "**/*.(spec|test).ts"
  ],
  // 컴파일 옵션
  "compilerOptions": { ... }
}
```


**include**    
```
{
  "include": ["src/**/*", "tests/**/*"]
}
```
include를 통해서 pattern 형태로 원하는 파일 목록을 지정할 수 있다.include와 exclude 모두 glob 패턴을 지원한다.

- *(asterisk) 없거나 하나 이상의 문자열과 일치 (디렉터리 구분자 제외)
- ? 하나의 문자와 일치 (디렉터리 구분자 제외)
- **/ 단계에 관계없이 아무 디렉터리와 일치

**exclude**    
exclude로 include에 지정한 파일이나 패턴을 제외시킬 수 있다. 주의할 점은 include에 지정하지 않은 파일은 적용되지 않는 점이다.

exclude를 지정하지 않으면 ["node_modules", "bower_components", "jspm_packages"]와 outDir에 지정한 경로가 기본값이 된다.






