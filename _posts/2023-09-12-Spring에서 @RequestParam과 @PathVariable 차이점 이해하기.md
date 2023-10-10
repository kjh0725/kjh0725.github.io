---
title: Spring에서 RequestParam과 PathVariable 차이점 이해하기
date: 2023-09-12 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - RequestParam
  - PathVariable
---
## 소개
Spring Framework에서 웹 애플리케이션을 개발하면서 클라이언트로부터 데이터를 받기 위해 여러 방법을 사용할 수 있습니다. 이 글에서는 `@RequestParam`과 `@PathVariable` 두 가지 어노테이션의 차이점과 적절한 사용 시나리오에 대해 상세히 설명하겠습니다.

## `@RequestParam`의 특징과 활용법
`@RequestParam` 어노테이션은 주로 쿼리 파라미터를 처리할 때 사용합니다. 쿼리 파라미터란 URL의 끝에 `?` 다음에 오는 키-값 쌍입니다. 예를 들어, `/search?keyword=apple`에서 `keyword`가 키고, `apple`이 값입니다.

### 예시 코드
```java
@RequestMapping("/search")
public String search(@RequestParam String keyword) {
  // 로직 구현
  return "result";
}
```

### 주의사항
- 필수 파라미터가 누락될 경우 `400 Bad Request` 에러가 발생합니다.
- 옵션 설정으로 필수가 아니게 설정할 수 있습니다.

## `@PathVariable`의 특징과 활용법
`@PathVariable`은 URL의 일부를 변수로 사용할 때 적용합니다. URL에서 `/`로 구분된 부분 중 원하는 값을 추출하여 사용합니다.

### 예시 코드
```java
@RequestMapping("/users/{userId}")
public String getUser(@PathVariable String userId) {
  // 로직 구현
  return "userProfile";
}
```

### 주의사항
- `{userId}` 부분은 반드시 URL에 있어야 합니다.
- 없을 경우 `404 Not Found` 에러가 발생합니다.

## 언제 무엇을 사용해야 하는가?
- `@RequestParam`은 검색, 필터링, 정렬과 같이 옵션이 있는 데이터를 다룰 때 유용합니다.
- `@PathVariable`은 RESTful API에서 자주 볼 수 있으며, 특정 리소스에 접근할 때 사용합니다.

## 결론
`@RequestParam`과 `@PathVariable`은 Spring에서 클라이언트로부터 데이터를 받는 방식에 따라 적절히 사용해야 합니다. 필요에 따라 두 어노테이션을 혼합해서 사용하는 것도 가능합니다. 어떤 상황에서 어떤 어노테이션을 사용할지 정확히 알고, 적절히 활용하면 더 효율적인 웹 애플리케이션을 개발할 수 있습니다.