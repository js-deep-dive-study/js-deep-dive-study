# Chapter14. 전역 변수의 문제점

## 14.1 변수의 생명 주기

생성 → 선언

소멸 → ?

### 14.1.1 지역 변수의 생명 주기

**일반적인 경우**

함수 종료 → 변수 소멸

**소멸되지 않는 경우**

변수의 생명 주기는 메모리 공간을 확보한 시점부터 해제되어 반환되는 시점까지이다.
할당된 메모리 공간은 아무도 참조하지 않을 때 해제된다.
함수 스코프를 누군가가 참조하고 있으면 스코프는 소멸하지 않는다.
함수 내 변수도 소멸하지 않는다.
클로저에서는 이 스코프를 참조하기 때문에 메모리가 해제되지 않는다.

**호이스팅은 스코프 기준으로 동작한다.**

### 14.1.2 전역 변수의 생명 주기

**전역 객체**

브라우저 환경: window
node.js 환경: global
표준 빌트인 객체: Object, String, Number, Array…

전역 객체 window는 웹 페이지를 닫기 전까지 유효하다

## 14.2 전역 변수의 문제점

1. 어디서든 참조 가능 → 변경 가능성↑
2. 생명 주기가 김 → 변경 가능성↑
3. 스코프 체인의 끝 → 검색 속도↓
4. 네임스페이스 오염 → 겹칠 가능성↑

## 14.3 전역 변수 사용 억제 방법

1. 즉시 실행 함수(IIFE)
2. 네임스페이스 객체 - 별 차이 없어보임
3. **모듈 패턴**
    
    ```jsx
    const Counter = (function () {
    	let num = 0; // 반환되는 객체에 포함X => private 멤버
    	return {
    		increase() { // public 멤버
    			return ++num;
    		},
    		decrease() {
    			return --num;
    		}		
    	}
    }())
    ```
    
    - 클로저 기반
    - 클래스 모방
    - 즉시 실행함수
    - **캡슐화** 구현 : 프로퍼티와 메서드를 **하나로 묶는 것**.
    - 정보 은닉 기능
4. ES6 모듈
    - 모듈 스코프
    - script 태그 type=”module” 어트리뷰트
    - 모듈 번들러: Webpack
    - mjs
    

# Chapter15. let, const 키워드 & 블록 레벨 스코프

## 15.1 var의 문제점

1. 변수 중복 선언
    
    ```jsx
    var x = 1;
    var x = 100;
    console.log(x); // 100;
    ```
    
    재할당하는 것처럼 동작한다.
    
    ```jsx
    var y = 2;
    var y;
    console.log(y); // 2
    ```
    
    할당문이 없는 선언문은 무시된다.
    
    **중복 선언 ⇒ 변수가 변경됨**
    
2. 함수 레벨 스코프
    
    코드 블록 안에서 선언해도 전역 변수가 됨.
    
    전역 변수로 인식하기 쉽지 않을 듯.
    
3. 변수 호이스팅
    
    실행 흐름에 맞지 않기 때문에 가독성을 해침.
    
    변수 호이스팅에 의존해서 구현을 하게되면 의도치 않은 오류를 일으킬 수 있겠다.
    

## 15.2 let

> var의 단점을 보완하기 위해 ES6에서 도입됨
> 
1. 변수 중복 선언 불가
    
    SyntaxError 발생함
    
2. 블록 레벨 스코프
    
    코드 블록을 지역 스코프로 인정함.
    
3. 변수 호이스팅
    
    **Temperal Dead Zone : TDZ**
    
    스코프 시작점부터 초기화 시작점까지 참조할 수 없는 구간.
    
    즉, 변수 선언하고 사용해라.
    
    변수 호이스팅은 발생한다. 하지만 호이스팅이 발생하지 않는 것처럼 동작한다.
    
    ```jsx
    let foo = 1;
    {
    	console.log(foo); // ReferenceError
    	let foo = 2;
    }
    ```
    
4. var 키워드와는 다르게 전역 객체(window, global)의 프로퍼티가 되지 않음
    
    let 전역변수는 보이지 않는 개념적인 블록 내에 존재하게 된다.
    
    전역 렉시컬 환경(물리적으로 존재)의 선언적 환경 레코드
    

## 15.3 const

> 상수 선언을 위해 사용함
> 
1. 선언과 동시에 초기화해야 함.
    
    ```jsx
    const foo; // SyntaxError
    ```
    

1. 블록 레벨 스코프
2. 호이스팅 발생 안 하는 것처럼 동작
3. 재할당 금지(TypeError)
    
    상수 선언에 사용됨(**상수 = 재할당이 금지된 변수**)
    
    원시값은 변경할 수 없음
    
4. 객체
    
    재할당이 금지일 뿐, 불변은 아님.
    
    프로퍼티 변경 가능.
    

## 15.4 var vs let vs const

- ES6 에서는 let, const 사용
- 재할당이 필요한 경우 let
- 변경 발생하지 않거나 읽기 전용 값은 const

# Chapter16. 프로퍼티 어트리뷰트

### 16.3.2 접근자 프로퍼티

getter / setter 함수를 선언할 때 get, set 프로퍼티를 사용하면 메서드 호출이 아니라 프로퍼티로 접근이 가능함.

```jsx
const person = {
	firstName: 'Jello',
	lastName: 'Song',
	get fullName() {
		return `${this.firstName} ${this.lastName}`;
	},
	set fullName(name) {
		[this.firstName, this.lastName] = name.split(' ');
	}
}

console.log(person.fullName); // Jello Song
person.fullName = 'Hyeonjin Song';
console.log(person.fullName); // Hyeonjin Song

```

읽기 전용 느낌으로 안정성, 보안성 유지

프로토타입(prototype)

- 상위 객체 역할을 한다. 하위 객체는 프로토 타입의 프로퍼티와 메서드를 사용할 수 있다.
- 프로토 타입 체인
    - 단방향 링크드 리스트 형태로 연결된 **상속 구조**
    - 프로퍼티, 메서드 탐색에 사용됨

## 16.5 객체 변경 방지

1. 객체 확장 금지
    
    `Object.prevetExtension()`
    
    프로퍼티 **추가 금지**
    
2. 객체 밀봉
    
    `Object.seal()`
    
    프로퍼티 추가, 삭제, 재정의 금지
    
    **읽기, 쓰기만 가능**
    
3. 객체 동결
    
    `Object.freeze()`
    
    프로퍼티 추가, 삭제, 재정의 금지, 값 갱신 금지
    
    읽기만 가능
    
4. 불변 객체
    
    중첩 객체까지 동결하기 위해서는 재귀적으로 Object.freeze() 메서드를 호출해야함
    

```jsx
1. 객체 확장 금지
const person = {name: 'Lee'};
Object.preventExtension(person);
console.log(Object.isExtensible(person)); // false;

// 프로퍼티 정의로도 추가 불가
Object.defineProperty(person, age, {value: 20}); // TypeError

2. 객체 밀봉
```