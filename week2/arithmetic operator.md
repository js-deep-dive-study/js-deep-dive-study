# 산술 연산자

산술(Arithmetic) 연산자는 피연산자를 대상으로 수학적 계산을 수행해 새로운 숫자 값을 만든다(산술 연산자를 통해 다른 데이터 타입의 값을 생성해낼 수 없다). 산술 연산이 불가능할 경우, `NaN`(Not a Number)를 반환한다

### 목차

- [1 이항(Binary) 산술 연산자](#1-이항(Binary)-산술-연산자)
- [2 단항(Unary) 산술 연산자](#2-단항(Unary)-산술-연산자)
  - [2-1 증감(Increment/Decrement) 연산자](#2-1-증감(Increment/Decrement)-연산자)
  - [2-2 + 단항 산술 연산자](#2-2-+-단항-산술-연산자)
  - [2-3 - 단항 산술 연산자](#2-3---단항-산술-연산자)
- [3 문자열 연결 연산자](#3-문자열-연결-연산자)
- [4 연산자에 의한 타입 변환](#4-연산자에-의한-타입-변환)

***

<br>

## 1 이항(Binary) 산술 연산자

2개의 피연산자를 산술 연산해서 새로운 숫자 값을 생성해내는 산술 연산의 형태다. 모든 이항 산술 연산자는 산술 연산을 수행해도 피연산자의 값을 변경하는 부수 효과가 없고 언제나 새로운 숫자 값을 생성한다

| 이항 산술 연산자 | 의미   | 부수 효과 |
| ---------------- | ------ | --------- |
| +                | 덧셈   | 없음      |
| -                | 뺼셈   | 없음      |
| *                | 곱셈   | 없음      |
| /                | 나눗셈 | 없음      |
| %                | 나머지 | 없음      |

```jsx
20 + 10; // → 30
20 - 10; // → 10
5 * 10; // → 50
10 / 5; // → 2
20 % 8; // → 4
```

<br>

## 2 단항(Unary) 산술 연산자

1개의 피연산자를 산술 연산해서 새로운 숫자 값을 생성해내는 산술 연산의 형태다

| 단항 산술 연산자 | 의미                                                | 부수 효과 |
| ---------------- | --------------------------------------------------- | --------- |
| ++               | 증가                                                | 있음      |
| --               | 감소                                                | 있음      |
| +                | 어떠한 효과도 없다(음수를 양수로 반전하지도 않는다) | 없음      |
| -                | 양수를 음수로, 음수를 양수로 반전한 값을 반환한다   | 없음      |

### 2-1 증감(Increment/Decrement) 연산자

증감(`++`/`--`) 연산자는 피연산자의 값을 변경하는 부수 효과가 있다. 이는 증감 연산을 실행했을 때 피연산자의 값을 변경하는 부수 효과가 있다는 뜻이다

```jsx
var count = 1;
	
count--; => count = count - 1; // → 1
console.log(count); // → 0
var count = 1;

count++; => count = count + 1; // → 1
console.log(count); // → 2
```

변수 값을 `+1` 혹은 `-1`씩 증감시킨다

```jsx
var count = 1; 
count = count + 1;
```

사람이 생각하는 `=`의 의미는 ‘같다’로 `count = count + 1`(`1 = 1 + 1`)이 `1 = 2`라는 소리인데 이게 어떻게 성립하는지 의문이 들 수 있다. 그러나 이것을 기억해야 한다. 컴퓨터 프로그래밍 상에서 쓰이는 `=`의 의미는 ‘할당하다'라는 뜻이다. 즉, 변수 `count`에 `count+1`의 평가 결과 값인 `2`를 재할당한다는 의미다. 프로그래밍 상에서 ‘같다'의 의미를 지닌 것은 `==`, `===`이다.

증감 연산자는 증감 연산자의 위치에 따라 부수 효과가 다르다:

- **후위 증가(Postincrement) 연산자**: **먼저 다른 연산을 수행한 후**, 피연산자의 값을 증가시키고 암묵적 할당이 이루어진다

  ```javascript
  // 후위 증가 연산자식
  var count = 1;
  
  var postIncre = count++;
  
  console.log(postIncre, count); // → 1 2
  
  // 위 후위 증가 연산자식 코드를 풀어쓴 것
  var count = 1;
  
  var postIncre = count; 
  count = count + 1; 
  
  console.log(postInre, count); // → 1 2
  ```

    1. 먼저 변수 `postIncre`에 변수 `count`의 변수 값 `1`을 할당하는 연산을 수행한 후,
    2. 표현식 `count + 1`대로 피연산자 `count`와 `1`을 더해
    3. 생성된 숫자 값 `2`를 변수 `count`에 암묵적으로 할당한다

- **후위 감소(Postdecrement) 연산자**: **먼저 다른 연산을 수행한 후**, 피연산자의 값을 감소시키고 암묵적 할당이 이루어진다

  1. 먼저 변수 `postDecre`에 변수 `count`의 변수 값 `1`을 할당하는 연산을 수행한 후,
  2. 표현식 `count - 1`대로 피연산자 `count`에서 `1`을 빼
  3. 생성된 숫자 값 `0`를 변수 `count`에 암묵적으로 할당한다

  ```javascript
  /* 후위 감소 연산자식 */
  var count = 1; 
  
  var postDecre = count--;
  
  console.log(postDecre, count); // → 1 0
  
  // 위 후위 감소 연산자식 코드를 풀어쓴 것
  var count = 1; 
  
  var postDecre = count; 
  count = count - 1;
  
  console.log(postDecre, count); // → 1 0
  ```

- **전위 증가(Preincrement) 연산자**: **먼저 피연산자의 값을 증가시킨 후 암묵적 할당이 이루어지고**, 다른 연산을 수행한다

  1. 먼저 표현식 `count + 1`대로 피연산자 `count`와 `1`을 더한 후
  2. 생성된 숫자 값 `6`을 변수 `count`에 암묵적으로 할당하고
  3. 변수 `preIncre`에 변수 `count`의 변수 값 `6`을 할당하는 연산을 수행한다

  ```javascript
  // 전위 증가 연산자식
  var count = 5; 
  
  var preIncre = ++count; 
  
  console.log(preIncre, count); // → 6 6
  
  // 위 전위 증가 연산자식 코드를 풀어쓴 것
  var count = 5;
  
  count = count + 1; 
  var preIncre = count;
  
  console.log(preIncre, count); // → 6 6
  ```

- **전위 감소(Predecrement) 연산자**: **먼저 피연산자의 값을 증가시킨 후 암묵적 할당이 이루어지고**, 다른 연산을 수행한다

  1. 먼저 표현식 `count - 1`대로 피연산자 `count`에서 `1`을 뺀 후
  2. 생성된 숫자 값 `9`를 변수 `count`에 암묵적으로 할당하고
  3. 변수 `preDecre`에 변수 `count`의 변수 값 `9`을 할당하는 연산을 수행한다

  ```javascript
  // 전위 감소 연산자식
  var count = 10; 
  
  var preDecre = --count;
  
  console.log(preDecre, count); // → 9 9 
  // 위 전위 감소 연산자식 코드를 풀어쓴 것
  var count = 10; 
  
  count = count - 1; 
  var preDecre = count; 
  
  console.log(preDecre, count); // → 9 9
  ```

### 2-2 + 단항 산술 연산자

숫자 타입이 아닌 피연산자에 `+` 단항 산술 연산자로 연산을 수행하면 피연산자를 숫자 타입으로 변환해서 반환한다. 피연산자의 값 자체를 변경하는 것이 아니라 숫자 타입으로 타입 변환만 수행해 변환된 값을 반환하는 것이다. 따라서 부수 효과는 없다

- 숫자로 이루어진 문자열 타입의 경우:

  피연산자 `x`의 값을 숫자 타입 `1`로만 변환하는 것이며, `x`를 참조했을 때 값 변환 없이 문자열 `‘1’`이 반환된다

  ```javascript
  var x = '1'; 
  console.log(+x); // → 1
  console.log(x); // → '1'
  ```

- 문자열 타입의 경우:

  ```javascript
  var x = 'Jace';
  console.log(+x); // → NaN
  console.log(x); // → 'Jace'
  ```

- 불리언 타입의 경우(불리언 값 `true`와 `false`가 `1`과 0`인` 이유에 대해서 [**여기**]()를 참고하자)

  ```javascript
  var x = true; 
  console.log(+x); // → 1
  console.log(x); // → true
  var x = false;
  console.log(+x) // → 0
  console.log(x) // → false
  ```

### 2-3 - 단항 산술 연산자

`-` 단항 산술 연산자는 피연산자의 부호를 반전한 값을 반환한다. `+` 단항 산술 연산자와 동일하게 숫자 타입이 아닌 피연산자에 연산을 수행하면 숫자 타입으로 부호만 바뀐채 변환된 값을 반환한다

```jsx
var x = -10;
console.log(-x); // *→* *10*
console.log(x); // *→* *-10*

var y = 10; 
console.log(-y); // *→* *-10*
console.log(y); // *→* 10
```

- 숫자로 이루어진 문자열의 경우

  ```javascript
  var x = '10'; 
  console.log(-x); // → -10
  console.log(x); // → '10';
  ```

- 문자열 타입의 경우

  ```javascript
  var x = -'Jace';
  console.log(-x); // → NaN
  console.log(x); // → NaN
  ```

- 불리언 타입의 경우

  ```javascript
  var x = true; 
  console.log(-x); // → -1
  console.log(x); // → 1
  ```

<br>

## 3 문자열 연결 연산자

`+` 연산자는 피연산자 중 하나 이상이 문자열인 경우 문자열 연결 연산자로 동작한다

```jsx
'1' + 2; // → '12'
1 + '2'; // → '12'
'1' + '2'; // → '12'
```

<br>

## 4 연산자에 의한 타입 변환

개발자의 의도와는 상관없이 JS 엔진에 의해 암묵적으로 데이터 타입이 자동 변환되기도 한다. 이를 암묵적 타입 변환(Implicit Coercion) 또는 타입 강제 변환이라고도 한다

> 암묵적 타입 변환에 대해 더 자세한 내용은 **[여기]()**를 참고하자

```jsx
// 문자열 연결 연산자
'1' + 2; // → '12'

// 불리언 타입 변환
1 + true; // → 2
1 + false; // → 1

// null 타입 변환
1 + null; // → 1

// undefined 타입 변환
+undefined; // → NaN
1 + undefined; // → NaN
```

<br>

***

- [모던 자바스크립트 Deep Dive](http://www.yes24.com/Product/Goods/92742567)
- [JavaScript 증감 연산자(Feat. 전위 연산자, 후위 연산자)](https://velog.io/@iamhayoung/JavaScript-%EC%A6%9D%EA%B0%90-%EC%97%B0%EC%82%B0%EC%9E%90-Feat.-%EC%A0%84%EC%9C%84-%EC%97%B0%EC%82%B0%EC%9E%90-%ED%9B%84%EC%9C%84-%EC%97%B0%EC%82%B0%EC%9E%90)
- [JavaScript 연산자](https://axce.tistory.com/50)

