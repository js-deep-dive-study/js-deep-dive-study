# 원시 값과 객체의 비교

### 목차

- [1 개요](#1-개요)
- [2 원시 값](#2-원시-값)
  - [2-1원시 값의 변경 - 변경 불가능한 값](#2-1-원시-값의-변경---변경-불가능한-값)
  - [2-2 원시 값의 저장](#2-2-원시-값의-저장)
    - [2-2-1 원시 값이자 객체인 문자열](#2-2-1-원시-값이자-객체인-문자열)
  - [2-3 원시 값의 전달](#2-3-원시-값의-전달)
- [3 객체 값](#3-객체-값)
- [3-1 객체 값의 변경 - 변경 가능한 값](#3-1-객체-값의-변경---변경-가능한-값)
- [3-2 객체 값의 저장](#3-2-객체-값의-저장)
- [3-3 객체 값의 전달](#3-3-객체-값의-전달)

***

<br>

## 1 개요

JS에서 원시 타입([7가지 데이터 타입]()) 이외의 모든 값은 객체 타입으로 구분된다. 원시 타입과 객체 타입의 차이점에 대해 알아보자

| 구분      | 원시 타입                               | 객체 타입                                          |
| --------- | --------------------------------------- | -------------------------------------------------- |
| 값의 변경 | 변경 불가능한 값 Immutable              | 변경 가능한 값 Mutable                             |
| 값의 저장 | 실제 값을 메모리 공간에 저장            | 실제 값이 연결된 참조 값을 메모리 공간에 저장      |
| 값의 전달 | 값에 의한 전달(메모리 주소에 의한 전달) | 참조에 의한 전달                                   |
| 값의 크기 | 상대적으로 적은 메모리 소비             | 상대적으로 메모리의 효율적 소비가 어려울 수도 있음 |

<br>

## 2 원시 값

### 2-1 원시 값의 변경 - 변경 불가능한 값

한번 생성된 원시 타입의 값은 읽기 전용으로서 변경할 수 없고, 어떠한 일이 있어도 원시 값은 불변하다. 이러한 원시 값의 특성으로 인해 원시 값은 예기치 못한 데이터의 변경에서 자유로우며 이는 곧 데이터의 신뢰성을 보장한다는 의미다

원시 값이 변경 불가능하다는 말은 원시 값 자체를 변경할 수 없다는 뜻이지 변수는 언제든지 재할당을 통해 변수 값을 변경할 수 있다. 변수의 상대 개념인 상수(상수 선언 키워드 `const`를 이용한 변수 선언)와 불변 값이 동일한 개념이라 헷갈릴 수 있다. 상수는 재할당이 금지된 변수일 뿐이므로 불변 값과 동일 시 해서는 안된다

### 2-2 원시 값의 저장

앞선 [값의 할당](https://github.com/jacenam/WIL-archive/blob/main/JavaScript/JavaScript%20Basic%20Concepts/assignment.md#1-값의-할당) 및 [재할당](https://github.com/jacenam/WIL-archive/blob/main/JavaScript/JavaScript%20Basic%20Concepts/assignment.md#2-값의-재할당), [타입 변환]() 파트에서 언급되었던 메모리의 동작 원리를 복기해보자:

```jsx
/* 값의 할당 및 재할당 */ 
var userName = 'Jace'; 
userName = 'Nam'; 
```

<img src="https://ifh.cc/g/CR75tq.jpg" style="max-width: 100%" align="center">

원시 값인 문자열 타입 `‘Jace’`을 이미 할당한 변수 `userName`에 새로운 원시 값인 문자열 타입 `‘Nam’`을 재할당하면 메모리 공간에 저장되어 있는 `‘Jace’`에 재할당할 `‘Nam’`을 덮어 씌우는 것이 아니라 새로운 메모리 공간에 `‘Nam’`을 저장한 후, 변수 `userName`은 `‘Nam’`이 저장된 메모리 주소를 가리키게 되는 것이다.

위 메모리 동작 원리에서 볼 수 있듯이 원시 값은 값이 삭제되거나 덮어 씌워지는 것이 아닌 이전 값은 그대로 남아있되, 새로운 메모리 공간에 새롭게 재할당할 원시 값을 저장하며 이러한 원시 값의 특성을 불변성(Immutability)라고 한다

### 2-2-1 원시 값이자 객체인 문자열

원시 타입에서 한 가지 특이사항은 존재한다. 원시 타입인 문자열 타입은 원시 값이면서도 객체일 수도 있다. 문자열은 원시 값이자 [유사 배열 객체]()이면서 [이터러블]()이므로 [배열]()(`[]` 인덱스 등)과 유사하게 각 문자에 접근할 수 있다. 원시 값인 문자열이 객체일 수도 있다는 사실에 혼란스러울 수 있다. 이에 대해서는 [원시 값과 래퍼 객체]()(`length` 프로퍼티, `toUpperCase()` 메서드 등)를 참고하자

```jsx
var userName = 'Jace Nam'; 

// 문자열은 유사 배열이기에 배열과 유사하게 인덱스를 사용해 각 문자에 접근이 가능하다
console.log(userName[0]); // → J

// 원시 값인 문자열이 객체처럼 동작한다
console.log(userName.length); // → 8
console.log(userName.toUpperCase()); // → JACE NAM
```

문자열은 원시 값이면서도 객체가 될 수 있다 했으니 만약 문자열의 한 문자만 변경하고자 한다면 어떻게 될까? `userName[1] = ‘A’`의 재할당문과 상관없이 변수 `userName`의 최초 할당 값인 `‘Jace Nam’`을 그대로 반환한다. 이는 문자열이 유사 배열 객체로서 객체일 수도 있으나, 원시 값이기 때문에 원시 값의 불변성은 유효하다

```jsx
var userName = 'Jace Nam'; 

console.log(userName[1]); // → a

// 문자열은 배열과 유사하게 인덱스를 사용해 각 문자에 접근할 수 있다 했다
userName[1] = 'A'; // 에러가 발생하지 않는다

console.log((userName); // → Jace Name
```

### 2-3 원시 값의 전달

윈시 값이 할당된 변수를 다른 변수에 할당하면 원본의 원시 값이 복사되어 전달되며 이를 ‘값의 의한 전달’이라고 한다

엄격하게 따지자면 ‘값’의 의한 전달이 아닌 ‘메모리 주소'에 의한 전달이라는 표현이 더욱 정확하다. 변수 같은 식별자는 값이 아니라 메모리 주소를 기억하고 있기 때문이다

```jsx
var original = 100; 
var copy = original; 

original = 200; 

console.log(original, copy); // → 100 100
```

변수 `original`에 숫자 값 `100`을 할당하고, 변수 `copy`에 변수 `original`을 할당했다. `var copy = original`에서 변수 `orginal`은 숫자 값 `100`으로 평가되므로 변수 `copy`에도 새로운 숫자 값 `100`이 할당된다. 이처럼 원시 값을 갖는 변수를 다른 변수에 할당하면 원시 값이 복사되어 전달되며 이를 값의 의한 전달이라고 부른다. 하지만 변수 `original`과 변수 `copy`의 원시 값 `100`은 각각 다른 메모리 공간에 별도로 저장된 별개의 값이라는 것을 기억하자

<img src="https://ifh.cc/g/68ObK9.jpg" style="max-width: 100%" align="center">

그렇다면 만약 위 값의 의한 전달 예제에서 변수 `original`의 값을 변경해보면 어떻게 될까:

```jsx
var original = 100; 
var copy = original; 

console.log(original, copy); // → 100 100
console.log(original === copy); // → true

original = 200; 

console.log(original, copy); // → 200 100
console.log(original === copy); // → false
```

변수 `original`에 숫자 값 `200`을 재할당하면 값의 의한 전달로 인해 변수 `copy`에도 숫자 값 `200`이 복사되어 재할당되지 않는다. 위에서 언급했듯이 변수 `original`과 `copy`의 원시 값(변수 값)은 각각의 메모리 공간에 저장된 별개의 값이다. 따라서 변수 `original`에 새로운 값을 재할당해도 변수 `copy`에 이미 할당된 값은 간섭받지 않게되어 값이 복사되어 전달되지 않는다. 만약 값의 복사 및 전달이 필요하다면 `copy = original;`이라는 재할당문으로 값의 의한 전달을 다시 한번 더 명령해야 한다

<img src="https://ifh.cc/g/ObKYyw.jpg" style="max-width: 100%" align="center">

<br>

## 3 객체 값

객체는 프로퍼티의 개수 정해져 있지 않으며 프로퍼티의 값에도 제약이 없다. 따라서 객체는 복합적인 자료 구조인만큼 원시 값과는 다르게 메모리 공간의 크기를 사전에 확보 및 정해둘 수 없다. 또한, 객체는 경우에 따라 소비하는 메모리의 크기가 매우 클 수도 있다. 따라서 객체는 원시 값과 다른 방식으로 메모리가 동작하도록 설계되어 있다

> JS의 객체는 다른 언어에서의 객체와 다른 차별점이 있다. 이에 대해서는 [JS 객체]() 파트를 참고하자

### 3-1 객체 값의 변경 - 변경 가능한 값

객체 타입의 값, 즉 객체는 변경 가능한 값(Mutable Value)이다. 앞서 언급했듯이, 원시 값은 불변 값이므로 변수의 값을 변경하려면 값의 재할당 외에는 방법이 없다. 그러나 객체는 재할당 없이 [프로퍼티를 동적으로 추가, 갱신, 삭제]()하며 객체를 직접 변경할 수 있다

```jsx
var user = {
	name: 'Jace' 
}

// 마침표 프로퍼티 접근 연산자를 활용한 프로퍼티 재할당(갱신)
user.name = 'Ju Hyung'; 

// 마침표 프로퍼티 접근 연산자를 활용한 프로퍼티의 동적 생성(추가)
user.age = 30; 
console.log(user); // → { name: 'Ju Hyung', age: 30 }

// 마침표 프로퍼티 접근 연산자와 delete 연산자를 활용한 프로퍼티의 동적 삭제
delete user.name; 
console.log(user); // → { age: 30 }
```

### 3-2 객체 값의 저장

객체 값은 어떻게 저장되길래 변경 가능한 값이라는걸까? 변수에 객체를 할당(저장)했을 때 메모리의 동작을 살펴보자

```jsx
var user = {
	name: 'Jace'
};

var user = 'Jace'; 
```

원시 값이 할당된 변수(식별자)는 저장된 메모리 주소를 통해 원시 값에 바로 접근할 수 있다. 그러나 객체가 할당된 변수의 경우, 객체 값에 바로 접근 하는 것이 아닌 객체 값이 **저장된 참조 값(Reference Value)**에 접근하게 된다. 참조 값이란 객체(값)가 저장된 메모리의 주소(위 예제에서는 `0x00000003`)를 의미한다.

<img src="https://ifh.cc/g/BMdZF2.png" style="max-width: 100%" align="center">

<img src="https://ifh.cc/g/3C3nBy.png" style="max-width: 100%" align="center">

**결론적으로, 객체가 할당된 변수를 참조(호출)하면 참조 값을 통해 실제 객체 값에 접근할 수 있게 된다.** 이러하기에 원시 값이 할당된 변수의 경우 “변수가 `X`값을 갖는다”, “변수의 값은 `X`다”라고 표현한다. 하지만 객체가 할당된 변수의 경우 “변수가 객체를 가리키고 있다”, “변수가 객체를 참조하고 있다"라고 표현한다

객체는 변경 가능한 값이라고 하니 객체 값을 변경하면 어떻게 될까

```jsx
var user = {
	name: 'Jace' 
}

// 마침표 프로퍼티 접근 연산자를 활용한 프로퍼티 값의 재할당(갱신)
user.name = 'Ju Hyung'; 

// 대괄호 프로퍼티 접근 연산자를 활용한 프로퍼티의 동적 생성(추가)
user['age'] = 30; 

console.log(user); // → { name: 'Ju Hyung', age: 30 }
```

위 객체 값의 변경 코드를 실행할 시 아래 그림과 같이 메모리는 동작한다:

<img src="https://ifh.cc/g/D4J0Vw.jpg" style="max-width: 100%" align="center">

객체는 변경 가능한 값이므로 메모리에 저장된 객체를 직접 변경할 수 있다. 객체가 할당된 변수 `user`는 참조 값을 통해 실제 객체 값이 저장된 메모리에 접근해서 기존 객체를 수정하거나 새로운 객체 값(프로퍼티)을 추가할 수 있다. 참고로 변수에 아예 새로운 객체를 할당하지 않는 이상 참조 값은 변경되지 않는다

### 3-3 객체 값의 전달

객체는 원시 값처럼 일정한 타입이 정해져있지 않아 크기가 매우 클 수도 있고, [프로퍼티 값이 객체일 수도]()(객체 안에 객체) 있다. 따라서 메모리의 효율적 소비가 어려운 객체의 구조적인 단점을 감안해, 객체를 복사해서 생성하는 행위가 이뤄졌을 때 메모리 소비를 절약하기 위해 객체는 변경 가능한 값으로 설계되어 있는 것이다. 하지만 객체의 이러한 설계에 따른 부작용이 있다. 원시 값과는 다르게 여러개의 식별자가 하나의 객체를 공유할 수 있다는 점이다. 여러 개의 식별자가 하나의 객체를 공유할 수 있다는 것은 무엇을 의미하는 걸까?

```jsx
var user = {
	name: 'Jace'
}; 

var copy = user;
```

객체 값이 할당된 변수 `user`를 변수 `copy`에 할당하면 변수 `user`의 객체 값이 아닌 참조 값을 복사해서 변수 `copy`에 저장한다. 이때 변수 `user`와 변수 `copy`가 저장된 메모리 주소는 다르지만 동일한 참조 값 `0x00000003`을 갖는다. 다시 말해, 원본 변수 `user`와 사본 변수 `copy`는 모두 동일 객체를 가리킨다는 의미다. 이는 두 개의 식별자(변수)가 하나의 객체를 공유하는 것이며, 참조 값이 복사되어 전달되는 현상을 **참조에 의한 전달**이라고 부른다

<img src="https://ifh.cc/g/bNybak.jpg" style="max-width: 100%" align="center">

그렇다면 앞서 언급한대로, 객체 값이 변경 가능하도록 설계한 부작용은 무엇일까? 앞서 언급했듯이, 객체는 여러개의 식별자가 하나의 객체를 공유할 수 있다. 따라서 원본 변수 혹은 사본 변수 중 어느 한쪽에서 객체를 변경할 경우 서로 영향을 주고 받는다(변수에 새로운 객체를 재할당하는 것이 아닌 이상 객체의 프로퍼티 값을 변경하거나 프로퍼티를 추가 또는 삭제할 경우). 이는 객체 값이 변경이 가능하기에 생긴 부작용이라 볼 수 있다. 따라서 객체 관리에 주의가 필요하다

```javascript
var original = { name: "Jace", age: 30 };
var copy = original;

console.log(original === copy); // → true

// 프로퍼티 값의 변경
original.name = "Ju Hyung"; 
copy.residence = "Seoul";

console.log(original === copy); // → true
console.log(original); // → { name: "Ju Hyung", age: 30, residence: "Seoul" }
console.log(copy); // → { name: "Ju Hyung", age: 30, residence: "Seoul" }
```

결국 원시 값의 전달 방식인 ‘값의 의한 전달’과 객체 값의 전달 방식인 ‘참조에 의한 전달'은 식별자(변수)가 가리키는 메모리 공간에 저장되어 있는 값을 복사해서 전달하는 면에서 전달 메커니즘은 동일하다. 다만 식별자(변수)가 가리키는 메모리 공간에 저장되어 있는 값이 원시 값이냐 참조 값이냐에 따라 전달 방식만 달라지는 것이다

<img src="https://ifh.cc/g/xVvXVX.jpg" style="max-width: 100%" align="center">

여기서 주의해야 할 부분이 있다. 아래 예제를 살펴보면, 변수 `copy`에 객체 값을 가진 변수 `original`을 할당했다. 그리고 변수 `original`의 객체 값 중 프로퍼티 키 `name`의 프로퍼티 값을 `“Ju Hyung”`으로 변경해서 재할당했다. 그렇다면 변수 `original`과 `copy`는 일치할까?

```javascript
var original = { name: "Jace", age: 30 };
var copy = original;

console.log(original === copy); // → true

// 객체 값의 재할당
original = { name: "Ju Hyung", age: 30 };

console.log(original === copy); // true일까? false일까?
```

답은 `false`로 일치하지 않는다. 왜 그런 것일까? 이는 변수 `original`의 프로퍼티만을 변경한 것이 아니라 변수 `original`에 새로운 객체 값을 재할당했기 때문이다. 변수 `copy`에 할당된 기존의 변수 `original`의 값 `{ name: “Jace”, age: 30 }`와 변수 `original`에 새롭게 재할당한 `{ name: “Ju Hyung”, age: 30 }`의 값은 전혀 다른 값이다. 다시 말해, 프로퍼티 값 `“Ju Hyung”` 하나만이 변경된것처럼 보여도, 다른 메모리에 저장될 새로운 값을 변수 `original`에 할당했다는 뜻이다. 따라서 동일한 객체 값(참조 값)을 공유하는 두 변수의 객체 값을 수정할 때, 프로퍼티 접근 연산자를 통해 객체 값을 수정해야 된다

<img src="https://ifh.cc/g/SQfQXd.jpg" style="max-width: 100%" align="center">

그렇다면 아래 예제의 변수들은 같은 참조 값을 공유하는지, 값은 동일한지 살펴보자:

```jsx
var user1 = {
	name: 'Jace',
	age: 30
}; 

var user2 = {
	name: 'Jace', 
	age: 30
}; 

console.log(user1.name === user2.name); // → true
console.log(user1['age'] === user2['age']); // → true 
console.log(user1 === user2); // true일까? false일까?
```

객체가 할당된 변수는 참조 값이 저장된 메모리 주소를 가리키게 되고, 원시 값이 할당된 변수는 원시 값이 저장된 메모리 주소를 가리킨다. 즉, 객체가 할당된 변수는 참조 값을 가지고 되고, 원시 값이 할당된 변수는 원시 값 자체를 가지게 된다. 변수 `user1`과 변수 `user2`가 가리키는 객체 `{ name: ‘Jace’, age: 30 }`의 내용은 동일하지만 다른 변수에, 즉 다른 메모리에 저장된 별개의 객체다. 변수 `user1`과 변수 `user2`의 참조 값은 전혀 다른 값이다. 따라서 `user1 === user2`는 `false`다

<img src="https://ifh.cc/g/z8Zprf.jpg" style="max-width: 100%" align="center">

그러면 `user1.name === user2.name`과 `user1[’age’] === user2[’age’]`는 왜 `true`일까? 식별자(변수)를 통해 값을 참조(호출)하는 [식별자 참조]()는 값을 생성하지는 않지만 참조된 값은 값으로 평가되기 때문에 표현식이라 했다. 프로퍼티 값을 호출하는 `user1.name`, `user2.name`은 모두 표현식이며, 모두 원시 값 `‘Jace’`로 평가된다. 따라서 `user1.name === user2.name`은 `true`다(`user1[’age’] === user2[’age’]`도 동일한 이유로 `true`다)

```jsx
user1.name === user2.name => 'Jace' === 'Jace' => true
user1['age'] === user2['age'] => 'Jace' === 'Jace' => true
```

<br>

------

### 참고

- [모던 자바스크립트 Deep Dive](http://www.yes24.com/Product/Goods/92742567)
- [원시타입(primitive type)과 참조타입(reference type)](https://ryulog.tistory.com/140)
- [원시 값과 참조 값](https://wonyoung2257.tistory.com/28)
- [원시 타입과 참조타입](https://velog.io/@nomadhash/Java-Script-깊은-복사와-얕은-복사)
- [값 타입(value type) & 참조 타입(reference type)](https://eun-ng.tistory.com/10)
- [변수, 원시 값과 참조 값](https://feel5ny.github.io/2017/11/29/JS_01/)