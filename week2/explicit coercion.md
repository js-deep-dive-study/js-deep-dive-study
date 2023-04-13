# 명시적 타입 변환

JS의 모든 [데이터(값)에는 타입]()이 있으며 타입들은 명시적/암묵적으로 다른 타입들로 변환할 수 있다. 먼저 명시적 타입 변환에 대해 알아보자

### 목차

- [1 명시적 타입 변환이란](#1-명시적-타입-변환이란)
- [2 문자열 타입으로의 명시적 타입 변환](#2-문자열-타입으로의-명시적-타입-변환)
- [3 숫자 타입으로의 명시적 타입 변환](#3-숫자-타입으로의-명시적-타입-변환)
- [4 불리언 타입으로의 명시적 타입 변환](#4-불리언-타입으로의-명시적-타입-변환)

***

<br>

## 1 명시적 타입 변환이란

개발자가 의도적으로 값의 타입을 변환하는 것을 **명시적 타입 변환(Explicit Coercion)** **또는** **타입 캐스팅(Type Casting)**이라 한다. 개발자는 다양한 방법으로 데이터 타입의 명시적 타입 변환이 가능하다.

<br>

## 2 문자열 타입으로의 명시적 타입 변환

문자열 타입이 아닌 값을 문자열 타입으로 명시적 타입 변환하는 방법은 [**표준 빌트인 생성자 함수**]() 또는 [**표준 빌트인 메서드**]()를 포함해 다음과 같다:

1. `String` 생성자 함수를 [`new` 연산자]() 없이 호출하는 방법

   > 표준 빌트인 생성자 함수인 `String` 생성자 함수에 대해 자세한 내용은 **[여기]()**를 참고하자

   ```jsx
   String(1); // → '1'
   String(NaN); // → 'NaN'
   String(Infinity); // → 'Infinity'
   
   String(true); // → 'true'
   String(false); // → 'false'
   ```

2. `Object.prototype.toString`(`toString()`) 메서드를 사용하는 방법

   > 표준 빌트인 메서드인 `Object.prototype.toString`(`toString()`) 메서드에 대한 자세한 내용은 [**여기**]()를 참고하자

   ```jsx
   (1).toString(); // → '1'
   (NaN).toString(); // → 'NaN'
   (Infinity).toString(); // → 'Infinity'
   
   ...
   ```

   ```jsx
   // toString() 메서드
   var num = 10; 
   
   var str = num.toString(); 
   console.log(str, typeof str); // → 10 'string'
   ```

3. [**`+` 문자열 연결 연산자**]()를 이용하는 방법

   ```jsx
   1 + ''; // → '1'
   NaN + ''; // → 'NaN'
   Infinity + ''; // → 'Infinity'
   
   ...
   ```

<br>

## 3 숫자 타입으로의 명시적 타입 변환

숫자 타입이 아닌 값을 숫자 타입으로 명시적 타입 변환하는 방법은 다음과 같다:

1. `Number` 생성자 함수를 `new` 연산자 없이 호출하는 방법

   > 표준 빌트인 생성자 함수인 `Number` 생성자 함수에 대해 자세한 내용은 **[여기]()**를, `prompt()` 함수에 대해서는 **[여기]()**를 참고하자

   ```jsx
   Number('0'); // → 0
   Number('-1'); // → -1
   Number('10.53'); // → 10.53
   
   Number(true); // → 1
   Number(false); // → 0
   ```

   ```jsx
   // 예제
   var input = prompt('숫자를 입력해주세요'); // 숫자 10을 입력했다고 가정
   console.log(input, typeof input); // → 10 string
   
   var numInput = Number( prompt('숫자를 입력해주세요') ); // 숫자 10을 입력했다고 가정
   console.log(numInput, typeof numInput); // → 10 'number'
   
   var textInput = Number( prompt('문자를 입력해주세요') ); // 문자 abc를 입력했다고 가정 
   console.log(textInput, typeof textInput); // → NaN 'number'
   ```

2. `parseInt`, `parseFloat` 함수를 사용하는 방법(문자열만 숫자 타입으로 변환 가능)

   > 표준 빌트인 함수인 `parseInt`, `parseFloat` 생성자 함수에 대해 자세한 내용은 **[여기]()**를 참고하자

   ```jsx
   parseInt('0'); // → 0
   parseFloat('10.53'); // → 10.53
   ```

3. [**`+` 단항 산술 연산자**]()를 이용하는 방법

   ```jsx
   +'0'; // → 0
   +'-1'; // → -1
   +'10.53'; // → 10.53
   
   +true; // → 1
   +false; // → 0
   ```

4. [`*` 산술 연산자]()를 이용하는 방법

   ```jsx
   '0' * 1; // → 0
   '-1' * 1; // → -1
   '10.53' * 1; // → 10.53
   
   true * 1; // → 1
   false * 1; // → 0
   ```

   이항 산술 연산자인 `*` 산술 연산자가 들어간 표현식의 평가 결과는 무조건 숫자 타입이어야 한다. 그렇기 때문에 피연산자들을 숫자 타입으로 타입 변환해서 표현식이 평가될 수 있도록 한다

<br>

## 4 불리언 타입으로의 명시적 타입 변환

불리언 타입이 아닌 값을 불리언 타입으로 명시적 타입 변환하는 방법은 다음과 같다:

1. `Boolean` 생성자 함수를 `new` 연산자 없이 호출하는 방법

   > 표준 빌트인 생성자 함수인 `Boolean` 생성자 함수에 대해 자세한 내용은 **[여기]()**를 참고하자

   ```jsx
   // 문자열 타입 to 불리언 타입
   Boolean('x'); // → true
   Boolean(''); // → false
   Boolean(' '); // → true
   
   // 숫자 타입 to 불리언 타입
   **Boolean(0); // → false
   Boolean(1); // → true
   Boolean(NaN); // → false
   Boolean(Infinity); // → true
   
   // null 타입 to 불리언 타입
   Boolean(null); // → false
   
   // undefined 타입 to 불리언 타입
   Boolean(undefined); // → false
   
   // 객체 타입 to 불리언 타입
   Boolean({}); // → true
   Boolean([]); // → true
   Boolean([10, 20]); // → true
   ```

2. [**`!` 부정 논리 연산자**]() 두번 연달아 사용하는 방법

   ```jsx
   // 문자열 타입 to 불리언 타입
   !!'x'; // → true
   !!''; // → false
   !!' '; // → true
   
   // 숫자 타입 to 불리언 타입
   !!0; // → false
   !!1; // → true
   !!NaN; // → false
   !!Infinity; // → true
   
   // null 타입 to 불리언 타입
   !!null; // → false
   
   // undefined 타입 to 불리언 타입
   !!undefined; // → false 
   
   // 객체 타입 to 불리언 타입
   !!{}; // → true
   !![]; // → true
   !![10, 20]; // → true
   ```

   `!` 부정 논리 연산자를 두 번 연달아 사용하는 이유에 대해서는 **[여기]()**를 참고하자

<br>

***

### 참고

- [모던 자바스크립트 Deep Dive](http://www.yes24.com/Product/Goods/92742567)