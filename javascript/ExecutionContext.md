# Execution Context

[나 집으로 돌아갈래!](/README.md)

### 키워드

**렉시컬 환경**, **환경 레코드**, **아우터 환경 참조**
**스코프 체인**, **호이스팅**, **클로저**

## 실행컨텍스란?

- 실행컨텍스트란 렉시컬 환경을 담고 있는 객체이며, 스코프 체인이 되어있는 변수를 찾기 위해 만들어진 객체이다.

- 렉시컬 환경은 다시 환경 레코드 + 아우터 환경 참조를 지니고 있다.

- 환경 레코드는 식별자와 식별자가 바인딩 하고 있는 값을 저장하고 있다.

  - **호이스팅**

    - 마치 선언문이 최상단 스코프로 올라간듯한 현상

    - 변수 호이스팅, 함수 호이스팅으로 나눌 수 있다.

      - 함수 선언문의 경우 호이스팅 표현식은 X - 변수에 할당하기 때문에 변수

    - var의 경우 선언과 초기화가 동시에 일어나기 때문에 undefined

    - let const, 실행 단계에서 선언만 이루어지 때문에 레퍼런스 에러

    ```js
    console.log(no); // undefined

    var no = "hello";

    console.log(a); // Error
    // TDZ
    const a = 15;
    ```

- 아우터 환경 참조는 외부 스코프를 연결하는 통로

  - **클로저(Closure)**
    이녀석을 이해하기 위해 빌드업 과정인거 같다.

  - 외부에서 접근 불가한 데이터를 다룰때 ⭐️
  - 콜백함수를 사용할때

요코드를 실행해보면 closure 실체를 확인할 수 있다.

```js
function outer() {
  let brand = "porsche";
  return function () {
    let model = "911";
    console.log(brand, model);
  };
}

console.dir(outer());
```

```js
function createCounter() {
  let count = 0;
  return {
    increment: function () {
      count++;
    },
    decrement: function () {
      count--;
    },
    getCount: function () {
      console.log(count);
    },
  };
}
const counter = createCounter();
// 핵심 외부에서 직접 데이터를 접근하지 못한다.
console.log(counter.count); // undefined
counter.increment();
counter.getCount(); // 1
```

##### 생각해보기

let, const만 사용하다보니 호이스팅 현상에 대해 깊게 생각해본적이 없었는데,
당연히 선언문 이전에 함수를 사용한다거나, var 식별자를 사용할 일이 없어서 고민해본적 없는 문제들. var가 사용되는 환경(es5로 빌드 하는 경우 -> ??)
