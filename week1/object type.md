<img src="https://ifh.cc/g/KpJfN0.png" style="max-width: 100%" align="center" >

### 목차
- [1 객체란](#1-객체란)
- [2 객체 리터럴](#2-객체-리터럴)
- [3 객체의 구성 요소](#3-객체의-구성-요소)
    - [3.1 프로퍼티란](#3.1-프로퍼티란) 
    - [3.2 프로퍼티 접근](#3.2-프로퍼티-접근)
    - [3.3 프로퍼티 값 갱신](#3.3-프로퍼티-값-갱신)
    - [3.4 프로퍼티의 동적 생성, 삭제 및 확인](#3.4-프로퍼티의-동적-생성,-삭제-및-확인) 
- [4 메서드](#4-메서드) 
***
<br>

JS는 객체 기반의 프로그래밍 언어로 JS에서 객체의 개념은 매우 중요하다. [원시 타입]()을 제외한 나머지 값(함수, 배열, 정규 표현식 등)은 모두 객체로 JS를 구성하는 거의 모든 값이 객체다. 즉, JS는 객체 기반의 언어이며 JS를 이루고 있는 거의 모든 것이 객체다
<br>

## 1 객체란
원시 타입과는 달리, 객체 타입은 원시 타입 또는 다른 객체를 하나의 단위로 구성한 복합적인 자료구조의 특성을 띄고 있다

원시 타입의 경우 단 하나의 값만 변수에 할당할 수 있다.  아래 예제에서는 논리 연산자의 논리 연산 결과 값 하나만이 변수에 할당된다
```javascript
var num = 1; 
var str = "Jace"; 
var boolean = true; 

var orOperator = false || null; // → null 
var andOperator = true && "word"; // → "word"
```
그러나 객체 타입의 경우, 다양한 타입의 값을 하나의 단위로 묶어 변수에 할당할 수 있다

> 원시 타입과 객체 타입의 대한 자세한 비교는 [원시 값과 객체의 비교]()를 참고하자

```javascript
var user = {
	name: "Jace", 
	age: 30,
	residence: "Seoul"
}; 

console.log(user); // → { name: 'Jace', age: 30, residence: 'Seoul' }
```
<br>

## 2 객체 리터럴
[리터럴]()이란 값을 나타내는 표기법이라고 했다. 객체 리터럴은 JS 엔진에 의해 값이 객체라고 인식되게 하기 위한 표기법이다. 중괄호(`{}`) 객체 리터럴을 사용하여 중괄호 내에 0개 이상의 프로퍼티를 JS 엔진이 ‘객체’로 인식할 수 있도록  정의(표현)한다. 객체 리터럴에 대한 더 자세한 내용은 [객체 리터럴에 의한 객체 생성]()을 참고하자

아래 예제와 같이 중괄호 내에 프로퍼티를 정의하지 않으면 빈 객체가 생성된다

```javascript
var emptyObj = {
}; 
  
console.log(emptyObj, typeof emptyObj); // → {} 'object'
```
<br>

## 3 객체의 구성 요소
객체는 프로퍼티(Property, 속성)와 메서드로 구성된 집합체라고 할 수 있다. 프로퍼티와 메서드의 역할은 다음과 같으며 프로퍼티에 대해 먼저 살펴보자:

- **프로퍼티**: 객체의 상태를 나타내는 값(데이터)
- **메서드**: 프로퍼티(상태 데이터)를 참조하고 조작할 수 있는 동작(Behavior)

### 3.1 프로퍼티란
객체 타입은 여러가지 원시 타입과 객체 타입을 하나의 단위로 묶어 변수에 할당할 수 있게 한다 했다. 여러가지 데이터 타입을 담아 복합적인 자료(데이터) 구조를 지니고 있는 객체의 데이터 성질을 분류 및 구조화해서 표현하기 위해 프로퍼티(속성)이 존재한다

프로퍼티는 키(Key)와 값(Value)으로 페어링되어 구성된다. 키와 값으로 구성된 프로퍼티들이 0개 이상 모여 하나의 집합으로서 객체를 이룬다. 아래 예제에서 프로퍼티 키는 `name`, `age`, `residence`이며 프로퍼티 값은 `‘Jace’`, `30`, `‘Seoul’`이다. 프로퍼티는 `name: ‘Jace’`, `age: 30`, `residence: ‘Seoul’`이다

<img src="https://ifh.cc/g/3hLQF4.png" style="max-width: 100%" align="center">

프로퍼티를 나열할 때는 쉼표(`,`)로 구분한다. 마지막 프로퍼티 뒤에는 쉼표를 사용하지 않으나 사용해도 좋다 
```javascript
var userAccount = {
	id: "Jace", 
	pw: 123, 
};
```
프로퍼티의 키와 값으로 사용할 수 있는 값은 다음과 같다:
- 프로퍼티 키: **모든 문자열(빈 문자열도 포함)**, 심벌 값 → *그러나 일반적으로 문자열 사용* 
- 프로퍼티 값: **JS에서 사용할 수 있는 모든 값**

프로퍼티 키는 프로퍼티 값에 접근할 수 있는 식별자로서의 역할을 수행한다. 반드시 [식별자 네이밍 규칙]()을 따라야 하는 것은 아니지만, 바로 앞에서 언급했듯이 프로퍼티 키는 문자열이기 때문에 따옴표(`’‘`, `““`)로 감싸야하고 식별자 네이밍 규칙을 준수하는 이름으로 프로퍼티 키를 지정했을 때 따옴표를 생략할 수 있어 가독성이 좋다
```javascript
var userName = {
	firstName: "Jace", // 식별자 네이밍 규칙을 준수한 경우 따옴표 생략이 가능하다
	"last-name": "Nam", //  식별자 네이밍 규칙을 미준수한 경우 따옴표 생략이 불가능하다
	last-name: "Nam" // → SyntaxError: Unexpected token -
};
```

프로퍼티 키에 문자열로 암묵적 타입 변환이 가능한 데이터 타입(e.g. 숫자 타입)은 사용이 가능하다. 콘솔에 반환된 객체 `obj`의 프로퍼티 키는 따옴표가 따로 붙지 않지만 실제로는 `"0"`, `"1"`, `"2"`로 문자열이다
```javascript
var obj = {
	0: 1, 
	1: 2, 
	2: 3
}; 

console.log(obj); // → {0: 1, 1: 2, 2: 3 }
```

이미 존재하는 프로퍼티 키를 중복 선언하면 나중에 선언한 프로퍼티가 먼저 선언한 프로퍼티를 덮어쓴다. **이미 존재하는 프로퍼티 키 이름을 중복 선언했다고 해서 에러가 발생하지 않는다는 점에 주의하자**
```javascript
var userName = {
	name: "Jace",
	name: "Ju Hyung"
}; 

console.log(userName); // → {name: 'Ju Hyung'}
```
### 3.2 프로퍼티 접근
객체 값(데이터)을 제어하기 위해서는 프로퍼티에 접근할 수 있어야 한다. 프로퍼티에 접근하는 방법은 두 가지가 존재한다. 프로퍼티 키가 **식별자 네이밍 규칙을 준수하는 이름이라면** 마침표 표기법과 대괄호 표기법을 모두 사용할 수 있다

1. 마침표 표기법(`.`, Dot Notation): 마침표 프로퍼티 접근 연산자를 사용하는 방법

   ```javascript
     var user = { 
         name: "Jace", 
         age: 30
     };
   
     console.log(user.name); // → Jace
   ```
2. 대괄호 표기법(`[]`, Bracket Notation): 대괄호 프로퍼티 접근 연산자를 사용하는 방법

   ```javascript
     var user = {
         name: "Jace", 
         age: 30
     };
   
     console.log(user["age"]); // → 30

프로퍼티 접근 연산자의 구조를 살펴보자. 대괄호 표기법을 사용하는 경우 **대괄포 프로퍼티 연산자 내부에 지정하는 프로퍼티 키는 반드시 따옴표(`’’`,` “”`)로 감싼 문자열**이어야 한다. 대괄호 프로퍼티 접근 연산자 내에 따옴표로 감싸지 않은 이름을 프로퍼티 키로 사용하면 JS 엔진은 이를 식별자로 인식하기 때문이다. 프로피티 키는 식별자 네이밍 규칙에 따라 이름을 지정한다 했지만, **문자열이지 식별자가 아니니 이 부분을 헷갈리지 않도록 주의하자**

<img src="https://ifh.cc/g/sBvMFD.png" style="max-width: 100%" align="center">

객체에 존재하지 않는 프로퍼티 접근하면 `undefined`를 반환한다. `ReferenceError`가 발생하지 않으니 주의하자
```javascript
var user = {
	name: "Jace"
};

console.log(user.age); // → undefined
console.log(user["age"]); // → undefined 
```
~~프로퍼티 키가 문자열로 암묵적 타입 변환이 가능한 숫자 타입 혹은 숫자로 이루어진 문자열 타입인 경우, 프로퍼티 접근 연산자(마침표, 대괄호)를 사용할 때 따옴표(`''`, `""`)를 생략할 수 있다~~. 이 부분은 책 내용에 에러가 있어 [그 이유](https://www.becomebetterprogrammer.com/can-javasscript-object-keys-be-numbers-or-non-string-values/)를 찾아보고 다시 정리해서 추가했다:

- 프로퍼티 키가 문자열로 암묵적 타입 변환이 가능한 숫자 타입 혹은 숫자로 이루어진 문자열 타입인 경우, **대괄호 프로퍼티 접근 연산자를 통해 프로퍼티에 정상적으로 접근이 가능**하다. 사실, 대괄호 프로퍼티 접근 연산자 내 '문자열'이라고 따옴표로 표시하기만 하면 모든 타입의 값을 사용할 수 있다. 이는 대괄호 프로퍼티 접근 연산자 내의 피연산자를 파싱해서 프로퍼티에 접근하기 때문이라 한다
  ```javascript
  var user = {
    1: "Jace", 
    2: "Ju Hyung"
    "{}": "Zhou Heng"
  }; 
  
  console.log(user[1]); // → Jace
  console.log(user["2"]); // → Ju Hyung
  console.log(user["{}"]); // → Zhou Heng
  ```
- 그러나 프로퍼티 키가 문자열로 암묵적 타입 변환이 가능한 숫자 타입 혹은 숫자로 이루어진 문자열 타입이더라도 **마침표 프로퍼티 접근 연산자를 사용하면 프로퍼티에 접근이 불가능**한 에러가 발생한다.  
  ```javascript
  var user = {
    1: "Jace", 
    2: "Ju Hyung"
  }; 
  
  // 에러가 발생한다
  console.log(user.1); // → Uncaught SyntaxError: missing ) after argument list
  console.log(user."2"); // → Uncaught SyntaxError: Unexpected string
  ```
  왜 에러가 발생하는 것일까? 마침표 프로퍼티 접근 연산자의 연산 대상인 피연산자는 프로퍼티 키다. 그리고 앞서 언급했듯이 프로퍼티 키는 프로퍼티 값에 접근하게 해주는 식별자로서의 역할을 수행한다 했다. 마침표 프로퍼티 접근 연산자의 피연산자인 프로퍼티 키가 문자열로 암묵적 타입 변환이 가능한 숫자 타입 혹은 숫자로 이루어진 문자열일 경우 프로퍼티 값의 '식별자'로서의 역할을 수행하지 못하기 때문에, 마침표 프로퍼티 접근 연산자 뒤에는 항상 문자열, 심벌 타입 혹은 문자열로 암묵적 타입 변환이 가능한 JS 키워드(`undefined`, `null`, `true`, `false`)가 위치해야 한다
  
  ```javascript
  var user = {
    undefined: "Jace", // => "undefined": "Jace"와 동일
    null: "Ju Hyung", // => "null": "Ju Hyung"과 동일
    false: "Zhou Heng" // => "false": "Zhou Heng"과 동일
  }
  
  console.log(user.undefined); // → Jace
  console.log(user.null); // → Ju Hyung
  console.log(user.false); // → Zhou Heng
  ```

### 3.3 프로퍼티 값 갱신
이미 존재하는 프로퍼티에 값(프로퍼티 값)을 할당하면 프로퍼티 값이 갱신된다 
```javascript
var user = {
  name: "Jace"
} 

user.name = "Ju Hyung"; 
console.log(user); // → { name: 'Ju Hyung' }
```
### 3.4 프로퍼티의 동적 생성, 삭제 및 확인 
객체는 프로퍼티의 개수가 정해져 있지 않으며, 동적으로 추가하고 삭제할 수 있다
- 프로퍼티의 동적 생성: 존재하지 않는 프로퍼티에 값(프로퍼티 키와 프로퍼티 값)을 할당하면 프로퍼티가 동적으로 생성되어 추가된다
  ```javascript
  var user = {
      name: 'Jace'
  };
  
  user.age = '30'; 
  console.log(user); // → { name: 'Jace', age: 30 }
  ```
- 프로퍼티의 동적 삭제: `delete` 연산자는 객체의 프로퍼티를 삭제한다
  ```javascript
  var user = {
      name: 'Jace'
  }; 
  
  user.age = 30; 
  console.log(user); // → { name: 'Jace', age: 30 }
  
  delete user.age; 
  console.log(user); // → { name: 'Jace' }
  ```
  만약 존재하지 않는 프로퍼티를 삭제하면 어떠한 에러 경고가 없음에 주의하자 
  ```javascript
  var user = {
      name: 'Jace'
  } 
  
  delete user.residence; 
  console.log(user); // → { name: 'Jace' }
  ```

- 프로퍼티의 확인: `in` 연산자는 객체에 특정 프로퍼티가 존재하는지 확인할 때 사용한다. 결과 값은 불리언 타입으로 반환된다
  ```javascript
  var user = {
      name: 'Jace', 
      age: 30
  }; 
  
  'name' in user; // → true
  'address' in user; // → false
  ```

<br>

## 4 메서드 
JS에서 사용할 수 있는 모든 값은 프로퍼티 값이 될 수 있다 했다. 함수도 프로퍼티 값으로 사용할 수 있는데, 프로퍼티 값이 함수일 경우 일반 함수와 구분하기 위해 [메서드(Method)]()라고 부른다. 즉, 메서드는 객체에 묶여있는 함수를 의미한다. 

<img src="https://ifh.cc/g/fp7T09.png" style="max-width: 100%" align="center">

앞서 JS에서 원시 타입을 이외의 모든 타입은 객체 타입이라 했다. 함수도 객체 타입이며 JS에서 함수는 [일급 객체]()이므로 값으로 취급할 수 있다. 객체와 함수는 밀접한 관계를 가진다. JS에서 함수와 객체는 분리해서 생각할 수 없는 개념이므로 객체와 함수의 관계에 대해서 제대로 이해해야 한다. 이에 대해서는 [함수와 일급 객체](), [객체지향 프로그래밍]()의 내용을 참고하자
<br>

***
### 참고
- [모던 자바스크립트 Deep Dive](http://www.yes24.com/Product/Goods/92742567)
- [JavaScript MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- [JavaScript - 객체(Object)에 대해 알아보자](https://velog.io/@surim014/%EC%9B%B9%EC%9D%84-%EC%9B%80%EC%A7%81%EC%9D%B4%EB%8A%94-%EA%B7%BC%EC%9C%A1-JavaScript%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-part-7-Object-35k01xmdfp)
- [[Javascript] 동적으로 프로퍼티 추가](https://developer-talk.tistory.com/511)
- [객체(Object) | JavaScript로 만나는 세상](https://helloworldjavascript.net/pages/180-object.html)

