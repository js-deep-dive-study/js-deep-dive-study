<img src="https://ifh.cc/g/MXNfT7.png" style="max-width: 100%" align="center">

<br>

### 목차

- [1 값의 할당](#1-값의-할당)
  - [1-1 값의 할당과 메모리](#1-1-값의-할당과-메모리)

- [2 값의 재할당](#2-값의-재할당)

- [3 값의 할당과 참조](#3-값의-할당과-참조)

***

<br>

## 1 값의 할당

앞서 모든 소프트웨어 프로그램은 [데이터 입력 - 처리 - 출력]의 과정을 통해 동작하며, 이러한 데이터 처리 과정에서 가장 필수적이고 기본적인 개념이 [변수](https://github.com/jacenam/WIL-archive/blob/main/JavaScript/JavaScript%20%EA%B8%B0%EB%B3%B8/%EB%B3%80%EC%88%98.md)라 했었다. 이때, 처리될 데이터의 입력은 변수에 지정해주어야 한다. 특정 데이터를 변수에 지정해주는 행위를 프로그래밍 언에서는 '할당(Assignment)'라 부르며, 할당 연산자(`=`, Assignment Operator)를 사용한다

아래 예제에서 볼 수 있듯이, `Jace`라는 우항의 값을 할당 연산자(`=`)를 통해 `userName`이라는 좌항의 변수에 할당하는 것이다. 프로그래밍 언어에서 할당 연산자는 '좌항과 우항이 같다'는 의미가 아니다

<img src="https://ifh.cc/g/6X8qcf.png" style="max-width: 100%" align="center" />

### 1-1 값의 할당과 메모리

변수에 값을 할당할 때는 JS 엔진은 기존 메모리 공간에 할당 값을 저장하는 것이 아니라 새로운 메모리 공간에 값을 저장한다. 예시를 살펴보자: 

아래 변수 선언문은 하나의 코드 문장처럼 보이지만, JS 엔진은 이를 (1) '변수의 선언' `var userName;`, (2) '값의 할당' `userName = Jace;`으로 2개의 문으로 나누어 실행한다

```javascript
var userName = "Jace"; 

// (1) var userName; 
// (2) userName = Jace; 
```

왜 두 번의 걸쳐 하나의 문(변수 선언문)을 실행하는 것일까? 이는 변수가 선언되고 변수에 값이 할당될 때 할당 값이 메모리에 저장되는 메커니즘 때문이다. 앞서 [변수의 선언](https://github.com/jacenam/WIL-archive/blob/main/JavaScript/JavaScript%20%EA%B8%B0%EB%B3%B8/%EB%B3%80%EC%88%98.md#5-%EB%B3%80%EC%88%98-%EC%84%A0%EC%96%B8)에서 살펴보았듯이, 변수 선언 단계에서는 변수에 할당될 값을 메모리에 저장하기 위한 공간에  `undefined`를 암묵적으로 할당해 해당 메모리 공간을 초기화시킨다

그리고 `undefined`가 할당(저장)된 메모리 공간 `0x00000001`에 할당 값 `Jace`을 저장하는 것이 아니라, 아예 다른 메모리 공간  `0x00000004`에 할당 값 `Jace`를 저장하는 것이다

<img src ="https://ifh.cc/g/8Jlt4m.png" max-width="100%" align="center" />

결국 값을 할당 또는 (뒤에 나올) 재할당할 때는 메모리에 있던 기존 값을 지우거나 새로운 값으로 대체하는 것이 아니라, 새로운 공간에 새로운 값을 저장하는 것이기 때문에 기존 값은 그대로 남이있게 된다. 즉, 한번 변수에 할당되어 메모리에 저장된 값은 변경될 수 없다는 성질을 띄기 때문에 이를 값의 불변성이라 부르기도 한다. 값의 불변성에 대해서는 데이터 타입 파트의 [원시 값과 객체의 비교]()에서 자세하게 다룰 예정이다

### 1-2 값의 할당 시점(feat. 호이스팅)

값의 할당은 런타임 이후에 실행된다. 앞서 [변수 호이스팅](https://github.com/jacenam/WIL-archive/blob/main/JavaScript/JavaScript%20%EA%B8%B0%EB%B3%B8/%EB%B3%80%EC%88%98.md#6-%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85)에서 언급했듯이, JS에서 런타임이란 소스코드가 JS 엔진에 의해 한 줄씩 순차적으로 실행되는 시점을 의미한다. 값의 할당은 변수 호이스팅이 발생하고 난 이후, 소스코드가 한 줄씩 실행되는 런타임 이후에 실행된다. 정리하자면: 

- 변수 선언의 실행 시점 - 소스코드가 순차적으로 실행되는 시점인 런타임 이전에 실행된다
- 값의 할당의 실행 시점 - 소스코드가 순차적으로 실행되는 시점인 런타임 이후에 실행된다

```javascript
// 변수 선언은 런타임 이전에 실행되고 호이스팅 된다
console.log(userName); // → undefined (ReferenceError가 발생하지 않는다)

var userName;
```

```javascript
// 값의 할당은 런타임 이후에 실행된다
console.log(userName); // → undefined

var userName; 
userName = "Jace"; 

console.log(userName); // → Jace
```

변수 선언과 값의 할당이 동시에(한 줄로) 이루어졌을 때도 변수 선언과 값의 할당의 실행 시점은 위 예제들과 동일하다

```javascript
console.log(userName); // → undefined

var userName = "Jace"; 

console.log(userName); // → Jace
```

JS는 소스코드가 한 줄씩 순차적으로 실행되지만, 변수 선언이 값의 할당보다 뒤에 위치해도 변수 선언과 값의 할당의 실행 시점으로 인해 에러 없이 코드가 실행된다

```javascript
console.log(userName); // → undefined

userName = "Jace"; 
var userName; 

console.log(userName); // → Jace
```

<br>

## 2 값의 재할당

재할당(Reassignment)이란 값이 할당되어진 변수에 새로운 값을 재차 할당하는 것을 의미한다

```javascript
var userName = "Jace";
userName = "Nam";
```

값의 할당과 동일하게, 새로운 값을 변수에 재할당할 때에도 기존 메모리 공간에 새로운 값을 대체하여 저장하는 것이 아니라 새로운 메모리 공간을 확보해서 재할당 값을 저장하는 것이다. 아래 예시를 살펴보자. 변수의 선언, 값의 할당, 값의 재할당 시 메모리에 저장되는 값을 보여준다. 값의 재할당이 불가능한 변수 선언 키워드도 존재한다(`const` 키워드). 이에 대해서는 스코프 파트를 참고하자

<img src="https://ifh.cc/g/qX8JaQ.jpg" max-width="100%" align="center" />

변수 `userName`의 이전 값인 `undefined`와 `Jace`는 어떤 식별자와도 연결되어 있지 않다. 식별자가 없어서 이렇게 재활용이 불가능해진 값들은 JS의 Garbage Collector에 의해 메모리에서 자동해제된다 (단, 메모리에서 언제 해제될지는 모른다) 

> JS는 Garbage Collector를 내장하고 있는 [매니지드 언어(Managed Language)]()로서 메모리 관리가 용이하고 메모리 누수도 방지한다

<br>

## 3 값의 할당과 참조

앞서 식별자(변수)를 값이 저장될 메모리에 연결해주는 것을 할당이라 했다. 반면 값이 저장된 메모리에 변수를 활용해 읽어드리는 것을 참조(Reference)라고 한다

```javascript
// 변수 선언 및 값의 할당
var userName = "Jace"; 

// 값의 참조
userName; // → Jace
```

변수 이름을 이용해 참조를 명령하면 JS 엔진은 변수 이름과 맵핑된 메모리 주소를 통해 메모리 공간에 접근하여 해당 메모리에 저장된 값을 반환한다. 변수에 저장될 수 있는 값은 모든 [데이터 타입(원시 타입과 객체 타입)]()이다.

<img src="https://ifh.cc/g/NHt25f.jpg" max-width="100%" align="center" />

<br>

***

### 참고

- [모던 자바스크립트 Deep Dive](http://www.yes24.com/Product/Goods/92742567)
