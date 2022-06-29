# Install 

Bundler는 의존성이 있는 모듈 코드를 하나 혹은 여러개의 파일로 만들어주는 도구이다. Chrome등 최신 브라우저에서는 ES6 Module을 지원하기도 하지만, 모듈화하여 작성한 코드를 브라우저에서 바로 실행할 수 없으므로 가공이 필요한데 번들러가 이 역할을 한다.대표적인 번들러로 Webpack, Parcel, Rollup등이 있다. 

번들러에 대한 소개는 [여기](https://sambalim.tistory.com/137)를 참고한다. 

## Rollup의 좋은 점 
장점에 대해서 살펴보자. 

* 속도가 웹팩보다 빠르고 결과물이 가볍다. 
* ES6 모듈 형태로 빌드 결과물을 출력할 수 있다. 



## 설치 

설치는 아래와 같이 설치한다.   자세한 사항은
[Installing Rollup locally](https://rollupjs.org/guide/en/#installing-rollup-locally)을 참고한다. 



```
npm install rollup --save-dev
```


