# 단축 평가

단축 평가(Short-circuit Evaluation)는 ‘단축해서 평가하다'라는 뜻으로, 표현식을 평가하는 도중에 평가 결과가 확정된 경우 나머지 평가 과정을 생략하는 것을 의미한다. 보통 [논리 연산]()을 수행할 때 단축 평가가 일어난다. 단축 평가가 어떻게 발생하는지 알아보자

### 목차

- [1 논리합 연산자에서의 단축 평가](#1-논리합-연산자에서의-단축-평가)
- [2 논리곱 연산자](#2-논리곱-연산자)
- [3 그래서 단축 평가는 어디에 쓰이는가](#3-그래서-단축-평가는-어디에-쓰이는가)

***

<br>

## 1 논리합 연산자에서의 단축 평가

`||` 논리합 연산자(OR, `||`)는 논리 연산의 대상인 피연산자들이 평가되어 하나라도 그 결과 값이 참이라면 `true`에 해당하는 값을 반환한다. 좌항에서 우항으로 평가가 진행되며 마지막 피연산자까지의 결과 값에 참이 없다면 마지막 `false`에 해당하는 값을 반환한다

```jsx
true || true; // → true
true || false; // → true
false || true; // → true
false || false; // → false
```

제어문과 삼항 조건 연산자의 조건식 평가 과정과 동일하게, `||` 논리합 연산자의 피연산자들은은 JS 엔진에 의해 평가되어 평가 결과가 Truthy 값 혹은 Falsy 값 두 가지로 분류되고 난 후 불리언 타입 `true` 또는 `false`로 암묵적 타입 변환되어 불리언 값을 생성한다. **단, 위에 언급했듯이 논리합 연산자에서는 `true`와 `false`에 해당하는 값을 최종적으로 반환한다**

```jsx
'cat' || 'dog'; // → 'cat'

// 위 논리합 연산자 표현식이 평가되고 결과가 반환되는 과정
'cat' => Boolean('cat') => Truthy => true // 결과 값이 참에 해당하는 문자열 값 'cat'을 반환
```

논리합 연산자에서 `false`로 평가되는 Falsy 값은 제어문과 삼항 조건 연산자와 동일하다. 위 예제에서 첫번 째 피연산자인 문자열 타입 `‘cat’`은 빈 문자열(`’’`)이 아니기 때문에 Truthy 값으로 분류되어 `true`로 평가된다. 그리고 `true`에 해당하는 `‘cat’`을 최종적으로 반환한다

바로 여기서 단축 평가가 발생한다. 논리합 연산자에서 `true`에 해당하는 값을 찾은 경우, 논리 연산 수행은 그 즉시 멈추고 바로 `true`에 해당하는 값을 반환한다. 즉, 두 번째 피연산자인 `‘dog’`까지 평가해보지 않아도 표현식의 결과가 `true`임을 알 수 있기 때문에 두 번째 피연산자의 평가 과정은 생략된다. `true` 값이 없는 경우도 살펴보자:

```jsx
'' || false || 0; // → 0

// 위 논리합 연산자 표현식이 평가되고 결과가 반환되는 과정
'' => Boolean('') => Falsy => false // 1단계 
false => Boolean(false) => Falsy => false // 2단계
0 => Boolean(0) => Falsy => false // 3단계
```

모든 피연산자가 `false`로 평가되는 경우, 마지막 `false`에 해당하는 값을 반환한다. 위 예제의 경우, 피연산자들이 모두 `false`로 평가되고 세 번째 피연산자인 `0`이 그대로 반환된다

<br>

## 2 논리곱 연산자

`&&` 논리곱 연산자(AND, `&&`)는 논리 연산의 대상인 피연산자들이 모두 참일 때만 `true`에 해당하는 값을 반환하며, 거짓이 하나라도 있다면 `false`에 해당하는 값을 반환한다. 논리곱 연산자의 평가 순서는 논리합 연산자와 동일하게 좌항에서 우항으로 평가가 진행되며, 불리언 타입으로의 암묵적 타입 변환 과정 또한 동일하다

```jsx
true && true; // → (두 번째) true
true && false; // → false
false && true; // → false
false && false; // → (첫 번째) false
```

여기서 주의해야할 점은 논리합 연산자와 논리곱 연산자의 단축 평가에서의 차이다

```jsx
'mouse' && 'rabbit'; // → 'rabbit'

// 위 논리곱 연산자 표현식이 평가되고 결과가 반환되는 과정
'mouse' => Boolean('mouse') => Truthy => true // 1단계 
'rabbit' => Boolean('rabbit') => Truthy => true // 2단계
'' && NaN; // → ''

// 위 논리곱 연산자 표현식이 평가되고 결과가 반환되는 과정
'' => Boolean('') => Falsy => false // 1단계에서 종료
```

논리합 연산자에서는 `true`에 해당하는 값을 찾은 그 즉시, 그리고 `true`에 해당하는 피연산자가 없을 때 마지막 `false`에 해당하는 값을 반환하는 단축 평가가 일어난다. 그러나 논리곱 연산자에서는 그 반대로 `false`에 해당하는 피연산자를 찾은 그 즉시, 그리고 모든 피연산자가 `true`일 때 마지막 `true`에 해당하는 값을 반환하는 단축 평가가 일어난다

<br>

## 3 그래서 단축 평가는 어디에 쓰이는가

1. 단축 평가를 통해 if문을 대체할 수 있다

   ```javascript
   // if문 예제 1
   var done = 'accomplished' && 'fulfilled'; 
   var message; 
   
   if ( done ) {
   	message = 'great job'; 
   } else {
   	message = 'keep trying';
   } 
   
   console.log(message); // → great job
   
   // 위 if문 예제를 논리 연산자로 대체
   var done = 'accomplished' && 'fulfilled'; 
   var message; 
   
   message = (done && 'great job') || 'keep trying'; 
   
   console.log(message); // → great job
   ```

   ```javascript
   // if문 예제 2 
   var done = '' || null; 
   var message; 
   
   if ( done ) { 
   	message = 'great job'; 
   } else {
   	message = 'keep trying'; 
   } 
   
   console.log(message); // → keep trying
   
   // 위 if문 예제를 논리 연산자로 대체
   var done = '' || null; 
   var message; 
   
   message = (done || [10, 20] ) && 'keep trying';   
   
   console.log(message); // → keep trying
   ```

2. 객체를 가리키기를 기대한 변수가 `null` 또는 `undefined`인지 아닌지 확인하고 프로퍼티를 참조할 때
3. 함수 매개변수에 기본값을 설정할 때
4. 옵셔널 체이닝 연산자
5. `null` 병합 연산자

<br>

***

### 참고

- [모던 자바스크립트 Deep Dive](http://www.yes24.com/Product/Goods/92742567)
- [삼항 연산자, Truthy와 Falsy, 단축 평가 논리 계산법](https://bbangson.tistory.com/56)
- [잘못 알고 있었던 논리 연산자](https://velog.io/@proshy/JS%EC%9E%98%EB%AA%BB-%EC%95%8C%EA%B3%A0-%EC%9E%88%EC%97%88%EB%8D%98-%EB%85%BC%EB%A6%AC%EC%97%B0%EC%82%B0%EC%9E%90)
- [타입변환과 단축평가](https://kongkong93.tistory.com/25)