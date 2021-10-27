---
title: '[Typescript] Typescript 기본 문법 알아보기(1)'
excerpt: '타입, 접근제한자, getter & setter'

categories:
  - Typescript
tags:
  - [Javascript, js, Typescript, ts, React]
last_modified_at: 2021-10-21
toc: true  
toc_sticky: true
---

기존 Javascript에 기능이 추가된 Typescript는 타입이 도입된 상위집합이다.

Javascript의 type이 너무 프리하다는 단점(가끔 장점)을 보완해줌과 동시에 기존에 없었던 interface와 enum을 사용할 수 있어 유용하다.

이에 대한 설명은 2편에서 확인해보도록 하고 우선, Typescript의 기본적인 문법을 정리해보자.

## Type

가장 큰 특징으로, 타입을 지정하여 버그를 방지한다.

적용 가능한 타입: string, number, boolean, null, undefined, bigint, [], {}

- 타입으로 any 지정 시 모든 타입 가능

### 변수

```tsx
let num1 : number = 1;
// num1 = 'str';
num1 = 2;

let arr : string[] = ['str1', 'str2'];

// union type
let union : string | number = 'str3';
union = 10; // ok!

// type alias : type을 변수화
type MyType = string | number;
let alias1 : MyType = 456;

//tuple type
type Tuple = [string, boolean];
let arr2 : Tuple = ['hi', false];
```

### 객체

```tsx
const obj : {key1 : string} = {key1 : 'hello'};

type MyType2 = {
	[key : string] : string, // string key에 value key
}

const obj2 : MyType2 = {'key' : 'val'};
```

### 함수 & 클래스

```tsx
// number x 받고 number 리턴
// ?를 붙여서 옵션 인자로 지정. 없을 시 로직 만들어주기
function func(x : number, y? : number) : number {
	if(y) ...
	else
		return x * 2;
}

class Class1 {
	varr : number;
	constructor(varr : number) {
		this.varr = varr;
	}

	doNothing (varr2 : boolean) : void {
		...
	}
}
```

## 접근제한자

Java같은 객체지향 언어에서 주로 보이던 접근제한자를 사용할 수 있다.

```tsx
class Class2 {
	public var1 : number = 1;
	protected var2 : string = 'protected';
	private _var3 : null = null; // private varible naming convention (_)
	var4 : undefined = undefined; // 접근제한자 생략 시 public
}

class Class3 {
	// var1, var2, var4 사용 가능
}
```

## getter, setter

```tsx
class Class4 {
	private _privateVar : string | null = null;

	get privateVar() : string {
		return this._privateVar;
	}

	set privateVar(newVal : string) {
		this._privateVar = newVal;
	}
}
```

- 참고

[https://yamoo9.gitbook.io/typescript/classes/getter-setter](https://yamoo9.gitbook.io/typescript/classes/getter-setter)

[https://kkangdda.tistory.com/67](https://kkangdda.tistory.com/67)

[https://youtu.be/xkpcNolC270](https://youtu.be/xkpcNolC270)