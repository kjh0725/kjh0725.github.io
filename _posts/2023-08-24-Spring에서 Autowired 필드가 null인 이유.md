---
title: Spring에서 Autowired 필드가 null인 이유
date: 2023-08-24 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - Autowired
  - "Null"
---
## 소개

Spring 프레임워크에서 의존성 주입(Dependency Injection)을 쉽게 처리하기 위해 `@Autowired` 애노테이션을 사용합니다. 그런데 이 애노테이션을 사용하다 보면, 예상치 못한 문제로 `null` 값을 반환하는 경우가 있습니다. 이 글에서는 그 원인과 해결 방법에 대해 자세히 알아보겠습니다.

## 주요 원인: 컨테이너 밖에서 생성된 객체

Spring에서 `@Autowired`가 작동하지 않는 가장 흔한 이유는, 해당 객체가 Spring 컨테이너의 관리 밖에서 생성된 경우입니다. Spring은 `@Component`, `@Service`, `@Repository` 등의 애노테이션을 사용해 객체를 관리하므로, 이 애노테이션이 없는 클래스는 `@Autowired`가 적용되지 않습니다.

## 해결 방법 1: 애노테이션 추가

해당 클래스에 `@Component` 또는 관련 애노테이션을 추가하여 Spring이 관리할 수 있게 만들 수 있습니다. 예를 들어,

```java
@Component
public class MyClass {
    @Autowired
    private MyService myService;
}
```

## 해결 방법 2: 스프링 컨텍스트에서 객체 얻기

만약 외부 라이브러리나 외부 코드에서 객체를 가져와야 한다면, 스프링 컨텍스트에서 명시적으로 객체를 얻어와야 합니다. `ApplicationContext`를 사용하면 가능합니다.

```java
MyClass myClass = context.getBean(MyClass.class);
```

## 해결 방법 3: `@PostConstruct` 사용

객체가 생성된 후 초기화 작업을 수행해야 하는 경우 `@PostConstruct` 애노테이션을 사용할 수 있습니다. 이 애노테이션은 객체 생성 후에 실행되므로 `null` 문제를 해결할 수 있습니다.

```java
@PostConstruct
public void init() {
    myService.doSomething();
}
```

## 정리

Spring에서 `@Autowired` 필드가 `null`인 경우 주로 객체가 Spring 컨테이너 밖에서 생성되어서 그렇습니다. 이 문제를 해결하기 위해 해당 클래스에 애노테이션을 추가하거나, 스프링 컨텍스트에서 객체를 명시적으로 가져오거나, `@PostConstruct`를 사용할 수 있습니다. 이러한 방법들로 대부분의 문제를 해결할 수 있습니다.