---
title: Spring 프레임워크에서 단위 테스트 시 @Value 어노테이션 사용하기
date: 2023-09-17 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - 프레임워크
  - Value어노테이션
---
## 문제 상황

Spring 프레임워크에서 개발을 하다 보면, `@Value` 어노테이션을 사용하여 프로퍼티 값을 주입받는 경우가 많습니다. 그러나 단위 테스트를 실행할 때 이러한 값들이 제대로 주입되지 않아 문제가 발생할 수 있습니다. 이 글에서는 그러한 문제를 어떻게 해결할 수 있는지에 대해 알아보겠습니다.

## MockPropertySource 사용하기

`MockPropertySource`는 테스트 환경에서 프로퍼티 값을 가짜로 설정할 수 있게 도와줍니다. 이것을 사용하면 `@Value` 어노테이션을 통해 주입받은 값을 제어할 수 있습니다.

```java
@Test
public void testSomething() {
    MockPropertySource mockPropertySource = new MockPropertySource();
    mockPropertySource.setProperty("your.property.name", "yourValue");
    TestPropertyValues.of(mockPropertySource).applyTo(applicationContext);
    // 이후 테스트 로직을 실행합니다.
}
```

여기서 "your.property.name"는 프로퍼티의 키 이름이고, "yourValue"는 그에 대응하는 값입니다.

## ReflectionTestUtils 사용하기

Reflection은 자바에서 동적으로 클래스나 메서드를 조작할 수 있는 기능입니다. `ReflectionTestUtils`는 이러한 리플렉션을 이용해 `@Value` 어노테이션을 가진 필드의 값을 설정할 수 있습니다.

```java
@Test
public void testAnotherThing() {
    ReflectionTestUtils.setField(yourClassInstance, "yourFieldName", "yourValue");
    // 이후 테스트 로직을 실행합니다.
}
```

여기서 "yourFieldName"은 `@Value` 어노테이션이 붙은 필드의 이름이고, "yourValue"는 그 필드에 주입할 값입니다.

## 결론

단위 테스트에서 `@Value` 어노테이션을 사용하여 값을 주입받을 때는 `MockPropertySource`나 `ReflectionTestUtils`를 활용할 수 있습니다. 각 방법은 다르게 작동하지만 목적은 같으며, 어떤 방법을 사용할지는 상황과 필요에 따라 결정할 수 있습니다. 이 두 방법을 잘 활용하면 테스트 환경에서도 원활하게 `@Value` 어노테이션을 사용할 수 있습니다.