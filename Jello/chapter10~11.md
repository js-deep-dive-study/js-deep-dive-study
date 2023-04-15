### 프로퍼티 접근

브라우저에는 name이라는 전역변수가 존재한다.

```jsx
const person = {
	'last-name': 'Lee',
	1: 10
}
person.last-name // 브라우저: NaN
								 // Node.js: ReferenceError: name is not defined
person[1]; // 10
```

선언하지 않은 프로퍼티에 접근하면 undefined

- 변수는 Reference Error

```jsx
const nums = {
	1:1,
	2:2
}
here //Uncaught ReferenceError: here is not defined at <anonymous>:1:1

nums.here //undefined
```

### 변경 가능한 값

- 원시 타입은 변경 불가능한 값. → **데이터의 신뢰성**
- 상수는 재할당이 금지된 변수다.
- 참조값을 갖는 변수를 할당받으면 객체의 주소가 복사되어 저장된다.

### 문자열 불변성

개발 편의성을 위해서 유사 배열 객체/iterable로 만들어짐. 

하지만 본질적으로 **원시 타입이라 변경은 불가능**하다.

```jsx
let name = 'Jello';
name[4] = 'y';
console.log(name); // 'Jello'

for (let i = 0; i < name.length; i++) {
    if (i === name.length - 1) {
        name[i] = 'y';
    }
}
name // 'Jello'
```

일부만 변경하고 싶다면 배열이나 새로운 문자열을 만들면 된다.

```jsx
// 배열을 사용해 문자를 변경
let name = 'Jello';
const chars = name.split('');
chars[chars.length - 1] = 'y';
console.log(chars.join('')); // 'Jelly'

// 새로운 문자열 만들기
console.log(name.slice(0, -1) + 'y'); // 'Jelly'
console.log(`${name.substring(0, name.length - 1)}y`)
```

### 원시값이 불변성을 지키는 방식

값을 복사해서 다른 메모리 공간에 저장한다.

즉,  두 변수는 다른 메모리 공간을 가리키고 있다.

따라서, 두 원시값은 서로 간섭할 수 없다.

```jsx
let numberA = 10;
let numberB = numberB;

numberB = 30;
console.log(numberA); // 10
console.log(numberB); // 30
```

자바스크립트 엔진 내부 동작을 정확히 알 수 없다.

실제로는 같은 주소를 참조하고 있다가 재할당이 발생하면 새로운 공간에 재할당된 값을 저장하는 방식으로 동작할 수도 있다(like 파이썬)

### 객체가 변경 가능한 값인 이유

객체는 **크기가 일정하지 않고 매우 커질 수 있기 때문에** 원시값처럼 복사해서 생성하기에는 고려해야할 사항이 많다. 또한 프로퍼티로 객체를 가질 수 있기 때문에 **복사 비용이 많이 들** 가능성도 있다.

정리하자면, **메모리를 효율적으로 사용하기 위해** 변경 가능한 값으로 설계되어 있다.

이런 구조 때문에 여러 식별자가 하나의 객체를 공유할 수 있다.