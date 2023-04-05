# Chapter.9 타입 변환과 단축 평가

## 9.1 타입 변환이란?

- 값의 타입은 개발자의 의도에 따라 다른 타입으로 변경이 가능하다. 이를 **명시적 타입 변환** / **타입 캐스팅**이라 한다.
- 또는 표현식이 평가될 때, 자바스크립트 엔진에 의해 암묵적으로 타입이 변환되기도 한다. 이를 **암묵적 타입 변환** / **타입 강제 변환**이라 한다.
    - 새로운 타입 값을 만들어 단 한 번 사용하고 버린다.
- 타입 변환 예측 실패로 인한 오류를 예방하기 위해 타입 변환이 어떻게 동작하는지 이해하고 사용하자

## 9.2 암묵적 타입 변환

- 코드 문맥에 부합하지 않는 경우, 에러를 가급적 발생시키지 않기 위해 실행한다.

### 1) 문자열 타입으로 변환

- `+` 연산자의 피연산자 중 하나 이상 문자열이 있을 경우 문자열 연결 연산자로 동작한다.
- **심벌 타입은 문자열로 변환이 불가능하다.** 그 외의 타입은 변환이 가능하다.

```jsx
// 숫자 타입
0 + '' // "0"

// 불리언 타입
true + '' // "true"

// null 타입
null + '' // "null"

// undefined
undefined + '' // "undefined"

// 심벌 타입
(Symbol()) + '' // TypeError: Cannot convert a Symbol value to a string

// 객체 타입
({}) + '' // "[object Object]"
```

### 2) 숫자 타입으로 변환

- **산술 연산자(-*/)**의 역할은 숫자 값을 만드는 것이다. 그래서 산술 연산자의 모든 피연산자는 숫자 타입이어야 한다.
    - 숫자 타입으로 변환할 수 없는 경우는 **NaN**이 된다.
- **비교 연산자(<>)**의 피연산자는 문맥상 모두 숫자 타입이어야 한다.
- **+단항 연산자**
    - undefined는 NaN으로 변환된다.
    - symbol은 타입 에러 발생
    - 객체의 경우, 빈배열을 제외하고는 NaN

```jsx
// 문자열
+'' // 0
+'0' // 0
+'a' // NaN

// 불리언
+true // 1
+false // 0

// null
+null // 0

// undefined
+undefined // **NaN**

// 심벌 타입
+Symbol() // TypeError: Cannot convert a Symbol value to a string

// 객체 타입
+{} // NaN
+[] // **0
+[1] // NaN**
+(function(){}) // NaN
```

### 3) 불리언 타입으로 변환

**Truthy 값**

**Falsy 값**

- false
- undefined
- null
- 0, -0
- NaN
- ‘’(빈 문자열)

## 9.3 명시적 타입 변환

- 명시적 타입 변환 방법
    - 표준 빌트인 생성자 함수(String, Number, Boolean)를 new 연산자 없이 호출하는 방법
    - 빌트인 메서드를 사용하는 방법
    - (암묵적 타입 변환를 사용하는 방법)

### 1) 문자열 타입으로 변환

1. String 생성자 함수를 new 연산자 없이 호출
    
    ```jsx
    String(1); // "1"
    String(NaN); // "NaN"
    
    String(true); // "true"
    String(false); // "false"
    ```
    
2. Object.prototype.toString 메서드 사용
    
    ```jsx
    (1).toString(); // "1"
    (NaN).toString(); // "NaN"
    
    (true).toString(); // "true"
    (false).toString(); // "false"
    ```
    
3. 문자열 연결 연산자 사용
    
    ```jsx
    1 + ''; // "1"
    NaN + ''; // "NaN"
    
    true + ''; // "true"
    false + ''; // "false"
    ```
    

### 2) 숫자 타입으로 변환

1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
2. paresInt, parseFloat 함수 사용(문자열만 숫자로 변환 가능)
3. +단항 산술 연산자 사용
4. *산술 연산자 사용

parseInt vs Number

- parseInt는 문자가 나오기 전까지 숫자형태의 문자를 숫자 타입으로 변환
- Number는 숫자가 아닌 문자가 있으면 NaN 반환

![number-convert](https://user-images.githubusercontent.com/60080167/229862224-604a8fc4-37d0-4e85-a82b-bca2b6c63cec.png)

### 3) 불리언 타입으로 변환

1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
    
    ```jsx
    Boolean(Infinity); // true
    Boolean({}); // true
    Boolean([]); // true
    ```
    
2. ! (부정 논리 연산자)를 두 번 사용하는 방법
    
    ```jsx
    !!'false'; // true
    !!{}; // true
    !![]; // true
    ```
    

## 9.4 단축 평가

### 1) 논리 연산자를 이용한 단축 평가

- 논리곱 연산자(&&)
    - **첫 피연산자가 true면 다음 피연산자를 그대로 반환한다.**
    - **첫 피연산자가 false면 그대로 반환한다.**
    
    ```jsx
    'Cat' && 'Dog' // 첫 번째 피연산자가 true로 평가됨. 두 번째 피연산자 'Dog'을 그대로 반환한다.
    ```
    
- 논리합 연산자(||)
    - **첫 번째 피연산자가 false면 다음 피연산자를 그대로 반환한다.**
    
    ```jsx
    'Cat' && 'Dog' // 첫 번째 피연산자가 Truthy 값이므로 'Cat'을 그대로 반환한다.
    ```
    
- 이런 특징으로 삼항 조건 연산자 or if…else 문을 대체할 수 있다.
- 객체가 null 또는 undefined인 경우 객체의 프로퍼티를 참조하면 타입 에러가 발생한다.
    
    ```jsx
    let elem = null;
    let value = elem.value; // TypeError
    ---
    let elem = null;
    let value = elem && elem.value; // elem이 Falsy 값이면 elem, Truthy 값이면 elem.value로 평가
    ```
    
- 함수 매개변수 기본값(default parameter) 설정

### 2) 옵셔널 체이닝 연산자

- 옵셔널 체이닝 연산자(`?.`) ECMAScript2020에서 도입됨.
- 좌항의 피연산자가 **null / undefined인 경우** undefined 반환한다. 그렇지 않은 경우, 우항의 프로퍼티를 참조한다.

### 3) null 병합 연산자

- null 병합 연산자(`??`)는 ECMAScript2020에서 도입됨.
- 좌항의 피연산자가 **null / undefined**인 경우 우항의 피연산자를 반환한다.