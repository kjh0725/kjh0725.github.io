---
title: Spring에서 여러 RequestMapping 어노테이션 사용하기
date: 2023-10-01 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - RequestMapping
---
## 서론: Spring Framework와 RequestMapping

Spring Framework는 자바 기반 웹 애플리케이션 개발을 위한 통합 프레임워크입니다. 이 프레임워크에서는 `@RequestMapping`이라는 어노테이션을 이용하여 HTTP 요청을 자바 메서드에 매핑할 수 있습니다. 즉, 웹에서 특정 URL을 호출했을 때 어떤 메서드가 실행될지 결정하는 역할을 합니다.

## 여러 RequestMapping 사용 방법

### 클래스 레벨에서의 사용
클래스 레벨에서 `@RequestMapping`을 사용하면 해당 클래스에 있는 모든 메서드에 공통된 경로(prefix)를 지정할 수 있습니다. 예를 들어, `/api`라는 공통된 경로를 설정하면, 그 아래의 메서드들은 `/api/xxx`, `/api/yyy` 등으로 접근 가능합니다.

```java
@RestController
@RequestMapping("/api")
public class MyController {
  // 클래스 레벨에서 "/api" 경로 설정
}
```

### 메서드 레벨에서의 사용
메서드 레벨에서는 각각의 메서드에 `@RequestMapping`을 붙여 다양한 URL과 HTTP 메서드를 지정할 수 있습니다. 예를 들어, `GET /api/users` 요청과 `POST /api/users` 요청을 다르게 처리하려면 다음과 같이 할 수 있습니다.

```java
@RequestMapping(value = "/users", method = RequestMethod.GET)
public String getUsers() {
  // GET 요청 처리
}

@RequestMapping(value = "/users", method = RequestMethod.POST)
public String createUser() {
  // POST 요청 처리
}
```

### 조합하여 사용하기
클래스 레벨과 메서드 레벨의 `@RequestMapping`을 함께 사용하면 더욱 다양한 URL 패턴을 표현할 수 있습니다.

```java
@RestController
@RequestMapping("/api")
public class MyController {
  
  @RequestMapping(value = "/users", method = RequestMethod.GET)
  public String getUsers() {
    // GET /api/users
  }

  @RequestMapping(value = "/users", method = RequestMethod.POST)
  public String createUser() {
    // POST /api/users
  }
}
```

## 주의사항: Ambiguous Mapping Error

클래스나 메서드에서 동일한 URL 패턴을 중복으로 지정하면 `Ambiguous Mapping Error`가 발생합니다. 이 오류는 두 개 이상의 메서드나 클래스가 같은 URL을 처리하려고 할 때 발생하므로, URL 패턴을 명확하게 구분해야 합니다.

## 결론: 효율적인 URL 매핑을 위한 최적의 전략

Spring에서는 `@RequestMapping` 어노테이션을 통해 다양한 URL 패턴과 HTTP 메서드를 유연하게 지정할 수 있습니다. 클래스 레벨과 메서드 레벨에서 적절하게 조합하여 사용하면, 더욱 효율적인 URL 매핑 전략을 구축할 수 있습니다. 하지만 이때 중복되는 URL 패턴을 피하고 명확한 구조를 유지하는 것이 중요합니다.