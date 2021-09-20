---
title: '[Java] Annotation'
excerpt: 'Annotation의 역할, 사용법, Custom Annotation을 만드는 법을 알아보자.'

categories:
  - Java
tags:
  - [Java, Spring]
last_modified_at: 2021-09-16
toc: true  
toc_sticky: true
---

자바 공부를 하다보면 어노테이션을 자주 보게 되지만 이것들이 실제 어떤 일을 하는지에 대해 깊게 생각해본 적은 없을 것이다.

주로 부모 클래스를 상속 받아 메서드를 오버라이드할 때 @Override라는 어노테이션을 본 게 전부일텐데, 어노테이션을 왜 쓰는지, 어떻게 쓰는지, 더 나아가서 어떻게 커스텀 어노테이션을 만들 수 있는지 알아보자.

## 어노테이션이란

어노테이션은 그대로 직역하면 주석이라는 뜻이다. 

하지만 주석처럼 아무 기능 없는 텍스트는 아니고, 미리 정의된 어노테이션을 통해 다른 프로그램에 필요한 정보를 제공하는 **메타데이터**(meta data: 데이터에 대한 데이터. 데이터를 설명해주는 데이터)로서의 역할을 한다.

즉, 주석처럼 쓰이지만 그 안에서 특정한 의미를 제공하거나 기능을 하게 된다.

자바의 내장 어노테이션은 표준 어노테이션과 메타 어노테이션으로 분류된다.

## 표준 어노테이션

### @Override

해당 메서드가 오버라이드된 메서드라는 것을 알려준다.

조상 클래스에서 메서드를 찾을 수 없으면 에러를 발생시킨다.

```java
class ParentClass {
	void parentMethod(){}
}

class ChildClass extends ParentClass {
	@Override
	void parentMethod(){ ... }
}
```

### @Deprecated

해당 메서드가 다른 것으로 대체되었으니 사용하지 않을 것을 권하는 의미이다.

@Deprecated가 붙은 메서드를 사용하면 에러는 나지 않지만 경고가 나타난다.

### @FunctionalInterface

함수형 인터페이스를 선언할 때 붙일 수 있으며 (필수 아님) 함수형 인터페이스를 올바르게 선언했는지 확인한다.

### @SuppressWarnings

경고메시지가 나타나지 않게 한다.

앞서 @Deprecated가 경고를 발생시킨다고 기술했는데, 이러한 경고 발생을 무시하는 역할을 한다.

```java
@SuppressWarnings("deprecation")
@SuppressWarnings({"deprecation", "varargs"})
```

### @SafeVarargs

메서드에서 제네릭과 같은 가변인자를 매개변수로 사용할 때 발생하는 "unchecked" 경고를 무시한다.

오버라이드된 메서드에는 사용할 수 없고, static이나 final이 붙은 메서드, 생성자에 붙일 수 있다.

unchecked warning
매개변수에 제네릭을 사용할 경우 컴파일 과정에서 타입 T는 Object로 바뀌게 되고, 이는 모든 타입 객체가 들어올 수 있다는 의미이기 때문에 위험하다고 경고를 보낸다.

## 메타 어노테이션

다음에 설명할 커스텀 어노테이션을 정의할 때 사용되는 어노테이션의 어노테이션이다.

어노테이션을 정의할 때 적용대상, 유지기간 등을 지정하는 데에 사용된다.

### @Target

어노테이션이 적용할 대상을 지정한다.

```java
@Target({TYPE, FIELD, METHOD})
```

- @Target으로 지정 가능한 적용대상의 종류
    - ANNOTATION_TYPE: 어노테이션
    - CONSTRUCTOR: 생성자
    - FIELD: 필드
    - LOCAL_VARIABLE: 지역변수
    - METHOD: 메서드
    - PACKAGE: 패키지
    - PARAMETER: 매개변수
    - TYPE: 타입
    - TYPE_PARAMETER: 타입 매개변수
    - TYPE_USE: 타입이 사용되는 모든 곳

### @Retention

어노테이션이 유지되는 기간 지정

- 어노테이션의 유지 정책의 종류
    - SOURCE: 소스파일에만 존재
    - CLASS: 클래스파일에 존재하지만 실행시에 사용 불가 (default)
    - RUNTIME: 클래스파일에 존재하며 실행시에 사용 가능

```java
@Retention(RetentionPolicy.RUNTIME)
```

### @Documented

어노테이션에 대한 정보가 javadoc으로 작성한 문서에 포함된다.

@Override와 @SuppressWarnings를 제외한 모든 기본 어노테이션에 붙어 있다.

### @Inferited

어노테이션이 자손 클래스에 상속된다.

### @Repeatable

반복적으로 어노테이션을 선언할 수 있다.

### @Native

네이티브 메서드에 의해 참조되는 상수 필드에 붙인다.

## 커스텀 어노테이션

커스텀 어노테이션을 정의하는 방법은 인터페이스 정의와 동일하다.

```java
@interface CustomAnnotation {
	type name();
}
```

### 어노테이션의 요소

위의 예와 같이 어노테이션 내부에 선언된 메서드를 어노테이션의 요소라고 한다.

어노테이션의 요소는 추상 메서드의 형태 (반환값 이름(); 매개변수 없음)을 가진다.

### 어노테이션 규칙

- 요소의 타입은 기본형, String, enum, 어노테이션, Class만 허용된다.
- () 안에 매개변수를 선언할 수 없다.
- 예외를 선언할 수 없다.
- 요소를 타입 매개변수로 지정할 수 없다.
- 각 요소는 기본값을 가질 수 있다.

```java
@interface TestAnnotation {
	int count() default 1; // 기본값이 1개인 경우
	String[] info() default {"a", "b"}; // 기본값이 여러개인 경우
}
@TestAnnotation // @TestAnnotation(count=1, info={"a", "b"}) 동일
```

- 요소가 1개이고 이름이 value이면 요소의 이름을 생략할 수 있다.

```java
@interface TestAnnotation2 {
	int value();
}

@TestAnnotaton2(2) // @TestAnnotaton2(value=2) 동일
```

### 마커 어노테이션

어노테이션의 값이 필요가 없어 요소를 지정하지 않을 수 있다.

이를 마커 어노테이션이라고 한다. 

- 참고

자바의 정석 Chapter 12