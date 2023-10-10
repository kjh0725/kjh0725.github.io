---
title: Spring Security에서 Role과 GrantedAuthority의 차이점
date: 2023-09-22 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringSecurity
  - Role
  - GrantedAuthority
---
## 소개
Spring Security는 자바 기반의 웹 어플리케이션에서 보안을 담당하는 프레임워크입니다. 보안이란 사용자 인증(Authentication)과 권한 부여(Authorization)을 의미하며, 이 두 요소를 관리하기 위해 Spring Security에서는 `Role`과 `GrantedAuthority`라는 두 가지 중요한 개념을 사용합니다.

## Role이란?
Role은 사용자의 역할을 나타내는 정보입니다. 예를 들어, "관리자", "사용자", "게스트" 등의 역할이 있을 수 있습니다. 일반적으로 Role은 특정 권한의 집합을 의미하며, 이를 통해 사용자에게 어떤 작업을 할 수 있는지를 결정합니다.

## GrantedAuthority란?
`GrantedAuthority`는 사용자에게 부여된 권한을 나타냅니다. 이는 보통 문자열로 표현되며, 특정 작업을 수행할 수 있는 권한을 의미합니다. 예를 들어, 파일을 읽을 수 있는 권한, 데이터를 수정할 수 있는 권한 등이 있습니다.

## Role과 GrantedAuthority의 차이점
1. **용도**: Role은 사용자의 역할을, GrantedAuthority는 특정 작업을 할 수 있는 권한을 나타냅니다.
2. **복잡성**: Role은 여러 권한을 묶은 것이므로 복잡성이 더 높습니다.
3. **표현 방식**: Spring Security에서는 Role은 보통 `"ROLE_"` 접두사를 붙여 표현하며, GrantedAuthority는 접두사 없이 표현합니다.
4. **데이터 구조**: Role은 일반적으로 데이터베이스의 별도 테이블에 저장되는 경우가 많고, GrantedAuthority는 메모리나 세션에 저장될 수 있습니다.

## 정리
Spring Security에서 Role과 GrantedAuthority는 보안을 관리하기 위한 중요한 구성 요소입니다. Role은 사용자의 역할을 나타내고, 복잡한 권한을 관리하는 데 유용하며, GrantedAuthority는 특정 작업에 대한 접근 권한을 제어합니다. 이 두 개념을 이해하고 적절히 활용하면 웹 어플리케이션의 보안을 효과적으로 관리할 수 있습니다.