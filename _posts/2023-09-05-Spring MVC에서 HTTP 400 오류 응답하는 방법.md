---
title: Spring MVC에서 HTTP 400 오류 응답하는 방법
date: 2023-09-05 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringMVC
  - HTTP400오류
---
## 개요

Spring MVC는 자바 웹 애플리케이션을 개발할 때 사용하는 프레임워크입니다. 이 글에서는 Spring MVC에서 `@ResponseBody` 어노테이션을 사용한 메서드에서 HTTP 400 (Bad Request) 오류를 어떻게 응답하는지에 대해 알아보겠습니다.

## @ResponseBody와 HTTP 상태 코드

`@ResponseBody` 어노테이션은 메서드가 반환하는 값을 HTTP 응답 본문에 직접 쓰도록 지시합니다. 이를 사용하면 다양한 HTTP 상태 코드를 설정하는 여러 가지 방법이 있습니다. HTTP 상태 코드는 웹 서버가 클라이언트에게 전달하는 응답의 상태를 나타냅니다. 예를 들어, 200은 성공을, 400은 잘못된 요청을 나타냅니다.

## ResponseEntity 사용하기

`ResponseEntity` 클래스를 사용하면 HTTP 상태 코드와 함께 응답을 보낼 수 있습니다.

```java
public ResponseEntity<String> yourMethod() {
  if (someCondition) {
    return new ResponseEntity<>("Your Message", HttpStatus.BAD_REQUEST);
  }
  return new ResponseEntity<>("Success Message", HttpStatus.OK);
}
```

## HttpStatus Enum 활용하기

`HttpStatus`는 HTTP 상태 코드를 간편하게 관리할 수 있는 Enum입니다. 위 예시에서 `HttpStatus.BAD_REQUEST`와 `HttpStatus.OK`는 각각 400과 200 상태 코드를 나타냅니다.

## @ResponseStatus 어노테이션 이용하기

`@ResponseStatus(HttpStatus.BAD_REQUEST)` 어노테이션을 메서드 또는 예외 클래스 위에 붙여 사용할 수도 있습니다.

```java
@ResponseStatus(HttpStatus.BAD_REQUEST)
public void yourMethod() {
  // Your logic here
}
```

## 핵심 정리

Spring MVC에서 `@ResponseBody`를 사용한 메서드에서 HTTP 400 오류를 응답하는 방법은 다양합니다. `ResponseEntity`를 사용하거나, `HttpStatus` Enum을 활용하거나, `@ResponseStatus` 어노테이션을 이용할 수 있습니다. 이러한 방법들을 알고 있으면 더 효과적으로 웹 애플리케이션을 개발할 수 있습니다.