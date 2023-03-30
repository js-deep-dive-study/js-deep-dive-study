<img src="https://ifh.cc/g/n9Axkr.png" style="max-width: 100%" align="center">

### 목차

- [1 숫자 타입](#1-숫자-타입)

- [2 문자열 타입](#2-문자열-타입)

- [2-1 템플릿(Template) 리터럴](#2-1-템플릿(Template)-리터럴)

  - [2-1-1 멀티라인 문자열](#2-1-1-멀티라인-문자열)

  - [2-1-2 표현식 삽입](#2-1-2-표현식-삽입)

  - [2-1-3 그 외의 문자열 처리 기능](#2-1-3-그-외의-문자열-처리-기능)

- [3 불리언 타입](#3-불리언-타입)

- [4 undefined 타입](#4-undefined-타입)

- [5 null 타입](#5-null-타입)
  - [5-1 undefined와 null의 차이](#5-1-undefined와-null의-차이)

- [6 심벌 타입](6-심벌-타입)

***

<br>

## 1 숫자 타입

C, Java의 경우 정수와 실수를 구분해서 `int`, `long`, `float`, `double` 등 다양한 숫자 타입을 제공한다. 그러나 JS는 하나의 숫자(Number) 타입만 존재한다. JS의 숫자 타입 값은 [배정밀도 64비트 부동소수점 형식]()을 따른다. 즉, 모든 수를 [**실수**](https://www.notion.so/01a5cc029f124f77a76bed2982360cc9)로 처리하며 [**정수](https://www.notion.so/01a5cc029f124f77a76bed2982360cc9), [2진수, 8진수, 16진수](https://www.notion.so/01a5cc029f124f77a76bed2982360cc9)**만 표현하기 위한 데이터 타입이 별도로 존재하지 않는다

> 사람이 수를 계산할 때 10진수를 사용하는데(손가락이 10개)에 반해 컴퓨터가 수를 다룰 때 2진수, 8진수, 16진수를 사용한다. 사람이 생각하는 숫자를 컴퓨터 상에 표현하기 위해서 각종 진수, 진법을 사용한다. 진수, 진법에 대한 자세한 내용은 [**여기**](https://hymndev.tistory.com/17)를 참고하자

```jsx
var int = 10; // 정수(자연수)
var double = 10.12; // 실수(유리수)
var negative = -20; // 음의 정수

1 === 1.0; // → true
4 / 2; // → 2
3 / 2; // → 1.5

// 정수 65를 표현하기 위한 2진수, 8진수, 16진수
var binary = 0b0100001; // 2진수
var octal = 0o101; // 8진수
var hex = 0x41; // 16진수
```

> **수 체계에 대한 개념을 참고하기 위해 정리해뒀다**
>
> - 실수, 유리수, 무리수, 정수
>
>   <img src="https://ifh.cc/g/7GBPvF.jpg" style="max-width: 100%" align="center">
>
>   - 소수: 1과 자신만으로 나누어 떨어지는 1보다 큰 자연수 (e.g. 1, 2, 3, 5, 7, 11 …) 
>   - 약수: 어떤 수를 나누어 떨어지게 하는 수 (e.g. 12의 약수는 1, 2, 3, 4, 6, 12)

그 외에 숫자 타입의 특별한 값 세 가지가 존재한다:

- 양의 무한대

  ```javascript
  10/0; // → Infinity
  ```

- 음의 무한대

  ```javascript
  5/-0; // → -Infinity
  -3/0; // → -Infinity
  ```

- 산술연산불가(`NaN`): JS 엔진은 `NaN`을 '산술연산이 불가하다'는 식별자로 해석하기 때문에 대소문자 구분을 명확히 `NaN`으로 하여 입력해야 한다

  ```javascript
  1 * 'String'; // → NaN
  
  var a = NaN;
  a; // > NaN 
  
  var b = NAN; // *> Reference Error: NAN is not defined*
  var c = Nan; // *> Reference Error: Nan is not defined*
  var d = nan; // *> Reference Error: nan is not defined*
  ```

<br>

## 2 문자열 타입

문자열(String) 타입은 텍스트 데이터를 나타내는 데 사용된다. 따옴표(`’ ‘`, `“ “`) 혹은 백틱(``` `)으로 텍스트를 감싸지 않으면 JS 엔진은 해당 문자열을 키워드나 식별자 같은 토큰으로 인식한다

```jsx
var userName = Jace; // *> ReferenceError: Jace is not defined*
```

JS의 문자열은 원시 타입이며, 변경 불가능한 불변값이다

### 2-1 템플릿(Template) 리터럴

템플릿 [리터럴]()은 ES6부터 도입된 문자열 표기법이다. 일반 문자열과 비슷해 보이지만 따옴표(`’ ‘`, `“ “`) 대신 **백틱(` `)을 사용**한다

```jsx
var template = `Template Literal`; 
console.log(template); // *> Template Literal*
```

템플릿 리터럴은 런타임에 일반 문자열로 변환되어 처리된다

- 변수 선언의 실행 시점 - 소스코드가 순차적으로 실행되는 시점인 런타임 이전에 실행된다
- **리터럴 값의 평가 실행 시점 - 소스코드가 순차적으로 실행되는 시점인 런타임에 실행된다**
- 값의 할당의 실행 시점 - 소스코드가 순차적으로 실행되는 시점인 런타임 이후에 실행된다

그렇다면 템플릿 리터럴은 왜 도입되었을까? 일반 문자열은 텍스트 데이터를 표현하는데 한계가 있다. 대표적으로:

- 줄바꿈이 허용되지 않는다

  ```javascript
  var userName = 'Jace' 
  Nam; // → SyntaxError: Invalid or unexpected token
  ```

- 길어지거나 반복되는 문자열로 인해 가독성이 떨어지고 코드의 입력이 불편하다

  ```javascript
  // 문자열 연산자를 통한 문자열끼리의 연결
  var firstName = 'Jace'; 
  var lastName = 'Nam';
  
  console.log('My name is' + firstName + ' ' + lastName + '.');
  
  // 다른 데이터가 필요한 반복되는 HTML 태그나 목록
  var firstCategory = `<ul>
  	<li><a href="#">books</a></li>
  	<li><a href="#">bags</a></li>
  	<li><a href="#">shoes</a></li>
  	<li><a href="#">pants</a></li>
  </ul>`
  
  var secondCategory = `<ul>
  	<li><a href="#">shirts</a></li>
  	<li><a href="#">tops</a></li>
  	<li><a href="#">accessories</a></li>
  	<li><a href="#">living</a></li>
  </ul>`
  ```

따라서 템플릿 리터럴은 멀티라인 문자열, 표현식 삽입, 태그드(Tagged) 템플릿 등의 문자열 처리 기능을 제공한다

### 2-1-1 멀티라인 문자열

일반 문자열은 줄바꿈이 허용되지 않기에 줄바꿈과 같은 ‘공백'을 표현하기 위해 이스케이프 시퀀스(Escape Sequence)를 사용해야 한다

>  이스케이프 시퀀스에 대한 상세 내용은 [**여기**](https://atomic0x90.github.io/c-language/2019/05/28/C-Language-escape-sequence.html)를 참고하자. 줄바꿈(개행)이 허용되지 않는 이유에 대해서도 [**여기**](https://ko.wikipedia.org/wiki/새줄_문자)를 참고하자

```javascript
// 출력결과 1
console.log('Jace\nNam');
Jace
Nam

// 출력결과 2
console.log('Juhyung\n\tNam'); 
Juhyung
	Nam
```

일반 문자열과 달리 템플릿 리터럴 내에서는 이스케이프 시퀀스를 사용하지 않아도 줄바꿈이 가능하며 모든 공백도 있는 그대로 표현된다

```jsx
// 출력결과 1
console.log(`Jace
Nam`);
Jace
Nam

// 출력결과 2
console.log(`Jace
   Nam`);
Jace
   Nam
```

### 2-1-2 표현식 삽입

문자열 [**연산자 `+`**]()를 통해 문자열끼리 연결할 수 있으나, 백틱 리터럴(``` `) 내에서 표현식 삽입(Expression Interpolation, `${ }`)을 활용하면 문자열이 아니더라도 문자열 타입으로 강제로 변환된다

```jsx
var a = 10;
var b = 20; 
var c = 'Jace'; 

console.log('저는 올해' + ' ' + (a + b) + '살이고' + ' ' + '이름은' + ' ' + c + '입니다');
// 저는 올해 31살이고 이름은 Jace입니다 
```

```jsx
var a = 10;
var b = 20; 
var c = 'Jace'; 

console.log(`저는 올해 ${a + b}살이고 이름은 ${c}입니다`);
// 저는 올해 31살이고 이름은 Jace입니다 
```

표현식 삽입은 문자열 표현인 따옴표가 아닌 백틱 리터럴(` `` `)내에서 사용해야만 일반 문자열이 아닌 표현식 삽입으로 인지된다

```jsx
var a = 10;
var b = 20; 
var c = 'Jace'; 

console.log('저는 올해 ${a + b}살이고 이름은 ${c}입니다');
// 저는 올해 ${a + b}살이고 이름은 ${c}입니다
```

### 2-1-3 그 외의 문자열 처리 기능

Tagged Template, Nesting Template, Raw Strings 등의 문자열 처리 기능에 대한 내용은 [**MDN Template Literals(Template Strings)**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)를 참고하자. 템플릿 리터럴을 활용한 DOM 조작에 대한 내용도 [**여기**](https://blogpack.tistory.com/635)를 참고하자

<br>

## 3 불리언 타입

불리언(Boolean) 타입은 `true`와 `false`의 논리적 참, 거짓을 나타내는 데이터 유형만 존재한다. 불리언은 일반적으로 JS 프로그램 내에서 값의 비교를 통해 생성된다

```jsx
var x = 10; 

x === 10 // → true
x === 1 // → false
	
x < 100 // → true
x > 100 // → false
```

불리언 타입의 값은 참과 거짓으로 구분되는 조건에 의해 프로그램의 어떤 코드 부문이 실행 또는 반복되어야 할지(`if문`과 `for문`) 제어하는 [**조건문**]()에서 자주 사용한다

```jsx
if ( x > 0 ) { 
	console.log(true); // x가 0보다 크면 불리언 true를 반환한다
} else {
	console.log(false); // x가 0보다 작으면 불리언 false를 반환한다
};
```

추후 [암묵적 타입 변환]() 파트에서 공부할 예정이지만 미리 살펴보자면, 공통적으로 프로그래밍 언어에서는 불리언 값 `true`는 숫자 `1`로, `false`는 `0`으로 반환된다. 왜 그런것일까? 컴퓨터는 `1`과 `0` 이진법의 기계어를 통해 동작한다. 종류가 다양한 다른 문자열과는 달리, 불리언은 오직 두 가지 값 `true`와 `false`만을 가지기 때문에 인간의 참과 거짓 논리를 기계어인 `1`과 `0`으로 변환해서 간단하게 표현할 때 쓰이기도 한다

```javascript
1 == true; // → true
0 == false; // → true

'1' == true // → true
'0' == false // → true

0 + true; // → 1
0 + false; // → 0
```

불리언 타입 사용 시 주의해야 될 것은 연산자, 원시 타입, 객체 타입에 따라 형 변환이 일어나 불리언 값이 예상치 못하게 생성되는 현상이다. 예를 들어, 빈 배열(`[]`)은 `false` 값을 가진다

> 형 변환에 따라 불리언 값 `true`와 `false`로 변환되는 값들, 그리고 그 이유에 대해서는 [**타입 변환과 단축 평가**](https://www.notion.so/d52133051411406f81e5f841bc5d7933)를 참고하자

```javascript
[] == false; // → true
[] == 0; // → true
```

<br>

## 4 undefined 타입

`undefined` 타입의 값은 `undefined` 하나만 존재한다. `undefined`는 변수의 데이터 타입이 정해지지 않았음(undefined)을 나타낸다

JS 언어는 [**매니지드 언어**](https://www.notion.so/77110bb52cb24a2da58b58c82a19c943)로서 변수의 데이터 타입을 별도로 표기하지 않고, 변수에 할당되는 값에 따라 데이터 타입이 자동적으로 결정된다. 이러한 특징으로 JS는 다른 언어보다 변수 값과 메모리 관리가 용이하나, 변수 맵핑이 해제된 메모리 안에 쓰레기 값이 남아있을 확률이 높다. 이에 JS에서는 변수 선언 키워드로 선언한 변수는 [**암묵적으로 undefined로 초기화**]()된다. 변수 선언을 통해 확보된 메모리 공간을 처음으로 값을 할당할때까지 빈 상태로 내버려두지 않고 JS 엔진이 `undefined`로 초기화하는 것이다

```jsx
var userName; // → undefined
console.log(userName); // → undefined
```

<br>

## 5 null 타입

`null` 타입의 값은 `null` 하나만 존재한다. JS는 대소문자로 구별되므로 `Null`, `NULL` 등과 다르다. `null`은 변수 값이 없다는 것을 의미하며 변수에 `null`값이 할당된 상태이므로 데이터 타입이 정해진(defined) 상태다. 따라서 `null` 타입은, 

- 의도적으로 변수에 값이 없다는 것을 명시할 때 사용한다

- `null` 값을 변수에 할당 시, 이전에 변수가 참조하던 값을 더 이상 참조하지 않겠다는 의미다

  ```jsx
  var userName = 'Jace';
  
  userName = null; // 이전 참조를 제거하므로써, userName 변수는 더 이상 'Jace'를 참조하지 않는다
  ```

### 5-1  undefined와 null의 차이

`undefined`: 변수에 어떠한 값도 할당되지 않아 데이터 타입이 정해지지 않은(undefined) 상태다. 의도적으로 할당하기 위한 값이 아닌 JS 엔진에 의해 변수를 초기화할 때 나오는 값

`null`: 변수에 `null`를 할당하는 것은 변수 값이 없다는 것을 나타내며, 변수에 `null` 값이 할당된 상태이므로 데이터 타입이 정해진(defined) 상태다. 의도적으로 변수에 값이 없다는 것을 명시할 때 사용하는 값

‘값이 없다’는 점에서 유사하지만 다른 개념이다:

- 데이터 타입을 반환하는 `typeof` 연산자를 통해 `undefined`와 `null`의 타입 차이를 알 수 있다:

  > `null`은 원시 타입인데 `typeof` 연산자로 데이터 타입을 확인해보면 왜 `object`라고 반환될까? 이에 대한 내용은 [**여기**](https://curryyou.tistory.com/183)를 참고하자

  ```javascript
  var variable1; 
  **var variable2 = null; 
  
  typeof variable1; // → 'undefined'
  typeof variable2; // → 'object'
  ```

- 느슨한 비교 `undefined == null`은 `true`, 엄격한 비교 `undefined === null`은 `false`가 반환된다. JS `==` 비교 연산자의 자동 형변환으로 인해 `==`를 이용한 느슨한 검사 시 `true` 값이 반환되지만, `===`를 이용한 엄격한 비교 시 `undefined`와 `null`은 같지 않다는 것을 알 수 있다

  ```javascript
  undefined == null; // → true
  undefined === null; // → false
  ```

<br>

## 6 심벌 타입

심벌(Symbol) 타입은 ES6에서 원시타입에 추가된 7번째 데이터 타입으로, 심벌의 값은 다른 값과 중복되지 않는 유일한 값이다. 주로 이름이 충동할 위험이 없는 객체의 유일한 프로퍼티 키를 만들기 위해 사용한다

심벌 이외의 원시 값은 리터럴을(입력하는 코드가) 통해 생성하지만 심벌은 `Symbol` 함수를 호출해 생성한다. 이때 생성된 심벌 값은 외부에 노출되지 않으며, 다른 값과 절대 중복되지 않는 유일무이한 값이다. 심벌 타입을 추후 직접 사용해보고 관련 내용을 추가할 예정이다

<br>

***

### 참고

- [모던 자바스크립트 Deep Dive](http://www.yes24.com/Product/Goods/92742567)

- [Symbol을 사용하는 이유는 뭘까 | symbol usage](https://another-light.tistory.com/105)