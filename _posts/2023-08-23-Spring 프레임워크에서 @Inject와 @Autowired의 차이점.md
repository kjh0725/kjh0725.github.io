---
title: Spring 프레임워크에서 @Inject와 @Autowired의 차이점
date: 2023-08-23 20:00:00 +0900
categories:
  - Spring
tags:
  - Inject
  - Autowired
  - Spring
  - 프레임워크
---
## 개요

Spring 프레임워크에서 의존성 주입(Dependency Injection)을 할 때 두 가지 주요 어노테이션(Annotation)인 `@Inject`와 `@Autowired`가 있습니다. 이 두 어노테이션은 비슷해 보이지만 몇 가지 중요한 차이점이 있습니다. 이 글에서는 그 차이점을 자세히 알아보겠습니다.

## 출처와 표준성

`@Autowired` 어노테이션은 Spring 프레임워크 자체에서 제공됩니다. 즉, Spring 전용입니다. 반면에 `@Inject`는 Java의 표준 어노테이션으로, JSR-330이라는 자바 표준을 따릅니다. 여러 다른 프레임워크에서도 `@Inject`를 사용할 수 있습니다.

## 선택적 의존성 주입

`@Autowired`는 선택적인 의존성을 주입할 수 있습니다. `required` 속성을 `false`로 설정하면, 스프링은 해당 의존성을 찾지 못해도 에러를 발생시키지 않습니다. 예를 들어, `@Autowired(required=false)`와 같이 설정할 수 있습니다. `@Inject`에서는 이러한 선택적 주입이 불가능합니다.

## 자격 지정자(Qualifier)

두 어노테이션 모두 자격 지정자(Qualifier)를 사용하여 의존성을 선택적으로 주입할 수 있습니다. `@Autowired`는 `@Qualifier` 어노테이션을 함께 사용하면 됩니다. `@Inject`는 `@Named` 어노테이션을 사용하여 동일한 기능을 수행할 수 있습니다.

## 에러 처리

`@Autowired`와 `@Inject`를 사용할 때 발생할 수 있는 에러는 대체로 유사합니다. 예를 들어, 필요한 빈(Bean)을 찾지 못한 경우 `NoSuchBeanDefinitionException`이 발생합니다. 이 에러는 둘 다 비슷한 방식으로 처리됩니다.

## 결론

`@Inject`와 `@Autowired`는 모두 Spring 프레임워크에서 의존성을 주입하기 위해 사용되지만, 표준성, 선택적 의존성 주입, 자격 지정자의 사용 등에서 차이가 있습니다. 이러한 차이를 이해하고 상황에 맞게 적절한 어노테이션을 선택하는 것이 중요합니다.