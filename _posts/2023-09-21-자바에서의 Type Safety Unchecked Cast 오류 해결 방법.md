---
title: 자바에서의 Type Safety Unchecked Cast 오류 해결 방법
date: 2023-09-21 20:00:00 +0900
categories:
  - Spring
tags:
  - JavaScript시간
  - Java오류
---
## 오류의 정의와 발생 이유

자바에서 프로그래밍을 하다보면, 가끔 "Type Safety: Unchecked Cast"라는 오류를 마주치게 됩니다. 이러한 오류는 제네릭(generics)을 사용할 때 주로 발생하며, 컴파일러가 타입의 안전성을 보장할 수 없을 때 나타납니다. 여기서 '제네릭'이란, 다양한 타입을 하나의 클래스나 메서드에서 처리할 수 있게 하는 프로그래밍 기술을 의미합니다.

## 해결 전략 1: 명시적 타입 선언

오류를 해결하기 위한 첫 번째 방법은 명시적으로 타입을 선언하는 것입니다. 제네릭 타입에 어떤 클래스가 들어갈지 명확히 알려줘야 컴파일러가 오류를 발생시키지 않습니다.

```java
List<String> list = new ArrayList<>();
```

위 코드처럼 `String` 타입을 명시적으로 선언하면, "Unchecked Cast" 오류를 피할 수 있습니다.

## 해결 전략 2: @SuppressWarnings 어노테이션 사용

두 번째 방법은 `@SuppressWarnings("unchecked")` 어노테이션을 사용하는 것입니다. 이 어노테이션은 컴파일러에게 해당 부분의 코드가 안전하다고 알려주는 역할을 합니다.

```java
@SuppressWarnings("unchecked")
List<String> list = (List<String>) getObject();
```

이 방법은 코드의 안전성을 프로그래머가 보장한다는 전제 하에 사용되어야 합니다.

## 해결 전략 3: instanceof 연산자 활용

마지막으로, `instanceof` 연산자를 사용하여 객체의 타입을 런타임에 체크할 수 있습니다. 이는 타입 안전성을 런타임에 확보하는 방법입니다.

```java
Object obj = getObject();
if(obj instanceof List<?>) {
    List<?> list = (List<?>) obj;
}
```

`instanceof` 연산자를 통해 `obj`의 실제 타입이 `List<?>`인지 확인한 후에 캐스팅을 수행합니다.

## 결론

"Type Safety: Unchecked Cast" 오류는 자바에서 제네릭을 사용할 때 자주 발생하는 문제입니다. 이 오류를 해결하기 위해 명시적 타입 선언, `@SuppressWarnings` 어노테이션, 그리고 `instanceof` 연산자를 활용할 수 있습니다. 각 해결 전략에는 그에 맞는 적절한 사용 시나리오가 있으므로, 상황에 따라 적절한 방법을 선택하면 됩니다.