---
title: Spring Annotation을 이용한 Properties 파일에서 리스트 읽기
date: 2023-09-24 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - Annotation
  - Properties
---
## 소개

Spring Framework에서는 여러가지 설정값을 관리하기 위해 Properties 파일을 자주 사용합니다. 이 문서에서는 `@Value` 어노테이션을 이용하여 Properties 파일에서 리스트를 읽어오는 방법을 설명하겠습니다.

## 에러명: NoMatchingBeanDefinitionException

가장 먼저 자주 발생하는 문제는 `NoMatchingBeanDefinitionException`입니다. 이 오류는 Spring이 필요한 Bean을 찾지 못했을 때 발생합니다. 이 문제를 해결하기 위해서는 올바르게 Bean을 정의해야 합니다.

## @Value 어노테이션 이해하기

`@Value`는 Spring에서 제공하는 어노테이션입니다. 이 어노테이션은 클래스의 필드에 직접 값을 할당할 수 있게 해줍니다. 예를 들어, Properties 파일에 아래와 같은 설정이 있다고 가정해보겠습니다.

```properties
my.list=1,2,3,4,5
```

이런 설정값을 `List<Integer>` 형태로 불러오고 싶다면 `@Value` 어노테이션을 이렇게 사용할 수 있습니다.

```java
@Value("#{'${my.list}'.split(',')}")
private List<Integer> myList;
```

여기서 `#{'${my.list}'.split(',')}` 부분은 Spring Expression Language(SpEL, 스프링 표현 언어)를 사용한 것입니다. 이 표현을 통해 문자열을 쉼표(',')로 분리하고 리스트로 변환합니다.

## 주의사항

단순한 값 뿐만 아니라, 복잡한 자료구조도 불러올 수 있지만, 형식에 맞지 않는 값을 할당하려고 하면 오류가 발생할 수 있습니다. 따라서 Properties 파일의 값과 Java 클래스 필드의 타입이 잘 매칭되는지 확인이 필요합니다.

## 결론

`@Value` 어노테이션과 Spring Expression Language를 활용하면 Properties 파일에서도 리스트 형태의 데이터를 쉽게 불러올 수 있습니다. 이 방법을 활용하면 설정값을 유연하게 관리할 수 있어, 개발의 효율성을 높일 수 있습니다.