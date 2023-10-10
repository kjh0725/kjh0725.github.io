---
title: Spring Security에서 현재 사용자 이름 얻는 정확한 방법
date: 2023-09-29 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringSecurity
---
## Spring Security의 핵심 개념

Spring Security는 자바 웹 애플리케이션에서 보안을 제공하는 프레임워크입니다. 인증(Authentication)과 권한 부여(Authorization) 등을 쉽게 관리할 수 있게 해줍니다. '인증'이라는 단어는 사용자가 누구인지 확인하는 과정을 의미하고, '권한 부여'는 해당 사용자가 어떤 작업을 수행할 수 있는지를 결정하는 것입니다.

## 현재 사용자 정보 얻기

Spring Security를 사용할 때, 현재 사용자의 이름을 얻는 다양한 방법이 있습니다. 대표적으로 두 가지 방법을 소개하겠습니다.

### SecurityContextHolder를 사용하는 방법

이 방법은 가장 일반적으로 사용됩니다. `SecurityContextHolder`는 보안 컨텍스트(Security Context) 정보를 저장하고 있습니다. 다음은 예시 코드입니다.

```java
String username = SecurityContextHolder.getContext().getAuthentication().getName();
```

### @AuthenticationPrincipal 어노테이션을 사용하는 방법

이 방법은 컨트롤러 메서드의 파라미터로 `@AuthenticationPrincipal` 어노테이션을 사용합니다. 이렇게 하면 메서드 내에서 사용자 정보를 직접 사용할 수 있습니다.

```java
public String someMethod(@AuthenticationPrincipal UserDetails userDetails) {
  String username = userDetails.getUsername();
}
```

## 장단점 비교

- **SecurityContextHolder 방법**
  - **장점**: 어디에서나 쉽게 사용자 정보를 가져올 수 있습니다.
  - **단점**: 테스트하기 어렵고, 코드의 의존성이 높아질 수 있습니다.

- **@AuthenticationPrincipal 방법**
  - **장점**: 의존성이 낮고, 테스트하기 쉽습니다.
  - **단점**: 컨트롤러 메서드에서만 사용할 수 있습니다.

## 오류 처리

Spring Security 사용 중에 오류가 발생한다면, 대표적으로 `NullPointerException`이 발생할 수 있습니다. 이는 주로 `SecurityContextHolder`에서 `Authentication` 객체를 얻을 수 없을 때 나타납니다. 이 경우, 보안 설정을 다시 확인해야 합니다.

## 결론

Spring Security는 다양한 방법으로 현재 사용자의 정보를 얻을 수 있게 해줍니다. 각 방법에는 그에 맞는 장단점이 있으므로, 상황에 따라 적절한 방법을 선택하는 것이 중요합니다.