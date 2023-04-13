# 그 외의 연산자들

### 목차

- [1 쉼표 연산자](#1-쉼표-연산자)
- [2 그룹 연산자](#2-그룹-연산자)
- [3 typeof 연산자](#3-typeof-연산자)
  - [3-1 typeof NaN](#3-1-typeof-NaN)
  - [3-2 typeof null](#3-2-typeof-null)
  - [3-3 typeof 연산자와 undefined](#3-3-typeof-연산자와-undefined)
- [4 그 외의 연산자](#4-그-외의-연산자)

***

<br>

## 1 쉼표 연산자

쉼표(Comma, `,`) 연산자는 좌측 피연산자부터 각각 차례대로 평가하고, 평가까지 끝나면 마자막 피연산자의 평가 결과를 반환한다. 배열, 객체, 함수의 매개변수와 호출 인수에서 사용하는 쉼표와 동일하지 않다. 쉼표(`,`) 연산자는 `for` 반복문, 함수(`map()`, `reduce()` 등)에서 사용될 때가 있다

```jsx
var a, b, c; 
a = 1, b = 2, c = 3; // → 3

var x, y, c; 
x = (y = 5, z = 6); // → 6

console.log(x); // → 6
```

<br>

## 2 그룹 연산자

그룹(`()`) 연산자로 감싸여진 피연산자는 가장 먼저 평가된다. 즉, 그룹 연산자를 사용하면 연산자와 평가될 피연산자의 우선순위를 조절할 수 있다. 그룹 연산자는 연산자 중 우선순위가 가장 높다

```jsx
10 * 5 + 10; // → 60
10 * ( 5 * 10 ); // → 500
```

<br>

## 3 `typeof` 연산자

**`typeof` 연산자는 피연산자의 데이터 타입을 문자열로 변경해서 반환**한다. 문자열로 반환되는 데이터 타입은 총 7가지로 `'string'`, `‘number'`, `‘boolean’`, `‘undefined’`, `‘symbol’`, `‘object’`, `‘function’`을 반환한다. `typeof` 연산자는 보통 다른 개발자와 협업을 할 때, 다른 개발자의 코드 중 데이터 타입이 명확하게 파악이 안될 경우 데이터 타입을 파악하는 용도로 자주 쓰인다. 중요한 것은 `typeof` 연산자를 통해 반환되는 데이터 타입의 문자열은 7개의 데이터 타입과 항상 정확히 일치하지는 않는다.

```jsx
typeof ''; // → 'string'
typeof 1; // → 'number'
typeof true; // → 'boolean'
typeof undefined; // → 'undefined'
typeof Symbol(); // → 'symbol'
typeof []; // → 'object'
typeof {}; // → 'object'
typeof function() // → 'function'
```

### 3-1 typeof NaN

`NaN`은 데이터 타입이 숫자가 아니라는 숫자 판명을 위해 쓰이므로 숫자 타입에 속한다

```jsx
typeof NaN; // → 'number'
```

### 3-2 typeof null

`null`은 `‘object'`로 반환되는데 이것은 첫 번째 JS 버전의 버그다. 기존 코드에 영향을 줄 수 있다는 이유에 아직까지 수정되지 못하고 있다.

```jsx
typeof null; // → 'object'
```

따라서 값이 `null` 타입인지 확인할 때는 일치 연산자(`===`)를 사용하자

```jsx
var x = null; 

typeof x === null; // → false
x === null; // → true
```

### 3-3 typeof 연산자와 undefined

선언하지 않은 것(undeclared)과 정의하지 않은 것(undefined)는 완전히 다른 개념이다.

```jsx
var x; 

x; // → undefined (변수에 값이 할당되지 않았음을 의미)
y; // → ReferenceError: y is not defined (변수 자체가 선언되지 않았음을 의미)
```

그러나 선언하지 않은 식별자를 `typeof` 연산자로 연산해보면 `ReferenceError`가 발생하지 않고 `‘undefined'`가 반환된다

```jsx
var x; 

x; // → undefined
y; // → ReferenceError: y is not defined

typeof x; // → 'undefined'
typeof y; // → 'undefined'
typeof z; // → 'undefined'
```

`typeof` 연산자의 Safety Guard라는 특성으로 인해 이러한 결과가 생긴다. Safety Guard는 특정 전역 변수의 존재 여부와 같이 예외사항을 확인할 수 있게 도와주는 기능인데, 모던 JS에서는 대부분 전역 변수를 사용하지 않아도 되기 때문에 의도적으로 사용할 필요가 없게 되었다

<br>

## 4 그 외의 자주 쓰이는 연산자 (추후 공부 후 내용 추가 예정)

앞서 언급된 [산술 연산자](), [할당 연산자](), [비교 연산자](), [삼항 조건 연산자](), [논리 연산자](), [쉼표 연산자](), [그룹 연산자](), `typeof` 연산자, [지수 연산자]()를 제외하고 추가적으로 6가지의 연산자가 더 존재한다

| 연산자       | 개요                                                        | 참고 |
| ------------ | ----------------------------------------------------------- | ---- |
| `?.`         | 옵셔널 체이닝 연산자                                        |      |
| `??`         | null 병합 연산자                                            |      |
| `delete`     | 프로퍼티 삭제                                               |      |
| `new`        | 생성자 함수를 호출할 때 사용하여 인스턴스를 생성            |      |
| `instanceof` | 좌변의 객체가 우변의 생성자 함수와 연결된 인스턴스인지 판별 |      |
| `in`         | 프로퍼티 존재 확인                                          |      |

<br>

***

### 참고

- [모던 자바스크립트 Deep Dive](http://www.yes24.com/Product/Goods/92742567)
- [[Javascript] You Don't Know JS: 타입과 값](https://baeharam.github.io/posts/javascript/jsyou-dont-know-js-value-and-type/)
- [자바스크립트 undefined와 typeof](https://www.huskyhoochu.com/typeof/)
- [자바스크립트 typeof 연산자](https://velog.io/@junseublim/자바스크립트-타입에-대한-완벽하게-알아보자)
- [You Don't Know JS: Types & Grammar](https://www.oreilly.com/library/view/you-dont-know/9781491905159/ch01.html)
- [Operator | PoiemaWeb](https://poiemaweb.com/js-operator)