# commonJS로 번들링

간단히 CommonJS 모듈로 빌드하고 사용하는 방법을 정리한다. 


자바스크립트에서 모듈에는 두 가지가 있다. 

* require는 NodeJS에서 사용되고 있는 CommonJS 키워드
* import는 ES6(ES2015)에 도입된 키워드 



NodeJS에서 사용하는 방식.

```jsx
const moment = require("moment");
```


ES6에서 사용하는 방식. 

```jsx
import moment from "moment";
```


## 내보내기 
CommonJS에서 모듈 생성하는 방법을 살펴본다. 

* 내보내기 
  * 여러 개의 객체를 내보낼 경우, exports 변수의 속성으로 할당한다.
  * 딱 하나의 객체를 내보낼 경우, module.exports 변수 자체에 할당한다.


### 여러 객체 내보내기 
3개의 함수 중에서 2개만 내보내려고 한다. 

```jsx
// currency-functions.js
const exchangeRate = 0.91;

function roundTwoDecimals(amount) {
  return Math.round(amount * 100) / 100;
}

const canadianToUs = function (canadian) {
  return roundTwoDecimals(canadian * exchangeRate);
};

function usToCanadian(us) {
  return roundTwoDecimals(us / exchangeRate);
}

exports.canadianToUs = canadianToUs; // 내보내기 1
exports.usToCanadian = usToCanadian; // 내보내기 2
```


**불러오기**     
```jsx
const currency = require("./currency-functions");

console.log("50 Canadian dollars equals this amount of US dollars:");
console.log(currency.canadianToUs(50));

console.log("30 US dollars equals this amount of Canadian dollars:");
console.log(currency.usToCanadian(30));
```


### 단일객체 내보내기 
이번에는 예제 코드를 살짝 수정하여 아래 두 개 함수를 객체로 묶어서 내보내기를 하였습니다. 내보낼 객체를 module.exports 변수에 할당해주면 됩니다.


```jsx
// currency-class.js 
const exchangeRate = 0.91;

// 안 내보냄
function roundTwoDecimals(amount) {
  return Math.round(amount * 100) / 100;
}

// 내보내기
const obj = {};
obj.canadianToUs = function (canadian) {
  return roundTwoDecimals(canadian * exchangeRate);
};
obj.usToCanadian = function (us) {
  return roundTwoDecimals(us / exchangeRate);
};
module.exports = obj;
```

**불러오기**     
```jsx
const currency = require("./currency-object");

console.log("50 Canadian dollars equals this amount of US dollars:");
console.log(currency.canadianToUs(50));

console.log("30 US dollars equals this amount of Canadian dollars:");
console.log(currency.usToCanadian(30));
```

# 빌드하기 


```
📂project_root
  📂src
    📄foo.js
    📄main.js
```

ES6로 foo.js를 만든다. 

```jsx
export default 'hello world';
```

main.js 만든다. 
```jsx
import foo from './foo';

export default function () {
    console.log(foo);
}
```

빌드한다. 

```
yarn rollup src/main.js -o ./src/nodejs/bundle.js -f cjs
```

bundle.js 파일이 만들어 진다. 

```jsx
'use strict';

var foo = 'hello world';

function main () {
    console.log(foo);
}

module.exports = main;
```


nodjs로 테스트한다. 


```
node ./src/nodejs/node-test.js 
```

