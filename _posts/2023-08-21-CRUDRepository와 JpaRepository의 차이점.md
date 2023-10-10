---
title: CRUDRepository와 JpaRepository의 차이점
date: 2023-08-21 20:00:00 +0900
categories:
  - Spring
tags:
  - CRUDRepository
  - JpaRepository
  - Spring
---
## 서론: Spring Data JPA 인터페이스에 대한 이해

Spring Data JPA는 Java 프로그래밍에서 데이터베이스 연결을 쉽게 해주는 프레임워크입니다. 이 프레임워크를 사용하면서, 개발자들은 종종 `CRUDRepository`와 `JpaRepository`라는 두 가지 인터페이스에 직면하게 됩니다. 이 두 인터페이스는 무엇이고 어떤 차이점이 있는지 알아보겠습니다.

## CRUDRepository: 기본적인 데이터 작업을 위한 인터페이스

`CRUDRepository`는 Spring Data JPA에서 가장 기본적인 인터페이스입니다. 이 인터페이스를 상속받아 사용하면, Create(생성), Read(읽기), Update(업데이트), Delete(삭제)와 같은 기본적인 데이터베이스 작업을 수행할 수 있습니다. `CRUDRepository`는 제네릭 인터페이스로, 두 개의 타입 파라미터가 필요합니다.

1. **엔터티 타입**: 데이터베이스 테이블에 매핑되는 Java 클래스
2. **ID 타입**: 엔터티의 식별자 타입, 즉 키값

## JpaRepository: JPA 특화 인터페이스

`JpaRepository`는 `CRUDRepository`를 상속받은 인터페이스입니다. 따라서 `CRUDRepository`의 모든 기능을 포함하며, 그 위에 JPA(Java Persistence API)의 추가적인 기능을 제공합니다. 예를 들어, 페이징과 정렬, 더 복잡한 쿼리를 실행할 수 있는 메서드가 추가적으로 제공됩니다.

## 주요 차이점

1. **기능의 확장성**: `JpaRepository`는 `CRUDRepository`에 비해 풍부한 기능을 제공합니다.
2. **쿼리 메서드**: `JpaRepository`는 JPA 특화 쿼리 메서드를 사용할 수 있습니다.
3. **구현체**: 두 인터페이스는 서로 다른 구현체를 가집니다. `SimpleJpaRepository`는 `JpaRepository`의 기본 구현체입니다.

## 결론: 어떤 것을 선택할까?

데이터 작업이 간단하고 JPA의 추가 기능이 필요 없다면 `CRUDRepository`를 사용하세요. 반면, JPA의 고급 기능이 필요하거나 이미 JPA를 사용하고 있다면 `JpaRepository`를 사용하는 것이 좋습니다.

이 글을 통해 `CRUDRepository`와 `JpaRepository`의 기본적인 개념과 차이점을 이해할 수 있을 것이라고 생각합니다. 이는 Java 및 Spring Data JPA 개발에서 중요한 지식입니다.