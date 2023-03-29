# JS Deep Dive

## **04장 변수**

### 4.1 변수란 무엇인가? 왜 필요한가?

- 변수는 프로그래밍 언어에서 데이터를 관리하기 위한 핵심 개념이다.
- 컴퓨터는 CPU를 사용해 연산하고, 메모리를 사용해 데이터를 기억한다.
  - 메모리는 데이터를 저장할 수 있는 메모리 셀의 집합체이다.
  - 메모리 셀 하나의 크기는 1바이트(8비트)이다.
  - 1바이트 단위로 데이터를 저장하거나 읽어들인다.
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7a42d7ef-1895-4134-ab03-5b0ad63958f8/Untitled.png)
  - CPU가 연산(10 + 20)해서 만들어낸 30이라는 숫자는 재사용할 수 없다.
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4b853cb8-b161-4d68-9471-ce48bb65a13e/Untitled.png)
  - 위 그림처럼 30이 저장된 메모리 공간에 직접 접근하는 것 외에는 방법이 없다.
  - 메모리 주소를 통해 값에 직접 접근하는 것은 치명적 오류를 발생시킬 가능성이 매우 높다.
- 변수는 하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 그 메모리 공간을 식별하기 위해 붙인 이름을 말한다.
- 변수 관련 용어
  - 변수 이름(변수 명): 메모리 공간에 저장된 값을 식별할 수 있는 고유한 이름
  - 변수 값: 변수에 저장된 값
  - 할당(대입, 저장): 변수에 저장하는 것
  - 참조: 변수에 저장된 값을 읽어 들이는 것

### 4.2 식별자

- 변수 이름을 식별자라고도 한다.
- 식별자는 값이 아니라 메모리 주소를 기억하고 있다.
- 변수, 함수, 클래스 등의 이름은 모두 식별자이다.
- 식별자 관련 용어
  - 선언 declaration : 자바스크립트 엔진에 식별자의 존재를 알린다.

### 4.3 변수 선언

- 변수 선언은 변수를 생성하는 것을 말한다.
  - 값을 저장하기 위한 메모리 공간을 확보하고 변수 이름과 확보된 메모리 공간의 주소를 연결해서 값을 저장할 수 있게 준비하는 것이다.
- 변수를 사용하려면 반드시 선언이 필요하다.
- 변수 선언에는 `var`, `let`, `const` 키워드를 사용한다.
  - ES6(2015년)에서 let과 const가 도입되었다.
- 변수 선언을 하고 변수에 값을 할당하지 않았으면, 확보된 메모리 공간이 비어있지 않고 undefined 값이 할당되어 초기화된다.
- 변수 선언 단계
  1. 선언 단계 : 변수 이름을 등록해서 자바스크립트 엔진에 변수의 존재를 알린다.
  2. 초기화 단계 : 값을 저장하기 위한 메모리 공간을 확보하고 암묵적으로 undefined를 할당해 초기화한다.
  - var를 사용한 변수 선언은 선언 단계와 초기화 단계가 동시에 진행된다.
- 변수 이름을 비롯한 모든 식별자는 실행 컨텍스트에 등록된다.
  - 자바스크립트 엔진이 소스코드를 평가하고 실행하기 위해 필요한 환경을 제공하고 코드의 실행 결과를 관리하는 영역이다.
  - 변수 이름과 변수 값은 실행 컨텍스트 내에 키 / 값 형식인 객체로 등록되어 관리된다.
- 초기화란 변수가 선언된 이후 최초로 값을 할당하는 것을 말한다.

### 4.4 변수 선언의 실행 시점과 변수 호이스팅

```jsx
console.log(score); // undefined

var score;
```

- 변수 선언이 소스코드가 한 줄씩 순차적으로 실행되는 시점, 즉 런타임이 아니라 그 이전의 단계에서 먼저 실행되기 때문이다.
- 런타임 전에 소스코드의 평가 과정을 거치면서 소스코드를 실행하기 위한 준비를 한다.
- 이처럼 변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 특징을 변수 호이스팅이라 한다.
  - var, let, const, function, function\*, class 키워드로 선언한 식별자는 호이스팅 된다.

### 4.5 값의 할당

```jsx
console.log(score); // undefined

var score = 88;

console.log(score); // 88
```

- 변수 선언은 소스코드가 순차적으로 실행되는 시점인 런타임 이전에 먼저 실행된다.
- 할당은 소스코드가 순차적으로 실행되는 시점인 런타임에 실행된다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5e936a33-0804-4db3-9f12-00a5766d02fa/Untitled.png)

- 변수에 값을 할당할 때 undefined가 저장되 있던 메모리 공간을 지우는 것이 아니다.
- 새로운 메모리 공간을 확보하고 그곳에 할당 값 80을 저장한다.

```jsx
console.log(score); // undefined

score = 80;
var score;

console.log(score); // 80
```

🤔 `score = 80`에 아무 오류가 없다는 것이.. 맞는 건가요?

### 4.6 값의 재할당

- var 선언한 변수는 선언과 동시에 undefined로 초기화되기 때문에 엄밀히 말하자면 변수에 처음으로 값을 할당하는 것도 사실은 재할당이다.
- 값을 재할당할 수 없어서 변수에 저장된 값을 변경할 수 없다면 변수가 아니라 상수constant라 한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6270b331-29bd-45b7-8dd7-11faceb4b503/Untitled.png)

- 재할당 또한 새로운 메모리 공간을 확보하고 그 메모리 공간에 숫자 값을 저장한다.
- score의 이전 값인 undefined, 80은 가비지콜렉터에 의해 메모리에서 자동 해제된다.
- 언매니지드 언어와 매니지드 언어
  - 자바스크립트는 매니지드 언어로 메모리의 할당 및 해제를 위한 메모리 관리 기능을 언어 차원에서 담당하고 개발자의 직접적인 메모리 제어를 허용하지 않는다.

### 4.7 식별자 네이밍 규칙

```jsx
// 카멜 케이스
var firstName;

// 스네이크 케이스
var first_name;

// 파스칼 케이스
var FirstName;

// 헝가리언 케이스
var strFirstName;
var $ele = document.getElementById("mtId");
var observables$ = fromEvent(document, "click");
```

## 05장 표현식과 문

### 5.2 리터럴 literal

- 리터럴은 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용해 값을 생성하는 표기법notation을 말한다.
- 자바스크립트 엔진은 코드가 실행되는 시점인 런타임에 리터럴을 평가해 값을 생성한다.

### 5.3 표현식 expression

- 표현식은 값으로 평가될 수 있는 문이다. 즉, 표현식이 평가되면 새로운 값을 생성하거나 기존 값을 참조한다.

```jsx
// 리터럴 표현식
10;
("Hello");

// 식별자 표현식 (선언이 이미 존재한다고 가정)
sum;
person.sum;
arr[1];

// 연산자 표현식
10 + 20;
sum = 10;
sum !== 10;

// 함수와 메서드 호출 표현식 (선언이 이미 존재한다고 가정)
square();
person.getName();
```

- 표현식과 표현식이 평가된 값은 동등한 관계, 즉 동치equivalent이다.

### 5.4 문 statement

- 프로그램을 구성하는 기본 단위이자 최소 실행 단위이다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/65630c21-5f02-4d24-be3b-cc68db13fc92/Untitled.png)

```jsx
// 변수 선언문
var x

// 할당문
x = 5

// 조건문
function foo() {}

// 반복문
for (var i = 0; i < 2; i++) {...}
```

###

## 06장 데이터 타입

- Primaitive type
  - number
  - string
  - boolean
  - undefined
  - null
  - symbol
- object type
  - object
  - function
  - array

### 6.3 템플릿 리터럴

```jsx
const person = "Mike";
const age = 28;

function myTag(strings, personExp, ageExp) {
  const str0 = strings[0]; // "That "
  const str1 = strings[1]; // " is a "
  const str2 = strings[2]; // "."

  const ageStr = ageExp > 99 ? "centenarian" : "youngster";

  // We can even return a string built using a template literal
  return `${str0}${personExp}${str1}${ageStr}${str2}`;
}

const output = myTag`That ${person} is a ${age}.`;

console.log(output);
// That Mike is a youngster.
```

🤔 템플릿 리터럴로 함수를 호출할 수 있다.

### 6.7 심벌 타입

- 변경 불가능한 원시 타입의 값이다.
- 다른 값과 중복되지 않는 유일무이한 값이다.
- 함수를 호출해 생성한다.
- 생성된 심벌 값은 외부에 노출되지 않는다.

```jsx
// 심벌 값 생성
var key = Symbol('key')
console.log(typeof key)  // symbol

// 객체 생성
var obj = {}

// 이름이 충돌할 위험이 없는 유일무이한 값인 심벌을 푸로퍼티 키로 사용
obj[key] = 'value'
console.log(obj[key]).   // value
```

### 6.9 데이터 타입의 필요성

- 데이터 타입에 의한 메모리 공간의 확보와 참조
- 데이터 타입에 의한 값의 해석

### 6.10 동적 타이핑

- 자바스크립트의 변수는 정적 타입 언어와 같이 미리 선언한 데이터 타입의 값만 할당할 수 있는 것이 아니다. 어떠한 데이터 타입의 값이라도 자유롭게 할당할 수 있다.
- 자바스크립트의 변수는 선언이 아닌 할당에 의해 타입이 결정된다. (타입 추론)
- 재할당에 의해 변수의 타입은 언제든지 동적으로 변할 수 있다. 이러한 특징을 동적 타이핑이라고 한다.
- 변수는 타입을 가지지 않는다.

### 6.10.2 동적 타입 언어와 변수

- 변수의 유효 범위(스코프)는 최대한 좁게 만들어 변수의 부작용을 억제해야 한다. 변수의 유효 범위가 넓을수록 변수로 인한 오류가 발생할 확률이 높아진다.
  - 전역 변수는 최대한 사용하지 않도록 한다. 의도치 않게 값이 변경될 가능성이 높고 다른 코드에 영향을 줄 가능성도 높다.
  - 또한 오류의 추적을 특정하기 어렵게 만든다.
- 변수보다는 상수를 사용해 값의 변경을 억제한다.
- 변수 이름은 변수 목적이나 의미를 파악할 수 있도록 네이밍한다. 이는 협업과 생산성 향상에 도움을 준다.
