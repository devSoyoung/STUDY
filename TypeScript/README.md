# 타입스크립트(Typescript)
## Getting Started
### Typescript 설치
```
$ npm install typescript
```

### Typescript 컴파일

* 타입스크립트는 실제 브라우저에서 실행 가능한 언어가 아님
* **컴파일 과정**을 통해 브라우저에서 실행 가능한 자바스크립트 코드로 변환되어야 함(**트랜스 컴파일**)

```
$ tsc [컴파일할 ts파일]
```

***
## TypeScript 기본타입
### Boolean
```typescript
let isDone: boolean = false;
```
true, false

### Number
```typescript
let decimal: number = 10;
let hex: number = 0xf00d;
```
10진수, 2진수, 8진수, 16진수 등의 모든 숫자 타입

### String
```typescript
let color: string = 'red';
```
문자열, (자바스크립트와 동일하게) `'`와 `"` 모두 지원함
* [ES6 추가 문법] 백틱(`)으로 문자열 치환도 동일하게 사용 가능

### Array
```typescript
let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];
```
타입의 뒤에 `[]`를 붙이는 방법과 Array의 <> 안에 타입을 명시하는 두 가지 방법이 있음

### Tuple
```typescript
let x: [string, number];        // 선언
x = ["apple", 1]    // 초기화
x = [1, "apple"]    // 에러
console.log(x[0].substr(1))     // 동작
console.log(x[1].substr(1))     // 에러
```
잘못된 값으로 초기화하면 에러, 해당 타입의 메소드만 사용 가능

```typescript
x[3] = "apple";
x[4] = 5;
x[6] = false;       // 에러
```
**범위 밖의 값을 설정하는 경우** 지정한 타입(string, number)이면 설정 가능하고, 다른 타입인 경우 에러 발생

### Enum
```typescript
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
```
숫자형 변수들의 묶음인 enum도 지원함

### Any
```typescript
let notSure: any = 4;
notSure = '4';
```
어떤 타입이든 가능하고, 중간에 다른 타입의 값으로 변경도 가능
> 타입스크립트를 사용하는 이점이 없기 때문에, 특수한 상황이 아니라면 남용하지 말자

### Void
```typescript
function warnUser(): void {
    console.log("This is my warning message");
}
```
함수의 리턴 값이 없는 경우 사용
> 변수의 경우 사용하지 않는데, undefined나 null을 지정해주기 때문

### Null and Undefined
```typescript
let u: undefined = undefined;
let n: null = null;
```
두 값이 각각 타입을 가지며, 모든 타입(number, string ..)의 기본이 되기 때문에, 나중에 다른 타입의 값 할당 가능
* `--strictNullChecks` : (권장) 


### Never
```typescript

```

### Object
```typescript

```

***

## 인터페이스
자바, C#과 같은 정적 타입 언어에서 사용되던 것으로, 클래스의 구현부 없이 정의만 있는 것
* 객체가 어떠한 프로퍼티와 메소드를 가지는지 정의
* 실질적인 구현은 이를 구현하는 클래스에서 함

```typescript
interface Shape {
    getArea(): number;
}

class App implements Shape {
    width: number;
    height: number;
    constructor(width, height) {
        this.width = width;
        this.height = height;
    }
    
    function getArea() {
        const { width, height } = this;
        return width * height;
    }
}
```

### 인터페이스와 덕 타이핑

인터페이스를 활용하면 [덕 타이핑](https://ko.wikipedia.org/wiki/%EB%8D%95_%ED%83%80%EC%9D%B4%ED%95%91)을 할 때 메소드를 검사하지 않고도 런타임 에러를 막을 수 있음
* **타입스크립트의 덕 타이핑** : 어떤 객체가 특정 인터페이스에서 명시하는 메소드를 가지고 있다면, 해당 객체가 그 인터페이스를 구현한 것으로 간주 

```typescript
interface Quackable {
    quack(): void;
}

class Duck implements Quackable {
    quack() {
        console.log("quack!");
    }
}

class Person {
    quack() {
        console.log("quack too!");
    }
}

function makeSomeNoiseWith(duck: Quackable): void {
    duck.quack();
}

makeSomeNoiseWith(new Duck());
makeSomeNoiseWith(new Person());
```

* `implements`로 명시적으로 `Quackable`를 구현한 **Duck**는 `makeSomeNoiseWith()`의 파라미터로 전달 가능
* **Person**은 명시적으로 `Quackable`를 구현하지 않았지만, quack()를 구현했기 때문에 `makeSomeNoiseWith()`의 파라미터로 전달 가능 => 구조적 타이핑(Structural Typing)

