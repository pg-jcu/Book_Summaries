# 정리

## 목차  
- [식별자](#식별자)  
- [값](#값)  
- [리터럴](#리터럴)  
- [표현식](#표현식)  
- [문](#문)  
- [객체](#객체)  
- [함수](#함수)  
- [스코프](#스코프)  
- [var, let, const](#var-let-const)  
- [프로퍼티 어트리뷰트](#프로퍼티-어트리뷰트)  
- [프로토타입](#프로토타입)  
- [this](#this)  
- [실행 컨텍스트](#실행-컨텍스트)  
- [클로저](#클로저)
- [클래스](#클래스)  
- [배열](#배열)  

## 식별자
식별자<sup>identifier</sup>는 어떤 값을 구별해서 식별할 수 있는 고유한 이름을 말한다.  
식별자는 값이 아니라 메모리 주소를 기억하고 있다.  

## 값
값<sup>value</sup>은 식(표현식<sup>expression</sup>)이 평가<sup>evaluate</sup>되어 생성된 결과를 말한다.
값을 사용할 수 있는 곳: 변수 할당문, 객체의 프로퍼티 값, 배열의 요소, 함수 호출의 인수, 함수 반환문  

```javascript  
1 + 2; // 3  
```

## 리터럴
리터럴<sup>literal</sup>은 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용해 값을 생성하는 표기법<sup>notation</sup>을 말한다.

```javascript 
3  // 숫자 리터럴
```

|리터럴|예시|
|-----|-----|
|정수|100|
|부동소수점|10.5|
|2진수|0b01000001|
|8진수|0o101|
|16진수|0x41|
|문자열|'Hello'<br>"World"|
|불리언|true<br>false|
|null|null|
|undefined|undefined|
|객체|{ name: 'Jeong', address: 'None' }|
|배열|[ 1, 2, 3 ]|
|함수|function() {}|
|정규 표현식|/[A-Z]+/g|

## 표현식
표현식<sup>expression</sup>은 값으로 평가될 수 있는 문<sup>statement</sup>이다.  
즉, 표현식이 평가되면 새로운 값을 생성하거나 기존값을 참조한다.  
리터럴, 식별자(변수, 함수 등의 이름), 연산자, 함수 호출 등의 조합으로 이뤄질 수 있다.  
표현식과 표현식이 평가된 값은 동등한 관계, 즉 동치<sup>equivalent</sup>다.

```javascript
// 리터럴 표현식
10
'Hello'

// 식별자 표현식(이미 선언되어있다고 가정)
sum
person.name
arr[1]

// 연산자 표현식
10 + 20
sum = 10
sum !== 10

// 함수/메서드 호출 표현식(이미 선언되어있다고 가정)
square()
person.getName()
```

## 문
문<sup>statement</sup>은 프로그램을 구성하는 기본 단위이자 최소 실행 단위다.  
문은 여러 토큰으로 구성된다.
- 토큰<sup>token</sup>이란 문법적인 의미를 가지며, 문법적으로 더 이상 나눌 수 없는 코드의 기본 요소를 의미한다.

```javascript
// 변수 선언문
let x;

// 할당문
x = 5;

// 함수 선언문
function func () {}

// 조건문
if (x > 1) { console.log(x); }

// 반복문
for (let i = 0; i < 2; i++) { console.log(i); }
```

> *표현식인 문과 표현식이 아닌 문을 구별하는 가장 간단하고 명료한 방법은 변수에 할당해 보는 것이다.*

## 객체  
자바스크립트를 이루고 있는 거의 *모든 것*이 객체다.  
객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성된다.  
객체 타입<sup>object/reference type</sup>은 다양한 타입의 값을 하나의 단위로 구성한 복합적인 자료구조<sup>data structure</sup>다.  
객체는 상태 데이터와 동작을 하나의 논리적인 단위로 묶은 복합적인 자료구조라고 할 수 있다.  
원시 타입의 값, 즉 원시 값은 변경 불가능한 값<sup>immutable value</sup>이지만 객체 타입의 값, 즉 객체는 변경 가능한 값<sup>mutable value</sup>이다.  

```javascript
var counter = {
  num: 0,                 // 프로퍼티: 객체의 상태를 나타내는 값(data)
  increase: function () { // 메서드: 프로퍼티(상태 데이터)를 참조하고 조작할 수 있는 동작(behavior)
    this.num++;
  }
};
```
> *객체 리터럴의 중괄호는 코드 블록을 의미하지 않기 때문에 세미콜론을 붙인다.*  
> *프로퍼티 키는 식별자 네이밍 규칙을 따르지 않는 이름에는 반드시 따옴표를 사용해야 한다.*  

### 전역 객체<sup>global object</sup>
코드가 실행되기 이전 단계에 자바스크립트 엔진에 의해 어떤 객체보다도 먼저 생성되는 특수한 객체다.  
계층적 구조상 어떤 객체에도 속하지 않은 모든 빌트인 객체(표준 빌트인 객체와 호스트 객체)의 최상위 객체다.  
전역 객체가 최상위 객체라는 것은 프로토타입 상속 관계상에서 최상위 객체라는 의미가 아니다.  
전역 객체 자신은 어떤 객체의 프로퍼티도 아니며 객체의 계층적 구조상 표준 빌트인 객체와 호스트 객체를 프로퍼티로 소유한다는 것을 말한다.  

### 일급 객체
1. 무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성이 가능하다.
2. 변수나 자료구조(객체, 배열 등)에 저장할 수 있다.
3. 함수의 매개변수에 전달할 수 있다.
4. 함수의 반환값으로 사용할 수 있다.

---
표준 빌트인 객체<sup>standard built-in objects/native objects/global objects</sup>  
호스트 객체<sup>host objects</sup>  
사용자 정의 객체<sup>user-defined objects</sup>  
래퍼 객체<sup>wrapper object</sup>  

## 함수
함수는 일련의 과정을 문<sup>statement</sup>으로 구현하고 코드 블록으로 감싸서 하나의 실행 단위로 정의한 것이다.  
함수 내부로 입력을 전달받는 변수를 **매개변수<sup>parameter</sup>(인자)**, 입력을 **인수<sup>argument</sup>**, 출력을 **반환값<sup>return value</sup>** 이라 한다.  
함수 이름은 함수 몸체 내부에서만 유효한 식별자이다.  
함수는 함수 이름으로 호출하는 것이 아니라 함수 객체를 가리키는 식별자로 호출한다.  
함수는 함수를 가리키는 식별자와 한 쌍의 소괄호인 함수 호출 연산자로 호출한다.  
함수는 매개변수와 인수의 개수가 일치하는지 확인하지 않고 매개변수의 타입을 사전에 지정할 수 없다.  
일반 객체는 호출할 수 없지만 함수는 호출할 수 있다.  
함수 객체는 callable이면서 constructor이거나 callable이면서 non-constructor다.  
함수가 일급 객체라는 것은 함수를 객체와 동일하게 사용할 수 있다는 의미다.  
함수 객체의 데이터 프로퍼티로 arguments, caller, length, name, prototype이 있다.  
함수는 자신의 내부 슬록 [[Environment]]에 자신이 정의된 환경, 즉 상위 스코프의 참조를 저장한다.  
매개변수 기본값은 매개변수에 인수를 전달하지 않은 경우와 undefined를 전달한 경우에만 유효하다.  
매개변수 기본값은 length 프로퍼티와 arguments 객체에 아무런 영향을 주지 않는다.  

|함수 정의 방식|예시|
|-----|-----|
|함수 선언문|function add(x, y) {<br>&nbsp;&nbsp;return x + y;<br>}|
|함수 표현식|var add = function (x, y) {<br>&nbsp;&nbsp;return x + y;<br>};|
|Function 생성자 함수|var add = new Function('x', 'y', 'return x + y');|
|화살표 함수|var add = (x, y) => x + y;|
|메서드 축약 표현|const obj = {<br>&nbsp;&nbsp;foo() {}<br>};|  
> *함수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 함수 호이스팅<sup>function hoisting</sup>이라 한다.*  
> *함수 표현식으로 함수를 정의하면 함수 호이스팅이 발생하는 것이 아니라 변수 호이스팅이 발생한다.*  

**콜백 함수<sup>callback function</sup>**: 함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수  
**고차 함수<sup>Higher-Order Function, HOF</sup>**: 매개변수를 통해 함수의 외부에서 콜백 함수를 전달받은 함수  
**생성자 함수<sup>constructor function</sup>**: new 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수  

### 빌트인 전역 함수
**eval**: 자바스크립트 코드를 나타내는 문자열을 인수로 전달받는다.  
**isFinite**: 전달받은 인수가 정상적인 유한수인지 검사한다.  
**isNaN**: 전달받은 인수가 NaN인지 검사한다.  
**parseFloat**: 전달받은 문자열 인수를 부동 소수점 숫자로 해석<sup>parsing</sup>하여 반환한다.  
**parseInt**: 전달받은 문자열 인수를 정수로 해석하여 반환한다.  
**encodeURI**: 완전한 URI<sup>Uniform Resource Identifier</sup>를 문자열로 전달받아 이스케이프 처리를 위해 인코딩한다.  
**decodeURI**: 인코딩된 URI를 인수로 전달받아 이스케이프 처리 이전으로 디코딩한다.  
**encodeURIComponent**: URI 구성 요소를 인수로 전달받아 인코딩한다.  
**decodeURIComponent**: 매개변수로 전달된 URI 구성 요소를 디코딩한다.  

### prototype 프로퍼티
prototype 프로퍼티는 생성자 함수로 호출할 수 있는 함수 객체, 즉 constructor만이 소유하는 프로퍼티다.  
prototype 프로퍼티는 함수가 객체를 생성하는 생성자 함수로 호출될 때 생성자 함수가 생성할 인스턴스의 프로토타입 객체를 가리킨다.  

### 즉시 실행 함수<sup>IIFE, Immediately Invoked Function Expression</sup>  
함수 정의와 동시에 즉시 호출되는 함수를 말하고 단 한 번만 호출되며 다시 호출할 수 없다.  
```javascript
const counter = (function () {
  let counter = 0;
  
  return function (predicate) {
    counter = predicate(counter)
    return counter;
  };
}());
```

**ES6에서는 함수를 사용 목적에 따라 세 가지 종류로 명확히 구분했다.**
|ES6 함수의 구분|constructor|prototype|super|arguments|
|---|:---:|:---:|:---:|:---:|
|일반 함수|Ο|Ο|Χ|Ο|
|메서드|Χ|Χ|Ο|Ο|
|화살표 함수|Χ|Χ|Χ|Χ|
> *ES6 사양에서 메서드는 메서드 축약 표현으로 정의된 함수만을 의미한다.*  
> *ES6 메서드는 자신을 바인딩한 객체를 가리키는 내부 슬롯 [[HomeObject]]를 갖는다.*

### 화살표 함수
화살표 함수는 선언문으로 정의할 수 없고 함수 표현식으로 정의해야 한다.  
매개변수가 한 개인 경우 소괄호를 생략할 수 있다.  
함수 몸체가 하나의 문으로 구성된다면 함수 몸체를 감싸는 중괄호를 생략할 수 있고 이때 함수 몸체 내부의 문이 값으로 평가될 수 있는 표현식인 문이라면 암묵적으로 반환된다.  
객체 리터럴을 반환하는 경우 객체 리터럴을 소괄호로 감싸 주어야 한다.  
화살표 함수도 즉시 실행 함수로 사용할 수 있다.  

**화살표 함수와 일반 함수의 차이**
1. 화살표 함수는 인스턴스를 생성할 수 없는 non-constructor다.
2. 중복된 매개변수 이름을 선언할 수 없다.
3. 화살표 함수는 함수 자체의 this, arguments, super, new.target 바인딩을 갖지 않는다.  

### Rest 파라미터
함수에 전달된 인수들의 목록을 배열로 전달받는다.  
Rest 파라미터는 반드시 마지막 파라미터이어야 한다.  
Rest 파라미터는 단 하나만 선언할 수 있다.  
Rest 파라미터에는 기본값을 지정할 수 없다.  

---
중첩 함수<sup>nested function</sup>또는 내부 함수<sup>inner function</sup>  
순수 함수<sup>pure function</sup>와 비순수 함수<sup>impure function</sup>  

## 스코프
모든 식별자는 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효 범위가 결정된다.  
전역 스코프<sup>global scope</sup>와 지역 스코프<sup>local scope</sup>이 있다.  
호이스팅은 스코프를 단위로 동작한다.  
스코프의 실체는 실행 컨텍스트의 렉시컬 환경이다.  
외부 렉시컬 환경에 대한 참조를 통해 상위 렉시컬 환경과 연결된 것을 스코프 체인이라고 한다.  

**스코프 체인<sup>scope chain</sup>**: 실행 컨텍스트의 렉시컬 환경을 단방향으로 연결<sup>chaining</sup>한 것이다.  
**함수 레벨 스코프<sup>function level scope</sup>**: var키워드로 선언된 변수는 오로지 함수의 코드 블록만을 지역 스코프로 인정된다.  
**렉시컬 스코프<sup>lexical scope</sup>**: 렉시컬 환경의 "외부 렉시컬 환경에 대한 참조"에 저장할 참조값, 즉 상위 스코프에 대한 참조는 함수 정의가 평가되는 시점에 함수가 정의된 환경(위치)에 의해 결정된다.  

## var, let, const  
### var 키워드
변수 중복 선언이 가능하고 중복 선언된 초기화문이 있는 변수 선언문은 자바스크립트 엔진에 의해 var 키워드가 없는 것처럼 동작한다.  
함수의 코드 블록만을 지역 스코프로 인정한다.  
변수 호이스팅에 의해 변수 선언문이 스코프의 선두로 끌어 올려진 것처럼 동작한다.  
선언 단계와 초기화 단계가 동시에 진행된다.  

### let 키워드
변수를 중복 선언하면 문법 에러<sup>SyntaxError</sup>가 발생한다.  
모든 코드 블록을 지역 스코프로 인정하는 블록 레벨 스코프<sup>block-level scope</sup>를 따른다.  
선언 단계와 초기화 단계가 분리되어 진행된다. 초기화 단계는 변수 선언문에 도달했을 때 실행된다.  
let 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아니다.  
선언적 환경 레코드<sup>Declarative Environment Record</sup>에서 관리한다.  

### const 키워드
상수<sup>constant</sup>를 선언하기 위해 사용한다. *예) const TAX_RATE = 0.1;*  
const 키워드로 선언한 변수는 반드시 선언과 동시에 초기화해야 하고 재할당이 금지된다.  
원시 값을 할당한 경우 할당된 값을 변경할 수 있는 방법은 없다.  
const 키워드로 선언된 변수에 객체를 할당한 경우 값을 변경할 수 있다.  
선언적 환경 레코드<sup>Declarative Environment Record</sup>에서 관리한다.  

## 프로퍼티 어트리뷰트
내부 슬롯<sup>internal slot</sup>과 내부 메서드<sup>internal method</sup>는 자바스크립트 엔진의 구현 알고리즘을 설명하기 위해 ECMAScript 사양에서 사용하는 의사 프로퍼티<sup>pseudo property</sup>와 의사 메서드<sup>pseudo method</sup>다.  
자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다.  
프로퍼티의 상태란 프로퍼티의 값<sup>value</sup>, 값의 갱신 가능 여부<sup>writable</sup>, 열거 가능 여부<sup>enumerable</sup>, 재정의 가능 여부<sup>configurable</sup>를 말한다.  

**데이터 프로퍼티<sup>data property</sup>**: 키와 값으로 구성된 일반적인 프로퍼티다.  
```javascript
const person = {
  name: 'Lee'
};

console.log(Object.getOwnPropertyDescriptor(person, 'name'));
// {value: "Lee", writable: true, enumerable: true, configurable: true}
```

**접근자 프로퍼티<sup>accessor property</sup>**: 자체적으로는 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수로 구성된 프로퍼티다.  
- __proto__는 Object.prototype 객체의 접근자 프로퍼티다.  

```javascript
const person = {
  firstName: 'Ungmo',
  lastName: 'Lee',
  
  // 접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 읽을 때 호출되는 접근자 함수
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },
  
  // 접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 저장할 때 호출되는 접근자 함수
  set fullName(name) {
    [this.firstName, this.lastName] = name.split(' ');
  }
};
```

**프로퍼티 정의**: 새로운 프로퍼티를 추가하면서 프로퍼티 어트리뷰트를 명시적으로 정의하거나, 기존 프로퍼티의 프로퍼티 어트리뷰트를 재저의하는 것을 말한다.  
```javascript
const person = {};

Object.defineProperty(person, 'firstName', {
  value: 'Ungmo',
  writable: true,
  enumerable: true,
  configurable: true
});

Object.defineProperty(person, 'lastName', {
  value: 'Lee'
});

Object.defineProperty(person, 'fullName' {
  get() {
    return `${this.firstName} ${this.lastName}`;
  },
  set(name) {
    [this.firstName, this.lastName] = name.split(' ');
  },
  enumerable: true,
  configurable: true
});
```

프로퍼티 디스크립터 객체에서 생략된 어트리뷰트는 다음과 같이 기본값이 적용된다.  
|프로퍼티 디스크립터 객체의 프로퍼티|대응하는 프로퍼티 어트리뷰트|생략할 때의 기본값|
|---|---|---|
|value|[[Value]]|undefined|
|get|[[Get]]|undefined|
|set|[[Set]]|undefined|
|writable|[[Writable]]|false|
|enumerable|[[Enumerable]]|false|
|configurable|[[Configurable]]|false|

자바스크립트는 객체의 변경을 방지하는 다양한 메서드(얕은 변경 방지<sup>shallow only</sup>)를 제공한다.
|구분|메서드|추가|삭제|값 읽기|값 쓰기|어트리뷰트 재정의|
|---|---|:---:|:---:|:---:|:---:|:---:|
|객체 확장 금지|Object.preventExtensions|Χ|Ο|Ο|Ο|Ο|
|객체 밀봉|Object.seal|Χ|Χ|Ο|Ο|Χ|
|객체 동결|Object.freeze|Χ|Χ|Ο|Χ|Χ|

**in 연산자**: 객체 내에 특정 프로퍼티가 존재하는지 여부를 확인한다.(확인 대상 객체가 상속받은 모든 프로토타입의 프로퍼티를 확인)  
**Object.prototype.hasOwnProperty 메서드**: 전달받은 프로퍼티 키가 객체 고유의 프로퍼티 키인 경우에만 true를 반환한다.  
**for...in 문**: 객체의 프로토타입 체인 상에 존재하는 모든 프로토타입의 프로퍼티 중에서 프로퍼티 어트리뷰트 [[Enumerable]]의 값이 true인 프로퍼티를 순회하며 열거한다.   
**Object.keys/values/entries 메서드**: keys 메서드는 객체 자신의 열거 가능한 프로퍼티 키를, values 메서드는 프로퍼티 값을, entries 메서드는 프로퍼티 키와 값의 쌍의 배열을 배열로 반환한다.  

### 빌트인 전역 프로퍼티
**Infinity**: 무한대를 나타내는 숫자값 Infinity를 갖는다.  
**NaN**: 숫자가 아님(Not-a-Number)을 나타내는 숫자값 NaN을 갖는다.  
**undefined**: 원시 타입 undefined를 값으로 갖는다.  

## 프로토타입
자바스크립트는 프로토타입<sup>prototype</sup>을 기반으로 상속을 구현한다.

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function () {
  console.log(`Hi! My name is ${this.name}`);
};

Person.staticProp = 'static prop';

Person.staticMethod = function () {
  console.log('staticMethod');
};
```
모든 객체가 가지고 있는 \_\_proto__ 접근자 프로퍼티와 함수 객체만 가지고 있는 prototype 프로퍼티는 결국 동일한 프로토타입을 가리킨다.  
|구분|소유|값|사용 주체|사용 목적|
|---|---|---|---|---|
|\_\_proto__ <br>접근자 프로퍼티|모든 객체|프로토타입의 참조|모든 객체|객체 자신의 프로토타입에 접근 또는 교체하기<br> 위해 사용|
|prototype <br>프로퍼티|constructor|프로토타입의 참조|생성자 함수|생성자 함수가 자신의 생성할 객체(인스턴스)의<br> 프로토타입을 할당하기 위해 사용|

프로토타입과 생성자 함수는 단독으로 존재할 수 없고 언제나 쌍<sup>pair</sup>으로 존재한다.  
프로토타입은 생성자 함수가 생성되는 시점에 더불어 생성된다.  
생성자 함수로서 호출할 수 있는 함수, 즉 constructor는 함수 정의가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성된다.  
사용자 정의 생성자 함수와 더불어 생성된 프로토타입은 오직 constructor 프로퍼티만을 갖는 객체다.  
프로토타입도 객체이고 모든 객체는 프로토타입을 가지므로 프로토타입도 자신의 프로토타입을 갖는다.  
하위 객체를 통해 프로토타입의 프로퍼티를 변경 또는 삭제하는 것은 불가능하다.  

**프로토타입 체인**: 객체의 프로퍼티(메서드 포함)에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티가 없다면 [[Prototype]] 내부 슬롯의 참조를 따라 자신의 부모 역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색한다.  

객체 **instanceof** 생성자 함수
- 우변의 생성자 함수의 prototype에 바인딩된 객체가 좌변의 객체의 프로토타입 체인 상에 존재하면 true로 평가된다.  
- 생성자 함수의 prototype에 바인딩된 객체가 프로토타입 체인 상에 존재하는지 확인한다.  

**정적<sup>static</sup>프로퍼티/메서드**: 생성자 함수로 인스턴스를 생성하지 않아도 참조/호출할 수 있는 프로퍼티/메서드를 말한다.  

## this
this는 객체 자신의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수<sup>self-referenceing variable</sup>다.  

|함수 호출 방식|this가 가리키는 값(this 바인딩)|
|---|---|
|일반 함수로서 호출|전역 객체|
|메서드로서 호출|메서드를 호출한 객체(마침표 앞의 객체)|
|생성자 함수로서 호출|생성자 함수가 (미래에) 생성할 인스턴스|  
> *this 바인딩은 함수 호출 시점에 결정된다.*  
> *strict mode가 적용된 일반 함수 내부의 this에는 undefined가 바인딩된다.*  
> *메서드 내부의 this는 메서드를 소유한 객체가 아닌 메서드를 호출한 객체에 바인딩된다.*  

### Function.prototype.apply/call/bind 메서드
apply와 call 메서드의 본질적인 기능은 함수를 호출하는 것이다.  
bind 메서드는 apply와 call 메서드와 달리 함수를 호출하지 않고 this로 사용할 객체만 전달한다.  

**new.target**: constructor인 모든 함수 내부에 암묵적인 지역 변수와 같이 사용되며 메타 프로퍼티라고 부른다.  
this 바인딩은 전역 환경 레코드와 함수 환경 레코드에만 존재한다.  
strict mode에서 일반 함수로서 호출된 모든 함수 내부의 this에는 전역 객체가 아니라 undefined가 바인딩된다.  
클래스 필드에 할당한 화살표 함수 내부에서 참조한 this는 constructor 내부의 this 바인딩과 같다.  

## 실행 컨텍스트
실행 컨텍스트<sup>execution context</sup>는 자바스크립트의 동작 원리를 담고 있는 핵심 개념이다.  
소스코드를 실행하는 데 필요한 환경을 제공하고 코드의 실행 결과를 실제로 관리하는 영역이다.  
식별자(변수, 함수, 클래스 등의 이름)를 등록하고 관리하는 스코프와 코드 실행 순서 관리를 구현한 내부 메커니즘으로, 모든 코드는 실행 컨텍스트를 통해 실행되고 관리된다.  
식별자와 스코프는 실행 컨텍스트의 렉시컬 환경으로 관리하고 코드 실행 순서는 실행 컨텍스트 스택으로 관리한다.  
실행 컨텍스트 스택의 최상위에 존재하는 실행 컨텍스트는 언제나 현재 실행 중인 코드의 실행 컨텍스트다.  
LexicalEnvironment 컴포넌트와 VariableEnvironment 컴포넌트로 구성된다.  

|소스코드의 타입|설명|
|---|---|
|전역 코드|전역에 존재하는 소스코드를 말한다. 전역에 정의된 함수, 클래스 등의 내부 코드는 포함되지 않는다.|
|함수 코드|함수 내부에 존재하는 소스코드를 말한다. 함수 내부에 중첩된 함수, 클래스 등의 내부 코드는 포함되지 않는다.|
|eval 코드|빌트인 전역 함수인 eval함수에 인수로 전달되어 실행되는 소스코드를 말한다.|
|모듈 코드|모듈 내부에 존재하는 소스코드를 말한다. 모듈 내부의 함수, 클래스 등의 내부 코드는 포함되지 않는다.|
> *소스코드의 타입에 따라 실행 컨텍스트를 생성하는 과정과 관리 내용이 다르다.*  

### 소스코드의 평가와 실행
자바스크립트 엔진은 소스코드를 2개의 과정, 즉 "소스코드의 평가"와 "소스코드의 실행" 과정으로 나누어 처리한다.  
1. 소스코드 평가 과정에서는 실행 컨텍스트를 생성하고 변수, 함수 등의 선언문만 먼저 실행하여 생성된 변수나 함수 식별자를 키로 실행 컨텍스트가 관리하는 스코프(렉시컬 환경의 환경 레코드)에 등록한다.  
2. 소스코드 평가 과정이 끝나면 비로소 선언문을 제외한 소스코드가 순차적으로 실행되기 시작한다. 즉, 런타임이 시작된다. 이때 소스코드 실행에 필요한 정보, 즉 변수나 함수의 참조를 실행 컨텍스트가 관리하는 스코프에서 검색해서 취득한다. 그리고 변수 값의 변경 등 소스코드의 실행 결과는 다시 실행 컨텍스트가 관리하는 스코프에 등록된다.  

### 렉시컬 환경
렉시컬 환경<sup>Lexical Enviroment</sup>은 식별자와 식별자에 바인딩된 값, 그리고 상위 스코프에 대한 참조를 기록하는 자료구조로 실행 컨텍스트를 구성하는 컴포넌트다.  
키와 값을 갖는 객체 형태의 스코프(전역, 함수, 블록 스코프)를 생성하여 식별자를 키로 등록하고 식별자에 바인딩된 값을 관리한다.  
렉시컬 환경은 실행 컨텍스트에 의해 참조되기는 하지만 독립적인 객체다.  
렉시컬 환경은 두 개의 컴포넌트로 구성된다.  
1. **환경 레코드<sup>Environment Record</sup>**  
   스코프에 포함된 식별자를 등록하고 등록된 식별자에 바인딩된 값을 관리하는 저장소다. 환경 레코드는 소스코드의 타입에 따라 관리하는 내용에 차이가 있다.  
2. **외부 렉시컬 환경에 대한 참조<sup>Outer Lexical Environment Reference</sup>**  
   외부 렉시컬 환경에 대한 참조는 상위 스코프를 가리킨다. 이때 상위 스코프란 외부 렉시컬 환경, 즉 해당 실행 컨텍스트를 생성한 소스코드를 포함하는 상위 코드의 렉시컬 환경을 말한다. 외부 렉    시컬 환경에 대한 참조를 통해 단방향 링크드 리스트인 스코프 체인을 구현한다.  

### 전역 코드 평가
1. 전역 실행 컨텍스트 생성  
2. 전역 렉시컬 환경 생성  
   1. 전역 환경 레코드 생성   
      1. 객체 환경 레코드 생성  
      2. 선언적 환경 레코드 생성  
   2. this 바인딩  
   3. 외부 렉시컬 환경에 대한 참조 결정  

### 함수 코드 평가
1. 함수 실행 컨텍스트 생성  
2. 함수 렉시컬 환경 생성  
   1. 함수 환경 레코드 생성  
   2. this 바인딩  
   3. 외부 렉시컬 환경에 대한 참조 결정  

![execution_context](https://user-images.githubusercontent.com/40534414/145710606-158dbe7b-be8b-4366-a390-8f89294bac23.png)

### 실행 컨텍스트와 블록 레벨 스코프  
let, const 키워드로 선언한 변수는 모든 코드 블록을 지역 스코프로 인정하는 블록 레벨 스코프를 따르기 때문에 선언적 환경 레코드를 갖는 렉시컬 환경을 새롭게 생성하여 기존의 전역 렉시컬 환경을 교체한다.  

### 식별자 결정
동일한 이름의 식별자가 다른 스코프에 여러 개 존재할 수도 있기 때문에 어느 스코프의 식별자를 참조하면 되는지 결정할 필요가 있다.  
식별자 결정을 위해 식별자를 검색할 때는 실행 중인 실행 컨텍스트에서 식별자를 검색하기 시작한다.  
선언된 식별자는 실행 컨텍스트의 렉시컬 환경의 환경 레코드에 등록되어 있다.  

## 클로저
외부 함수보다 중첩 함수가 더 오래 유지되는 경우 중첩 함수는 이미 생명 주기가 종료한 외부 함수의 변수를 참조할 수 있다.  
중첩 함수가 상위 스코프의 식별자를 참조하고 있고 중첩 함수가 외부 함수보다 더 오래 유지되는 경우에 한정하는 것이 일반적이다.  
"함수가 자유 변수에 대해 닫혀있다.", 쉽게 의역하면 "자유 변수에 묶여있는 함수"라고 할 수 있다.  
클로저는 상태가 의도치 않게 변경되지 않도록 안전하게 은닉<sup>information hiding</sup>하고 특정 함수에게만 상태 변경을 허용하여 상태를 안전하게 변경하고 유지하기 위해 사용한다.  

**자유 변수<sup>free variable</sup>**: 클로저에 의해 참조되는 상위 스코프의 변수  

## 클래스
클래스는 값으로 사용할 수 있는 일급 객체이다.  
클래스는 생성자 함수와 마찬가지로 프로토타입 기반의 객체 생성 메커니즘이다.  
클래스 몸체에서 정의할 수 있는 메서드는 constructor(생성자), 프로토타입 메서드, 정적 메서드의 세 가지가 있다.  
클래스의 constructor 메서드와 프로토타입의 constructor 프로퍼티는 직접적인 관련이 없다.  
서브클래스는 자신이 직접 인스턴스를 생성하지 않고 수퍼클래스에게 인스턴스를 생성을 위임한다.  
```javascript
class Person {
  // private 필드 정의
  #age = '';
  // static private 필드 정의
  static #tribe = 'human';
  
  constructor(name, age) {
    this.name = name;
    this.#age = age;
  }
  
  sayHi() {
    console.log(`Hi! My name is ${this.name}`);
  }
  
  static sayHello() {
    console.log('Hello!');
  }
}
```

**클래스와 생성자 함수의 차이**  
1. 클래스를 new 연산자 없이 호출하면 에러가 발생한다. 
2. 클래스는 상속을 지원하는 extends와 super 키워드를 제공한다.
3. 클래스는 호이스팅이 발생하지 않는 것처럼 동작한다.
4. 클래스 내의 모든 코드에는 암묵적으로 strict mode가 지정되어 실행되며 strict mode를 해제할 수 없다.
5. 클래스의 constructor, 프로토타입 메서드, 정적 메서드는 모두 프로퍼티 어트리뷰트 [[Enumerable]]의 값이 false다. 

**정적 메서드와 프로토타입 메서드의 차이**  
1. 정적 메서드와 프로토타입 메서드는 자신이 속해 있는 프로토타입 체인이 다르다.
2. 정적 메서드는 클래스로 호출하고 프로토타입 메서드는 인스턴스로 호출한다.
3. 정적 메서드는 인스턴스 프로퍼티를 참조할 수 없지만 프로토타입 메서드는 인스턴스 프로퍼티를 참조할 수 있다.  

**클래스에서 정의한 메서드의 특징**
1. function 키워드를 생략한 메서드 축약 표현을 사용한다. 
2. 객체 리터럴과는 다르게 클래스에 메서드를 정의할 때는 콤마가 필요 없다.
3. 암묵적으로 strict mode로 실행된다.
4. for...in 문이나 Object.keys 메서드 등으로 열거할 수 없다.
5. 내부 메서드 [[Construct]]를 갖지 않는 non-constructor다.  

**super 키워드**
- super를 호출하면 수퍼클래스의 constructor(super-constructor)를 호출한다.  
  - 서브클래스에서 constructor를 생략하지 않는 경우 서브클래스의 constructor에서 반드시 super를 호출해야한다.
  - 서브클래스의 constructor에서 super를 호출하기 전에는 this를 참조할 수 없다.
  - super는 반드시 서브클래스의 constructor에서만 호출한다.
- super를 참조하면 수퍼클래스의 메서드를 호출할 수 있다.
  - 서브클래스의 프로토타입 메서드 내에서 super.method는 수퍼클래스의 프로토타입 메서드 method를 가리킨다.
  - ES6의 메서드 축약 표현으로 정의된 함수만이 [[HomeObject]]를 갖는다는 것이다.  
  - 서브클래스의 정적 메서드 내에서 super.method는 수퍼클래스의 정적 메서드 method를 가리킨다.

## 배열
자바스크립트의 배열은 일반적인 배열의 동작을 흉내 낸 특수한 객체다.  
인덱스로 배열 요소에 접근하는 경우에는 일반적인 배열보다 느리다.  
특정 요소를 검색하거나 요소를 삽입 또는 삭제하는 경우에는 일반적인 배열보다 빠르다.  
배열은 요소를 최대 <img src="https://render.githubusercontent.com/render/math?math=2^{32} - 1">(4,294,967,295)개 가질 수 있다.  
배열에는 같은 타입의 요소를 연속적으로 위치시키는 것이 최선이다.  
정수 이외의 값을 인덱스처럼 사용하면 요소가 생성되는 것이 아니라 프로퍼티가 생성된다.  

**밀집 배열<sup>dense array</sup>**: 배열의 요소는 하나의 데이터 타입으로 통일되어 있으며 서로 연속적으로 인접해 있는 배열이다.  
**회소 배열<sup>sparse array</sup>**: 배열의 요소가 연속적으로 이어져 있지 않고 length와 배열 요소의 개수가 일치하지 않는다.  

### 배열 생성
**배열 리터럴**: 0개 이상의 요소를 쉼표로 구분하여 대괄호로 묶는다.  
**Array 생성자 함수**: 전달된 인수가 1개이고 숫자인 경우 length 프로퍼티 값이 인수인 배열을 생성한다.  
**Array.of 메서드**: 전달된 인수를 요소로 갖는 배열을 생성한다.  
**Array.from 메서드**: 유사 배열 객체 또는 이터러블 객체를 인수로 전달받아 배열로 변환하여 반환한다. 두 번째 인수로 전달한 콜백 함수를 통해 값을 만들면서 요소를 채울 수 있다.  

**유사 배열 객체<sup>array-like object</sup>**: 마치 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있고 length 프로퍼티를 갖는 객체를 말한다.  

### 배열 메서드
배열에는 원본 배열(배열 메서드를 호출한 배열, 즉 배열 메서드의 구현체 내부에서 this가 가리키는 객체)을 직접 변경하는 메서드<sup>mutator method</sup>와 원본 배열을 직접 변경하지 않고 새로운 배열을 생성하여 반환하는 메서드<sup>accessor method</sup>가 있다.  

**Array.isArray 메서드**: 전달된 인수가 배열이면 true, 배열이 아니면 false를 반환한다.  
**Array.prototype.indexOf 메서드**: 원본 배열에서 인수로 전달된 요소를 검색하여 인덱스를 반환한다.  
**Array.prototype.push 메서드<sup>m</sup>**: 인수로 전달받은 모든 값을 원본 배열의 마지막 요소로 추가하고 변경된 length 프로퍼티 값을 반환한다.  
**Array.prototype.pop 메서드<sup>m</sup>**: 원본 배열에서 마지막 요소를 제거하고 제거한 요소를 반환한다.  
**Array.prototype.unshift 메서드<sup>m</sup>**: 인수로 전달받은 모든 값을 원본 배열의 선두에 요소로 추가하고 변경된 length 프로퍼티 값을 반환한다.  
**Array.prototype.shift 메서드<sup>m</sup>**: 원본 배열에서 첫 번째 요소를 제거하고 제거한 요소를 반환한다.  
**Array.prototype.concat 메서드**: 인수로 전달된 값들(배열 또는 원시값)을 원본 배열의 마지막 요소로 추가한 새로운 배열을 반환한다. 인수로 전달한 값이 배열인 경우 배열을 해체하여 새로운 배열의 요소로 추가한다.  
**Array.prototype.splice 메서드<sup>m</sup>**: 원본 배열의 중간에 요소를 추가하거나 중간에 있는 요소를 제거하고 제거한 요소를 반환한다.  
**Array.prototype.slice 메서드**: 첫 번째 인수로 전달받은 인덱스부터 두 번째 인수로 전달받은 인덱스 이전까지 요소들을 복사하여 배열로 반환한다.  
**Array.prototype.join 메서드**: 원본 배열의 모든 요소를 문자열로 변환한 후, 인수로 전달받은 문자열로 연결한 문자열을 반환한다.  
**Array.prototype.reverse 메서드<sup>m</sup>**: 원본 배열의 순서를 반대로 뒤집고 변경된 배열을 반환한다.  
**Array.prototype.fill 메서드<sup>m</sup>**: 인수로 전달받은 값을 배열의 처음부터 끝까지 요소로 채운다.  
**Array.prototype.includes 메서드**: 배열 내에 특정 요소가 포함되어 있는지 확인하여 true 또는 false를 반환한다.  
**Array.prototype.flat 메서드**: 인수로 전달한 깊이만큼 재귀적으로 배열을 평탄화한다.  

---
연산자<sup>operator</sup>  
피연산자<sup>operand</sup>  
부수 효과<sup>side effect</sup>  
암묵적 타입 변환<sup>implicit coercion</sup> 또는 타입 강제 변환<sup>type coercion</sup>  
동등 비교<sup>loose equality</sup>(값)  
일치 비교<sup>strict equality</sup>(값과 타입)  
삼항 조건 연산자<sup>temary operator</sup>(값으로 평가할 수 있는 표현식인 문)  
폴스루<sup>fall through</sup>  
레이블 문<sup>label statement</sup>  
명시적 타입 변환<sup>explicit coercion</sup> 또는 타입 캐스팅<sup>type casting</sup>  
단축 평가<sup>short-circuit evaluation</sup>  
옵셔널 체이닝<sup>optional chaining</sup>(?.)  
null 병합<sup>nullish coalescing</sup>(??)  
계산된 프로퍼티 이름<sup>computed property name</sup>  
유사 배열 객체<sup>array-like object</sup>  
얕은 복사<sup>shallow copy</sup>와 깊은 복사<sup>deep copy</sup>  
암묵적 결합<sup>implicit coupling</sup>  
일시적 사각지대<sup>Temporal Dead Zone, TDZ</sup>(스코프 시작 시점부터 초기화 시작 시점까지 변수를 참조할 수 없는 구간)  
프로퍼티 디스크립터<sup>PropertyDescriptor</sup> 객체  
바인딩<sup>name binding</sup>(식별자와 값을 연결하는 과정을 의미)  
스코프 세이프 생성자 패턴<sup>scope-safe constructor</sup>  
프로퍼티 섀도잉<sup>property shadowing</sup>  
암묵적 전역<sup>implicit global</sup>  
