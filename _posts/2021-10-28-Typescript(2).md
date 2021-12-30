---
title: '[Typescript] Typescript 기본 문법 알아보기(2)'
excerpt: 'Interface, Enum, Generic'

categories:
  - Typescript
tags:
  - [Javascript, js, Typescript, ts, React]
last_modified_at: 2021-10-28
toc: true  
toc_sticky: true
---


[Typescript의 기본 문법 (타입, 접근제한자, getter & setter)](https://waterdrag0n.github.io/typescript/Typescript(1)/)을 알아본 이전 포스팅에 이어 Interface, Enum, Generic에 대해 알아보자.

## Interface

프로퍼티를 정의해서 사용하고자 할 때는 object 타입이 아닌 Interface를 사용해야 한다.

### 객체형

```tsx
type langs = 'js' | 'ts' | 'java' | 'python';

interface Person {
	property1 : string;
	property2 : number;
	property3? : boolean; // 없어도 에러나지 않음
	readonly property4 : number; // 처음에 값 할당 후 수정 불가
	[key : string] : langs;
}

let person : Person = {
	property1 : 'hello',
	property2 : 100,
	property4 : 200,
	'property' : 'python', // [key:string] : string;
	// 'property' : 'c++'
}

// person.property4 = 1; error!
```

### 함수형

```tsx
interface Func {
	(var1 : number, var2 : number): number; // number 2개 받고 number return
}

const func : Func = function(var1, var2) {
	return var1 + var2;
}

const func2 : Func = (a, b) => {
	return a + b;
}
```

### 클래스형

```tsx
interface ClassInterface {
	var1 : string;
	var2 : number;
	func(): void;
}

class ClassImplement implements ClassInterface {
	var1 = 'str';
	var2;
	constructor(var2: number){
		this.var2 = var2;
	}
	func() = {console.log('interface!')}
}

// interface 확장
interface ClassInterface2 extends ClassInterface {
	var3 : boolean;
	func2(): number;
}

class ClassImplement2 implements ClassInterface2 {
	// ClassInterface와 ClassInterface2의 변수 모두 구현해야 한다. 
}

class ClassImplement3 implements ClassInterface, ClassInterface2 {
	...
}
```

## Enum

```tsx
enum ProgrammingLanguage {
	javascript = 'js',
	typescript = 'ts'
}

const jsAbbreb : ProgrammingLanguage = ProgrammingLanguage.javascript

// object 타입이기 때문에 똑같이 활용 가능
Object.keys(ProgrammingLanguage) // ['javascript', 'typescript']
Object.values(ProgrammingLanguage) // ['js', 'ts']
```

## Generic

제네릭이 없고 타입만 있다면, 같은 기능을 하지만 타입만 다른 함수들이 있는 상황에 어쩔 수 없이 모두 수작업으로 작성을 해야 할 것이다.

하지만 제네릭이 있기 때문에 중복되는 코드를 줄일 수 있다.

```tsx
function GenericFunc<T>(arg : T) : T {
	return arg;
}

let result = GenericFunc<number>(100); // 100

function GenericFunc2<T>(arg: T[]) : number {
	return arg.length;
}

class GenericClass<T> {
	val1 : T;
	func1 : (par1:T, par2:T) => T;
}

let myGenericClass = new GenericClass<number>();
myGenericClass.val1 = 0;
myGenericClass.func1 = (x, y) => x + y;
```

## 참고

[https://velog.io/@soulee__/TypeScript-Interface-2](https://velog.io/@soulee__/TypeScript-Interface-2)

[https://youtu.be/OIMPLNICzoc](https://youtu.be/OIMPLNICzoc)

[https://www.typescriptlang.org/ko/docs/handbook/2/generics.html](https://www.typescriptlang.org/ko/docs/handbook/2/generics.html)

[https://hyunseob.github.io/2017/01/14/typescript-generic/](https://hyunseob.github.io/2017/01/14/typescript-generic/)