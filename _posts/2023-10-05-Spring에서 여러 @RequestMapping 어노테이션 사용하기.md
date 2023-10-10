---
title: Spring에서 여러 RequestMapping 어노테이션 사용하기
date: 2023-10-05 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - RequestMapping
---
## 문제 상황: `@RequestMapping` 어노테이션 충돌

Spring Framework에서 웹 어플리케이션을 개발하다 보면, 여러 URL 패턴을 하나의 컨트롤러나 메서드에 매핑해야 할 때가 있습니다. 이럴 때 사용하는 것이 `@RequestMapping` 어노테이션입니다. 그런데 문제는, 같은 컨트롤러 안에서 같은 메서드에 여러 개의 `@RequestMapping`을 어떻게 적용할지 모르는 경우입니다.

## 해결책: `value` 속성 활용하기

`@RequestMapping` 어노테이션에는 `value`라는 속성이 있습니다. 이 `value` 속성은 배열 형태로 URL 패턴을 받을 수 있어요. 이를 통해 하나의 메서드에 여러 URL을 매핑할 수 있습니다. 

```java
@RequestMapping(value = {"/url1", "/url2"})
public String handleMultipleUrls() {
  // 로직 구현
}
```

이렇게 하면 `/url1`과 `/url2` 두 가지 경로로 들어오는 요청을 동일한 메서드로 처리할 수 있습니다.

## 고려사항: HTTP 메서드와 `params`

`@RequestMapping`은 단순히 URL 패턴만을 고려하는 것이 아니라, HTTP 메서드나 파라미터 등도 함께 고려할 수 있습니다. 예를 들어, 특정 HTTP 메서드(GET, POST 등)로만 요청을 받고 싶다면 `method` 속성을 사용합니다.

```java
@RequestMapping(value = {"/url1", "/url2"}, method = RequestMethod.GET)
public String handleGetRequests() {
  // 로직 구현
}
```

`params` 속성을 이용하면 특정 파라미터가 있는 요청만을 처리할 수 있습니다. 

```java
@RequestMapping(value = "/url", params = "type=myType")
public String handleWithParam() {
  // 로직 구현
}
```

## 주의사항: Ambiguous Mapping Error

동일한 URL 패턴과 HTTP 메서드를 가진 `@RequestMapping`이 여러 개 존재하면 `Ambiguous Mapping Error`가 발생합니다. 이러한 오류는 개발자가 실수로 중복된 매핑을 생성할 경우 나타납니다. 이를 해결하기 위해서는 각 `@RequestMapping`이 유니크하게 설정되어야 합니다.

## 결론

Spring에서 `@RequestMapping`을 효율적으로 활용하려면 `value`, `method`, `params` 등 다양한 속성들을 잘 조합해야 합니다. 이를 통해 더욱 강력하고 유연한 URL 매핑 전략을 구성할 수 있습니다.