# 제어문의 종류

### 목차

- [1 조건문](#1-조건문)
  - [1-1 if…else문](#1-1-if...else문)
  - [1-2 switch문](#1-2-switch문)
- [2 반복문](#2-반복문)
  - [2-1 for문](#2-1-for문)
  - [2-2 while문](#2-2-while문)
  - [2-3 do…while문](#2-3-do...while문)
- [3 반복문과 switch문의 제어](#3-반복문과-switch문의-제어)
  - [3-1 break문](#3-1-break문)
  - [3-2 레이블(Label) 문](#3-2-레이블(Label)-문)
  - [3-3 continue문](#3-3-continue문)

***

<br>

## 1 조건문

조건문(Conditional Statement)은 주어진 조건식 평가 결과에 따라 특정 코드 블록(블록문)의 실행 여부를 결정한다. 조건식은 평가되어 불리언 값을 생성할 수 있는 [표현식]()이어야 한다

### 1-1 if…else 문

`if…else`문은 주어진 조건식의 평가 결과 참 또는 거짓에 따라 실행할 코드 블록을 결정한다. 조건식의 평가 결과가 불리언 값 `true`일 경우 `if` 문의 코드 블록이 실행되고, 불리언 값 `false`일 경우 `else` 문의 코드 블록이 실행된다

```jsx
var x = 10; 

if ( x % 2 ) {
	console.log('홀수'); 
} else {
	console.log('짝수'); // → 짝수
}
```

위 예제에서 `10 % 2`는 `0`이다. `0`은 `false`로 암묵적 타입 변환된다. 이처럼 `if` 문의 조건식이 불리언 값이 아닌 다른 값으로 평가될 경우, 해당 값은 JS 엔진에 의해 암묵적으로 불리언 값으로 타입 변환되어 실행할 코드 블록을 결정한다. 이에 대해서는 [**타입 변환과 단축 평가**]()를 참고하자

조건식을 추가해서 조건에 따라 실행될 코드 블록을 늘리고 싶으면 `else if` 문을 덧붙여서 사용한다.

```jsx
if (조건식 1) {
	// 조건식 1이 참이면 이 코드 블록이 실행된다 
} else if (조건식 2) {
	// 조건식 2가 참이면 이 코드 블록이 실행된다 
} else {
	// 조건식 1과 조건식 2가 모두 거짓이면 이 코드 블록이 실행된다 
} 
```

`if` 문과 `else` 문은 2번 이상 사용할 수 없지만 `else if` 문은 여러 번 사용할 수 있다. 그러나 조건식과 실행될 코드 블록의 수가 늘어나면 가독성이 떨어진다

```jsx
var upDown = 147; 

if ( upDown === 160)  {
	console.log('Down'); 
} else if ( upDown === 150 ) {
	console.log('Down')
} else if ( upDown === 140 ) {
	console.log('Up'); 
} else if ( upDown === 145 ) {
	console.log('Up'); 
} else if ( upDown === 147 ) { 
	console.log('정답'); // → 정답
} else {
	console.log('못 맞추겠다'); 
}
```

대부분의 `if…else` 문은 [삼항 조건 연산자]()로 바꿔 쓸 수 있다

```jsx
// if...else 조건문
var x = 10; 
var result; 

if ( x % 2 ) {
	result = '홀수'; 
} else {
	result = '짝수'; 
}

console.log(result); // → 짝수

// 삼항 조건 연산자 
var x = 10; 
var result = x % 2 ? '홀수' : '짝수'; 

console.log(result); // → 짝수
```

### 1-2 switch문

`switch`문은 `case`문, `default`문으로 이루어진 조건문이다. `default`문을 사용할지는 선택사항이다.

```jsx
switch (표현식) {
	case 표현식1: 표현식의 값과 표현식1의 값이 일치하면 실행될 문; 
	case 표현식2: 표현식의 값과 표현식2의 값이 일치하면 실행될 문; 
	default: 표현식의 값과 표현식1, 표현식2의 값이 일치하지 않을 떄 실행될 문; 
}
```

`switch`문의 표현식을 평가해서 생성되는 값과 동일하게 값을 생성하는 `case`문의 표현식이 존재한다면, 그 `case`문을 실행하는 것이다. 만약 `switch`문의 표현식과 일치하는 `case`문이 없을 때는 `default`문을 실행한다.

`if…else`문의 조건식은 참과 거짓의 불리언 값으로 평가되어야 하지만 `switch`문의 표현식은 불리언 값보다는 문자열이나 숫자 값인 경우가 더 많다. 다시 말해, `switch`문은 논리적 참, 거짓보다는 실행할 코드 블록을 결정할 때 사용한다.

예시로 살펴보자:

```jsx
var user = 'Jace';

switch (user) {
	case 'Ju Hyung': user = 'Ju Hyung Nam'; 
	case 'Jace': user = 'Jace Nam'; 
	default: console.log('일치하는 사용자가 없습니다'); 
}

console.log(user); // → Jace Nam
```

1. `switch (user)`에서 괄호(`()`) 안에 들어가는 `user`는 평가되어 문자열 값 `‘Jace’`를 참조하게 하는 식별자 표현식이다
2. 첫 번째 `case`의 `‘Ju Hyung’`은 평가되어 문자열 `‘Ju Hyung’`을 생성하는 표현식이기는 하나, `switch`문의 식별자 표현식인 `user`와 동일한 값을 생성하지 않으므로 첫 번째 `case`문 `user = ‘Ju Hyung Nam’;`을 실행하지 않는다
3. 두 번째 `case`의 `‘Jace’`는 평가되어 문자열 `‘Jace’`를 생성하는 표현식이며, `switch`문의 식별자 표현식인 `user`와 동일한 값을 생성하므로 두 번째 `case`문 `user = ‘Jace Nam’;`을 실행한다

위 예제를 가져와서 다시 살펴보자. 실제로 예제를 실행할 경우, 콘솔에 변수(식별자) `user`의 값을 참조해서 반환하기를 요구했는데 콘솔에는 `일치하는 사용자가 없습니다`도 반환된다. 왜 그런 것일까?

```jsx
var user = 'Jace';

switch (user) {
	case 'Ju Hyung': user = 'Ju Hyung Nam'; 
	case 'Jace': user = 'Jace Nam'; 
	default: console.log('일치하는 사용자가 없습니다'); // → 일치하는 사용자가 없습니다
}

console.log(user); // → Jace Nam
```

이를 **폴스루(Fall Through)**라고 하며, `switch` 문의 표현식 평가 결과와 일치하는 두 번째 `case`문의 `user = ‘Jace Nam’;` 재할당 코드 블록이 실행된 것은 맞지만 코드 블록을 실행한 후 `switch`문의 코드블록(`{ }`)을 탈출하지 않고 `switch`문이 끝날때까지 `default`문의 `console.log(’일치하는 사용자가 없습니다');` 코드블록을 실행했기 때문이다.

이러한 결과가 나온 이유는 `break`문을 사용하지 않았기 때문이다. `break`문은 `switch`문의 코드블록(`{}`)에서 코드의 흐름을 탈출시키는 역할을 한다. `break`문을 사용하면 `switch`문의 표현식과 일치하는 `case`문을 도달했을 때 다음 `case`문 또는 `default`문이 실행되지 않게 코드의 흐름을 `switch`문의 코드블록(`{}`)에서 탈출시킬 수 있다.

```jsx
var user = 'Jace';

switch (user) {
	case 'Ju Hyung': user = 'Ju Hyung Nam'; 
		break;
	case 'Jace': user = 'Jace Nam'; 
		break;
	default: console.log('일치하는 사용자가 없습니다');
}

console.log(user); // → Jace Nam
```

코드 실행은 두 번째 `case`문에서 멈춘다. `default`문을 실행하지 않을 뿐더러, 만약 세 번째, 네 번째 `case`문이 존재하더라도 실행하지 않는다

`break`문을 의도적으로 사용하지 않아 `폴스루`를 활용하는 방법도 있다. 폴스루를 활용해 여러 개의 `case`문을 하나의 조건으로 사용할 수도 있다:

```jsx
// 입력 받은 연도가 윤년인지 판별해서 2월의 일수를 반환(입력 받은 값이 숫자만일 때 판별기 실행)
var year = prompt('연도를 입력해주세요'); 
var month = 2; 
var days; 

if ( isNaN(year) === true ) {
	alert(`입력해주신 "${year}"는 숫자가 아니라 판별이 불가능합니다`);
	window.location.reload();
} else {
	switch ( month ) {
	    case 1: case 3: case 5: case 7: case 8: case 10: case 12: days = 31; 
	        break;
	    case 4: case 6: case 9: case 11: days = 30; 
					break;
	    case 2:
	        days = ( year % 4 === 0 && year % 100 !== 0) || ( year % 400 === 0 ) ? 29 : 28; 
	        ( year % 4 === 0 && year % 100 !== 0) || ( year % 400 === 0 ) ? document.write(`${year}년은 윤년이고 ${year}년의 2월은 ${days}일 입니다`) : document.write(`${year}년은 윤년이 아니고 ${year}년의 2월은 ${days}일 입니다`);
	        break; 
	}
}
```

- `isNaN()`함수는 숫자가 아닌 값을 판별하는 함수다. 괄호(`()`)안에 들어오는 표현식 혹은 값이 숫자가 아닐 경우 불리언 값 `true`를, 숫자인 경우 불리언 값 `false`를 반환한다
- `window.location.reload()`는 현재의 페이지를 새로고침하는 메소드다

만약 `if…else`문으로 해결할 수 있다면 `switch`문보다 `if…else`문을 사용하는 편이 좋다. 그러나 조건이 너무 많거나 복잡할 경우 `if…else`문보다 `switch`문을 사용했을 떄 가독성이 더 좋은 경우도 있다. 따라서 `if…else`문, `switch`문 중 필요에 따라 대응해서 사용하는 것을 권장한다(항상 `switch문`이 가독성이 좋다는 얘기는 아니다)

<br>

## 2 반복문

반복문(Loop Statement)은 조건식을 평가해 참인 경우 코드블록(`{}`)을 실행하고, 그 후 조건식을 다시 평가해서 여전히 참인 경우 코드블록을 다시 실행한다. 이처럼 조건식을 반복해서 평가하여 거짓일 때까지 반복된다. JS에서는 `for`문, `while`문, `do…while`문 총 세 가지의 반복문을 제공한다.

JS에서는[ `forEach` 메서드](), [`for…in`문](), [`for…of`문]()과 같이 반복문을 대체할 수 있는 다양한 기능을 제공한다

### 2-1 for문

`for`문은 조건식이 거짓으로 평가될 때까지 코드블록을 반복 실행한다

```jsx
for ( 변수 선언문 또는 할당문; 조건식; 증감식 ) {
	조건식이 참일 경우 반복적으로 실행될 문;
}
```

예시로 살펴보자:

```jsx
for ( var i = 1; i < 5; i++ ) {
	console.log(i); // → 1 2 3 4
}
```

변수 이름을 `i`로 사용하는 이유는 반복문에서 반복을 의미하는 iteration의 맨 앞 알파벳을 따온 것이다. 반복문의 변수 이름을 꼭 `i`로 지정할 필요는 없지만 `i`를 사용하는 것이 일반적이다

반복문의 실행 순서를 알아보자:

<img src="https://user-images.githubusercontent.com/92138751/231492888-db25855c-f807-4963-983c-cb7a7dec4afb.png" style="width: 100%" align="center">

1. `for`문을 실행하면 가장 먼저 변수 선언문 ① `var i = 0;` 이 실행된다. **변수 선언문은 반복 사이클 전체에서 단 한번만 실행된다**
2. 변선 선언문 ①의 실행이 완료되면 조건식 ② `i < 5`가 실행된다. 변수 `i`의 값은 `1`이므로 평가 결과는 `true`다
3. **(주의)** 조건식 ②의 평가 결과가 `true`이므로 코드블록 ③ `console.log(i);`가 실행된다. **증감문 ④ `i++;`은 바로 실행되는 것이 아니다!**
4. 코드블록 ③의 실행이 종료되면 증감문 ④ `i++;`가 실행되어 변수 `i`의 값이 `1`만큼 증가한다
5. 증감문 ④의 실행이 종료되면 변수 선언문 ①이 아닌 조건식 ②가 다시 실행되는 것이다

정리하자면, `for`문의 실행 순서는 ① → ② → ③ → ④ → (② → ③ → ④)  → (② → ③ → ④)…로 조건식 ②의 평가 결과가 `false`가 될때까지  (② → ③ → ④)가 반복된다. 위에 언급했듯이, **중요한 것은 증감문은 조건식이 평가되어 코드블록을 실행한 이후에 실행된다는 것이다**

`for`문 내에 `for`문을 중첩해 사용하는 것도 가능하며 이를 중첩 `for`문이라 부른다. 예시로 살펴보자:

```jsx
// 주사위를 던졌을 때 두 눈의 합이 6이 되는 경우의 수를 출력하기 위한 중첩 for문
for ( var i = 1; i <= 6; i++ ) {
	for ( var j = 1; j <= 6; j++) {
		if ( i + j === 6 ) {
			document.write(`${i}, ${j}<br>`);
		}
	}
}
// 도큐먼트 상 결과
1, 5
2, 4
3, 3
4, 2
5, 1
```

`document.write()` 메소드 내 `<p></p>`를 넣지 않으면 개행(줄바꿈) 없이 결과가 출력된다. `<p></p>` 말고 `<br>` 태그도 이용 가능하다 이 `console.log()` 메소드 이용 시 `<p>` 태그 없이 깔끔하게 출력이 가능하다

### 2-2 while문

`while`문은 조건식을 평가해 참이면 코드블록을 계속해서 반복 실행한다. `for`문은 반복 횟수가 명확할 때 사용하고, `while`문은 반복 횟수가 불명확할 때 주로 사용된다는 차이점이 있다

```jsx
while ( 조건식 ) {
		조건식이 참일 경우 반복적으로 실행될 문; 
}
```

`while`문은 조건식이 참일 경우 반복적으로 코드블록을 실행하다가, 조건식이 거짓이 되면 반복문의 실행을 종료한다. 만약 조건식의 평가 결과가 불리언 값이 아닐 경우 불리언 값으로 타입 변환해서 참, 거짓을 구별한다

```jsx
// (1)
var num = 0; 

while ( num < 5 ) {
	console.log(num); // → 0 1 2 3 4
	num++; 
}
```

만약 여기서 증가문 `num++`을 `console.log(num)`보다 먼저 사용하게 되면 어떻게 될까?

```jsx
// (2)
var num = 0; 

while ( num < 5 ) {
	num++; 
	console.log(num); // → 1 2 3 4 5
}
```

할당문(변수선언 및 할당문), 조건식은 모두 동일한데 어째서 값이 다른것일까? 그건 단순히 코드가 위에서 아래 방향 순서대로 실행되기 때문이다. (1) 예제에서 변수 선언과 값의 할당 `var num = 0`이 이루어지고, 조건식 `num < 5`의 평가가 진행되어 `console.log()` 메서드를 실행한 후 증감문 `num++`(`num = num + 1`)을 실행하게 된다. (2) 예제에서는 조건식 평가까지는 코드 진행 순서가 (1) 예제와 동일하다. 그러나 증감문 `num++`(`num = n + 1`)이 먼저 실행되어 `num`의 값이 먼저 `1`로 증가되고 그 이후 콘솔 메서드가 실행된다

<img src="https://user-images.githubusercontent.com/92138751/231493496-8c0b90bc-9a81-44d3-b165-20d1cea47b97.png" style="width: 100%" align="center">

`for`문 예제와 동일하다. 변수 선언문 ①이 먼저 실행되고 조건식 ②이 실행되며, 코드블록 ③ 콘솔 메서드가 실행되고 난 이후 증감문 ④이 실행되는 것이다. `while`문 (2) 예제처럼 ① → ② → ④ → ③의 순서로 for문이 진행되는 것이 아니다

`while`문에서 조건식의 평가 결과가 언제나 참이면 무한루프가 되며, 코드블록을 무한히 반복 실행하게 된다

```jsx
var num = 0; 

while ( 0 == false ) {
	console.log(num); // → 0, 1, 2, 3 ... 20001, 20002, 20003 ...
	count++;
}
```

`while`문에서 조건식의 평가 결과가 언제나 참일 가능성이 있다면, 무한루프를 방지하기 위해서는 코드블록 내에 `if`문으로 무한루프 탈출 조건을 만들고 `break`문으로 코드블록을 탈출해야 한다

```jsx
var num = 0; 

while ( 0 == false) {
	console.log(num); // → 0 1 2 3 4
	num++;
	
	if ( num === 5 ) {
		break; 
	}
}
```

위 `while`문 예제는 어떻게 실행되는 것일까?

```jsx
var num = 0; // num = 0 

while ( 0 == false ) { // true
	console.log(num); // 0 
	num++; // num = num + 1 => num = 0 + 1 => num = 1

while ( 0 == false ) { // true 
	console.log(num); // 1
	num++; // num = num + 1 => num = 1 + 1 => num = 2

while ( 0 == false ) { // true 
	console.log(num); // 2
	num++; // num = num + 1 => num = 2 + 1 => num = 3

while ( 0 == false ) { // true
	console.log(num); // 3
	num++; // num = num + 1 => num = 3 + 1 => num = 4 

while ( 0 == false ) { // true
	console.log(num); // 4
	num++; // num = num + 1 => num = 4 + 1 => num = 5 

// num = 5이기 때문에 if문 발동
	if ( num === 5 ) { // true
		break; // console.log(num), num++ 실행 없이 while문 탈출
	}
} 
```

### 2-3 do…while문

`do…while`문은 코드블록을 먼저 실행하고 조건식을 평가한다. 즉, 코드블록은 조건식의 평가 여부를 떠나 최소 한 번 이상은 무조건 실행된다

```jsx
var num = 0; 

do { 
	console.log(num); // → 0 1 2
	num++; 
} while ( num < 3 ); 
```

위 `do…while`문 예제를 쪼개서 보자

```jsx
var num = 0; // num = 0

do {
	console.log(num); // 0
	num++; // num = num + 1 => num = 0 + 1 => num = 1
} while ( num < 3); // 1 < 3 => true

	{
	console.log(num); // 1 
	num++; // num = num + 1 => num = 1 + 1 => num = 2
} while ( num < 3 ); // 2 < 3 => true

	{
	console.log(num); // 2 
	num++; // num = num + 1 => num = 2 + 1 => num = 3
} while ( num < 3); // 3 < 3 => false. do...while문 실행 멈춤
```

만약 조건식이 `do…while`문 시작부터 `false`라면?

```jsx
var num = 1; 

do {
	console.log(num); // → 1
	num++; // num = num + 1 => num = 1 + 1 => num = 2 
} while ( num < 0 ); // false. do...while문 실행 멈춤

console.log(num); // → 2
```

<br>

## 3 반복문과 switch문의 제어

반복문(`for`, `for…in`, `for…of`, `while`, `do…while`), `switch`문에서 조건에 따라 반복 실행되는 코드블록 루프(Loop)로부터 코드의 실행 흐름을 다른 곳으로 변경(탈출)하기 위해서는 제어를 위한 수단이 필요하다

### 3-1 break문

`break`문은 레이블(Label) 문, 반복문, `switch`문의 코드블록을 탈출하게 한다

```jsx
// 반복문에서 if문과 더불어 코드블록을 탈출하게 하는 break문
var num = 0; 

while ( 0 == false) {
	console.log(num); // → 0 1 2 3 4
	num++;
	
	if ( num === 5 ) {
		break; 
	}
}
// switch문에서 폴스루를 방지하기 위한 break문
var user = 'Jace';

switch (user) {
	case 'Ju Hyung': user = 'Ju Hyung Nam'; 
		break;
	case 'Jace': user = 'Jace Nam'; 
		break;
	default: console.log('일치하는 사용자가 없습니다');
}

console.log(user); // → Jace Nam
```

레이블 문, 반복문, `switch`문의 코드블록 외에 `break`문을 사용하면 `SyntaxError`가 발생한다

```jsx
if ( true ) {
	break; // → Uncaught SyntaxError: Illegal break statement
}
```

### 3-2 레이블(Label) 문

레이블 문이란 식별자가 붙은 [블록문]()을 말한다. 레이블 이름은 예약어가 아닌 이상 임의로 이름을 지정해서 식별자로 사용이 가능하다

```jsx
var userName = 'Jace';
var userAge = 30;

userInfo: {
	console.log(userName); // → Jace
	break userInfo; 
	console.log(userAge); 
}
```

레이블 문을 탈출하려면 `break`문에 레이블 식별자(`userInfo`)를 지정해야한다

그럼 레이블 문은 왜 사용하는 것일까? 중첩된 `for`문의 외부로 탈출할 때 유용하다

```jsx
outer: 
	for ( var i = 0; i < 3; i++) {
		for ( var j = 0; j < 3; j++) {
			if ( i + j === 3 ) {
				break outer; 
			}
			console.log(`(${i}, ${j})`); // → (0,0) (0,1) (0,2) (1,0) (1,1)
		}
	}
```

(명확한 해답을 찾을 수 없어 실제 코드 사례들을 직접 쳐보거나 보게되면 다시 보충할 예정) 단순히 추측해보자면… 위 예제를 포함해 여러 겹으로 중첩된 `for`문에서 가장 외부의 `for`문까지 한번에 탈출할 때 용이하기 때문이라 판단된다. 레이블 문 없이 중첩 `for`문에서 탈출할 시 가독성이 더 많이 저하될 수도 있다

### 3-3 continue문

`continue`문은 반복문 `for`문의 코드블록 실행을 현 지점에서 중단하고 `for`문의 증감식으로 실행 흐름을 이동시킨다. `break`문처럼 반복문을 탈출하지 않는다

```jsx
for ( var num = 0; num < 10; num++) {
	 if ( num === 4 ) { 
		continue; 
		var num = 100; 
	}
	console.log(num); // → 1 2 3 5 6 7 8 9
}

// 위 for반복문, continue문 예제와 동일한 코드다
for ( var num = 0; num < 10; num++) {
	if ( num !== 4 ) {
		console.log(num); // → 0 1 2 3 5 6 7 8 9
	}
}
```

변수 `num`의 값이 `4`인 경우 현 지점에서 실행을 일시 중단하고 반복문의 증감식으로 돌아간다. 변수 선언 및 할당문 `var num = 100;`은 `continue`문이 실행되었을 때 실행되지 않는다

그렇다면 `while`문에서 `continue`문이 실행되면 어떻게 동작할까:

```jsx
var a = 0; 
var b = 0;

while ( a < 5 ) {
	a++; 
	
	if ( a === 3 ) {
		continue; 
	} 
	
	b += a);
}

console.log(b); // → 12
```

`for`문과는 달리, `while`문에서 `continue`문이 실행되면 증감식이 아닌 `while`문의 조건식으로 실행 흐름을 이동시킨다. 풀어서 살펴보자:

```jsx
var a = 0; 
var b = 0; 

// 1회차 순회
while ( a < 5 ) { // a === 0이므로 조건식은 참이다 
	a++; // a = a + 1 => a = 0 + 1 => a = 1

	if ( a === 3) { // a === 1이므로 조건식은 거짓이다
		continue; // continue문은 실행되지 않는다
	}
	
	b += a; // b = b + a => b = 0 + 1 => b = 1
}

// 2회차 순회
while ( a < 5 ) { // a === 1이므로 조건식은 참이다 
	a++; // a = a + 1 => a = 1 + 1 => a = 2

	if ( a === 3) { // a === 2이므로 조건식은 거짓이다
		continue; // continue문은 실행되지 않는다
	}
	
	b += a; // b = b + a => b = 1 + 2 => b = 3
}

// 3회차 순회
while ( a < 5 ) { // a === 2이므로 조건식은 참이다 
	a++; // a = a + 1 => a = 2 + 1 => a = 3

	if ( a === 3) { // a === 3이므로 조건식은 참이다
		continue; // continue문이 실행된다. 4회차 순회 때 while문의 조건식으로 돌아간다
	}
	
	b += a; // 할당 연산문은 실행되지 않는다
}
	
// 4회차 순회
while ( a < 5 ) { // a === 3이므로 조건식은 참이다
	a++; // a = a + 1 => a = 3 + 1 => a = 4

	if ( a === 3) { // a === 4이므로 조건식은 거짓이다
		continue; // continue문은 실행되지 않는다  
	}

	b += a; // b = b + a => b = 3 + 4 => b = 7
}

// 5회차 순회
while ( a < 5 ) { // a === 4이므로 조건식은 참이다
	a++; // a = a + 1 => a = 4 + 1 => a = 5

	if ( a === 3) { // a === 5이므로 조건식은 거짓이다
		continue; // continue문은 실행되지 않는다  
	}

	b += a; // b = b + a => b = 7 + 5 => b = 12
}

// 반복문 실행의 종료
console.log(b); // → 12
```

<br>

***

### 참고

- [모던 자바스크립트 Deep Dive](http://www.yes24.com/Product/Goods/92742567)
- [&& 논리 연산자로 if문 단축하기](https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-IF%EB%AC%B8-%EB%8B%A8%EC%B6%95-%EB%AC%B8%EB%B2%95-TIP)
- [IF문 반복하지말고! 이렇게 합시다!](https://youtu.be/TIbjzOEg7EI)
- [if, else 문 최소화하기](https://leffept.tistory.com/363)
- [조건문 더 스마트하게 쓰기](https://learnjs.vlpt.us/useful/05-smarter-conditions.html)
- [자바스크립트 isNaN() 함수로 NaN 체크하기](https://dasima.xyz/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-isnan-%ED%95%A8%EC%88%98-nan-%EC%B2%B4%ED%81%AC/)
- [자바스크립트 조건문과 switch](https://www.codingfactory.net/10442)
- [자바스크립트 조건문 사용하기](https://velog.io/@grinding_hannah/Switch-%EC%A1%B0%EA%B1%B4%EB%AC%B8-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)
- [JavaScript - 반복문(Loops)에 대해 알아보자](https://velog.io/@surim014/웹을-움직이는-근육-JavaScript란-무엇인가-part-5-Loops)
- [자바(+스크립트)의 레이블 구문 쁠랚쓰하게 활용하기](https://dev.to/composite/-59m4)
- [자바스크립트에서 switch(true) 패턴 사용하기](https://github.com/pming-kr/pming-content/discussions/101)