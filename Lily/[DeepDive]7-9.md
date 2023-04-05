# 7장 연산자

- 연산자operator는 하나 이상의 표현식을 대상으로 산술, 할당, 비교, 논리, 타입, 지수 연산 등을 수행해 하나의 값을 만든다.

## 7.1 산술연산자

- 피연산자를 대상으로 수학적 계산을 수행해 새로운 숫자 값을 만든다.
- 산술 연산이 불가능한 경우, `NaN`을 반환한다.

### 7.1.1 이항 산술 연산자

### 7.1.2 단항 산술 연산자

- `++` : 증가
- `--` : 감소

```jsx
var x = 5
var = result

result = x++
console.log(result, x)  // 5 6

result = ++x
console.log(result, x)  // 7 7
```

### 7.1.3 문자열 연결 연산자

- 개발자의 의도와는 상관없이 자바스크립트 엔진에 의해 암묵적으로 타입이 자동으로 변환되기도 한다.
- 암묵적 타입 변환 또는 타입 강제 변환이라고 한다.

## 7.2 할당 연산자

- 우항에 있는 피연산자의 평가 결과를 좌항에 있는 변수에 할당한다.
- 표현식은 값으로 평가될 수 있는 문이고, 문에는 표현식인 문과 표현식이 아닌 문이 있다.
- 할당문은 값으로 평가되는 표현식인 문으로서 할당된 값으로 평가된다.

## 7.3 비교 연산자

## 7.4 삼항 조건 연산자

- 삼항 조건 연산자 표현식은 `if ... else` 문과 중요한 차이가 있다.
  - 삼항 조건 연산자는 값처럼 사용할 수 있다.
  - `if ... else` 문은 값처럼 사용할 수 없다.
- 삼항 조건 연산자 표현식은 값으로 평가할 수 있는 표현식인 문이다.

## 7.5 논리 연산자

- `||` : 논리합(OR)
- `&&` : 논리곱(AND)
- `!` : 부정(NOT)

# 8장 제어문

## 8.1 블록문

- 0개 이상의 문을 중괄호로 묶은 것

## 8.2 조건문

## 8.3 반복문

### 8.3.1 for

### 8.3.2 while

### 8.3.3 do … while

## 8.4 break

## 8.5 continue

# 9장 타입 변환과 단축 평가

## 9.1 타입 변환이란?

- 명시적 타입 변환(explict coercion) 또는 타입 캐스팅(type casting)

  - 개발자가 의도적으로 값의 타입을 변환하는 것

    ```jsx
    var x = 10
    var str = x.toString()

    console.log(typeof str, str) // string 10
    console.log(typeof x, x) // number 10
    ```

- 암묵적 타입 변환(implicit coercion) 또는 타입 강제 변환(type coercion)

  - 개발자의 의도와는 상관없이 표현식을 평가하는 도중에 자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환되는 것

    ```jsx
    var x = 10
    var str = x + ''

    console.log(typeof str, str) // string 10
    console.log(typeof x, x) // number 10
    ```

- 자신이 작성한 코드에서 암묵적 타입 변환이 발생하는지, 발생한다면 어떤 타입의 값으로 변환 되는지, 그리고 타입 변환된 값으로 표현식이 어떻게 평가될 것인지 예측 가능해야 한다.

### 9.2.1 문자열 타입으로 변환

- 템플릿 리터럴의 표현식 삽입은 표현식의 평가 결과를 문자열 타입으로 암묵적 타입 변환한다.
  ```jsx
  ;`1 + 1 = ${1 + 1}` // "1 + 1 = 2"
  ```

### 9.2.3 불리언 타입으로 변환

- Falsy
  - false
  - undefined
  - null
  - 0, -0
  - NaN
  - ‘’ (빈 문자열)
- Truthy : falsy 값 이외의 값

## 9.3 명시적 타입 변환

- 변경 방법
  - 표준 빌트인 생성자 함수(String, Number, Boolean)를 new 연산자 없이 호출하는 방법
    - `String()`, `Number()`, `Boolean()`, `parseInt()`, `parseFloat()`
  - 빌트인 메서드를 사용하는 방법
    - `.toString()`

## 9.4 단축 평가

### 9.4.1 논리 연산자를 사용한 단축 평가

- 논리합(||) 또는 논리곱(&&) 연산자 표현식의 평가 결과는 불리언 값이 아닐 수도 있다.
  - 언제나 2개의 피연산자 중 어느 한쪽으로 평가된다.
- 논리곱(&&) 연산자는 두 개의 피연산자가 모두 true로 평가될 때 true를 반환한다.
- 논리곱 연산자는 좌항에서 우항으로 평가가 진행된다.
  ```jsx
  'Cat' && 'Dog' // -> 'Dog'
  ```
  - 첫 번째 피연산자는 Truthy 값이므로 true로 평가된다.
  - 두 번쨰 피연산자가 위 논리곱 연산자 표현식의 평가 결과를 저장한다.
  - 논리곱 연산자는 논리 연산의 결과를 결정하는 두 번째 피연산자, 즉 문자열 ‘Dog’를 그대로 반환한다.
- 논리합(||) 연산자는 두 개의 피연산자 중 하나만 true로 평가되어도 true를 반환한다.
- 논리합 연산자도 좌항에서 우항으로 평가가 진행된다.
  ```jsx
  'Cat' || 'Dog' // -> 'Cat'
  ```
  - 첫 번째 피연산자는 Truty 값이므로 true로 평가된다.
  - 두 번째 피연산자까지 평가해 보지 않아도 위 표현식을 평가할 수 있다.
  - 이 때 논리합 연산자는 논리 연산 결과를 결정한 첫 번째 피연산자, 즉 문자열 ‘Cat’을 그대로 반환한다.
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f41581b4-cd49-4757-b39f-8e27fa06eea4/Untitled.png)
- 단축 평가를 사용하면 if문을 대체할 수 있다.
  - 어떤 조건이 Truthy일 때 무언가를 해야 한다면 논리곱(&&) 연산자 표현식
  ```jsx
  var done = true
  var message = ''

  if (done) message = '완료'

  message = done && '완료'
  console.log(message) // 완료
  ```
  - 어떤 조건이 Falsy일 때 문언가를 해야 한다면 논리합(||) 연산자 표현식
  ```jsx
  var done = false
  var messge = ''

  if (!done) message = '미완료'

  message = done || '미완료'
  console.log(message)
  ```
- 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 수 있다.
  ```jsx
  var elem = null
  var value = elem && elem.value
  ```
- 함수 매개변수에 기본값을 설정할 때 단축 평가를 사용해 매개변수의 기본값을 설정하면 undefined로 인해 발생할 수 있는 에러를 방지할 수 있다.
  ```jsx
  function getStringLen(str) {
    str = str || ''
    return str.length
  }
  ```

### 9.4.2 옵셔널 체이닝 연산자 `?.`

- 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.
  ```jsx
  var elem = null

  var value = elem?.value
  console.log(value)
  ```
  - 좌항 피연산자가 false로 평가되는 falsy 값이라도 null 또는 undefined가 아니면 우항의 프로퍼티 참조를 이어간다.

### 9.4.3 null 병합 연산자 `??`

- 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환한다.
- 변수에 기본값을 설정할 때 유용하다.
  ```jsx
  var foo = null ?? 'default string'
  console.log(foo) // 'default string'
  ```
- 하지만 null 연산자는 좌항의 피연산자가 false로 평가되는 Falsy 값이라도 null 또는 undefined가 아니면 좌항의 피연산자를 그대로 반환한다.
  ```jsx
  var foo = '' ?? 'default string'
  console.log(foo) // ''
  ```
