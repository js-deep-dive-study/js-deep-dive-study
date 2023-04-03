# 4. 변수

## 4.1 변수란 무엇인가? 왜 필요한가?

### 1) 변수(variable)

- 메모리 공간을 식별하기 위한 이름이다.

### 2) 변수가 필요한 이유?

- 값을 재활용하기 위해 메모리에 값을 저장하고 읽어들이는 메커니즘이 필요하다.
- 값이 저장된 메모리 공간에 **직접 접근하는 건 치명적인 오류를 발생시킬 수 있다**.
    - 프로그램에서 접근해서는 안 되는 메모리에 접근해서 값을 변경하면 프로그램 실행에 영향을 줄 수 있다.
- 값이 저장될 메모리 주소는 코드가 실행될 때의 메모리 상황에 따라 임의로 결정된다.

### 3) 용어

- 변수 이름 : 값이 저장된 메모리 주소를 식별하기 위한 이름. 식별자(Identifier)라고도 부른다.
- 변수 값 : 변수 이름을 통해 접근할 수 있는 메모리 공간에 저장된 값.
- 할당(assignment) : 변수에 값을 저장하는 것.

## 4.2 식별자

### 1) 식별자(Identifier)

- 변수 이름을 식별자라고도 한다.
- 값이 저장된 메모리 주소와 매핑 관계
- 식별자와 메모리 주소의 매핑 관계도 메모리에 저장된다.

![identifier](https://user-images.githubusercontent.com/60080167/229606088-d552cbdf-1ebb-4421-99c2-7a43862e55ad.png)

### 2) 메모리 상에 존재하는 값을 식별할 수 있는 이름은 모두 식별자라고 부른다

- 변수 이름
- 함수 이름
- 클래스 이름

## 4.3 변수 선언

### 1) 변수 선언(Variable Declaration)

- 변수를 생성하는 것을 말한다.
- var, let, const 키워드를 사용한다.
    - var는 함수 레벨 스코프를 지원하기 때문에 의도치 않은 전역 변수가 선언되어 side-effect가 발생할 수 있다.

### 2) 변수 선언의 과정(var)

1. **선언 단계** : 자바스크립트 엔진에 변수의 존재를 알린다.
2. **초기화 단계** : 값을 저장하기 위한 메모리 공간을 확보하고 암묵적으로 undefined를 할당해 초기화한다.

### 3) 초기화의 이유

- 확보된 메모리 공간에 다른 애플리케이션이 사용했던 값(쓰레기 값)이 남아 있을 수 있다.
- 값을 할당하기 전에 변수 값을 참조하면 쓰레기 값이 나올 수 있다.

### 4) 용어

- 메모리 공간 확보(allocate) : 값을 위해 메모리 공간을 확보하는 것을 의미한다.
- 초기화(initialization) : 최초로 값을 할당하는 것을 의미한다.

## 4.4 변수 선언의 실행 시점과 변수 호이스팅

### 1) 변수 선언은 언제 실행되나?

- 모든 선언문(변수 선언문, 함수 선언문)은 런타임(소스코드가 실행되는 시점) 이전에 먼저 실행된다.

### 2) 호이스팅

- 변수 선언이 런타임 이전에 먼저 실행된다는 증거이다.
- 변수 선어문이 코드의 선두로 끌어올려진 것처럼 동작하는 자바스크립트 고유의 특징이다.

```jsx
console.log(foo); // undefined

var foo;
```

### 3) Temperal Dead Zone(TDZ)

- let의 변수 선언은 var와 다르게 선언 단계와 초기화 단계가 따로 실행된다.
- 선언 단계는 런타임 이전에 실행된다.
- 초기화 단계는 선언문 소스 코드에 도달했을 때 실행된다.
- 변수에 대한 접근은 `ReferenceError`를 발생시킨다.

```jsx
{
  // TDZ starts at beginning of scope
  console.log(bar); // undefined
  console.log(foo); // ReferenceError
  var bar = 1;
  let foo = 2; // End of TDZ (for foo)
}
```

![var-lifecycle([https://poiemaweb.com/js-data-type-variable](https://poiemaweb.com/js-data-type-variable))](https://user-images.githubusercontent.com/60080167/229606180-1057675d-c88a-4bc2-a4e6-be6d241e5903.png)

![let-lifecycle([https://poiemaweb.com/es6-block-scope](https://poiemaweb.com/es6-block-scope))](https://user-images.githubusercontent.com/60080167/229606195-7b63fb41-5ea5-4bbd-b518-60beebee5af2.png)

## 4.5 값의 할당

### 1) 할당(assignment)

- 할당 연산자(=)를 사용한다.
- 런타임(소스코드가 순차적으로 실행되는 시점)에 실행된다.
- 변수 선언과 할당을 하나의 문으로 단축 표현할 수 있다.
    - 실행은 2개의 문으로 나눠서 한다.

### 2) 새로운 메모리 공간에 값을 저장한다

- 초기값을 바꾸는게 아니라 새로운 값을 저장하고 그 주소를 매핑한다.

## 4.6 값의 재할당

### 1) 재할당

- undefined로 초기화되기 때문에 할당도 실제로는 재할당이다.
- 상수(const)는 재할당이 불가능하다.
- 재할당 되는 값을 메모리 공간에 새롭게 저장하고 그 주소를 매핑한다.

![identifier](https://user-images.githubusercontent.com/60080167/229606088-d552cbdf-1ebb-4421-99c2-7a43862e55ad.png)


![assignment](https://user-images.githubusercontent.com/60080167/229606377-84f20526-5e2e-4624-9beb-ed90bf2d16f2.jpg)


### 2) 해제

- 사용되지 않는 메모리 공간은 메모리에서 자동 해제(release)된다.
    - 어떤 식별자도 참조하지 않는 메모리 공간을 의미한다.
- 가비지 콜렉터를 통해 진행되기 때문에 언제 해제될지는 알 수 없다.

## 4.7 식별자 네이밍 규칙

### 1) 규칙

- 문자(특수문자 제외), 숫자, 언더스코어, 달러 기호
- 숫자로 시작할 수 없다.
- 예약어(reserved word)는 프로그래밍 언어에서 사용하고 있기 때문에 식별자로 사용할 수 없다.

### 2) 네이밍 컨벤션

```
// 카멜 케이스(camelCase)
var firstName;

// 스네이크 케이스(snake_case)
var first_name;

// 파스칼 케이스(PascalCase)
var FirstName;

// 헝가리언 케이스(typeHungarianCase)
var strFirstName;
var $elem = document.getElementById('myId'); // DOM 노드
var observable$ = fromEvent(document, 'click'); // RxJS 옵저버블
```