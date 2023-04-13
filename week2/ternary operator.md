# 삼항 조건 연산자

### 목차

- [1 삼항 조건 연산자란](#1-삼항-조건-연산자란)
- [2 불리언 타입으로의 암묵적 타입 변환](#2-불리언-타입으로의-암묵적-타입-변환)
- [3 삼항 조건 연산자와 if…else 제어문](#3-삼항-조건-연산자와-if...else-제어문)

***

<br>

## 1 삼항 조건 연산자란

```jsx
조건문(조건식) ? 실행문1 : 실행문2; 
```

삼항 조건(Ternary) 연산자는 조건문의 평가 결과에 따라 반환할 값을 결정한다. JS의 유일한 삼항 연산자이며 부수 효과는 없다. 삼항 조건 연산자는 세개의 항(피연산자)을 하나의 항으로 연산 처리하는 방식이다

<img src="https://user-images.githubusercontent.com/92138751/231506968-e2524ce2-fef6-4e2d-a0ad-81d526ce8271.jpg" style="width: 100%" align="center">

첫 번째 피연산자는 `true`와 `false` 불리언 타입의 값으로 평가되며 평가 결과에 따라 두번째 또는 세번 째 피연산자를 반환한다. 각 실행문들(두 번째와 세 번째 피연산자)은 어떠한 데이터 타입이 들어갈 수 있다

<br>

## 2 불리언 타입으로의 암묵적 타입 변환

만약 조건문(첫 번째 피연산자)의 평가 결과가 불리언 값이 아니면 불리언 값으로 암묵적 타입 변환이 된다

```jsx
Boolean() ? 실행문1 : 실행문2; 

// 삼항 조건 연산자식
var x = 10; 

var result = x % 2 ? '홀수' : '짝수'; 
console.log(result); // → 짝수

// 위 삼항 조건 연산자식의 불리언 타입 변환 과정
var x = 10; 

var result = Boolean( x % 2 ) ? '홀수' : '짝수';
console.log(result); // → 짝수
```

`10 % 2`는 `0`이고, `0`은 불리언 값으로 암묵적 타입 변환이 되었을 때 `false`다

<br>

## 3 삼항 조건 연산자와 if…else 제어문

삼항 조건 연산자의 첫 번째 피연산자 또한 조건식이므로 `if…else` 문을 사용해도 삼항 조건 연산자 표현식과 유사하게 연산을 처리할 수 있다

```jsx
// 삼항 조건 연산자식
var score = 65; 

var result = score >= 60 ? 'pass' : 'fail'; 
console.log(result); // → pass

// 위 삼항 조건 연산자식 코드를 풀어쓴 것
var score = 65; 
var result; 

if ( score >= 60 ) {
	result = 'pass'; // → 'pass'
} else {
	result = 'fail';
}; 

console.log(result); // → pass
```

<br>

***

### 참고

- [모던 자바스크립트 Deep Dive](http://www.yes24.com/Product/Goods/92742567)