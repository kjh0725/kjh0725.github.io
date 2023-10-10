---
title: Spring Data에서 findAll과 OrderBy 함께 사용하기
date: 2023-09-09 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringData
  - findAll
  - OrderBy
---
## 정렬 기능 이해하기

Spring Data JPA는 자바에서 데이터베이스 작업을 쉽게 할 수 있도록 도와주는 라이브러리입니다. 이 중에서도 `findAll`과 `OrderBy`를 같이 사용하려면 어떻게 해야 할까요? `findAll`은 모든 데이터를 가져오는 메서드이고, `OrderBy`는 그 데이터를 정렬하는 기능입니다.

## 메서드 명명 규칙

Spring Data JPA는 메서드 이름만으로 쿼리를 생성할 수 있는 강력한 기능을 제공합니다. 예를 들어, `findAllByOrderBy{필드명}Asc` 또는 `Desc`라는 이름의 메서드를 정의하면, 해당 필드를 기준으로 오름차순(Asc) 또는 내림차순(Desc)으로 데이터를 가져옵니다. 

```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findAllByOrderByNameAsc();
}
```

여기서 `User`는 엔터티 클래스, `Name`은 그 중에서 정렬하고 싶은 필드입니다.

## 정렬 파라미터 사용하기

또 다른 방법은 `Sort` 객체를 파라미터로 전달하는 것입니다. `findAll(Sort sort)` 형태로 사용하면 됩니다.

```java
Sort sort = Sort.by(Sort.Order.asc("name"));
List<User> users = userRepository.findAll(sort);
```

`Sort.by()` 메서드를 사용하여 정렬 조건을 명시적으로 지정할 수 있습니다.

## 정렬과 페이징

`Pageable` 객체를 사용하면, 페이징과 정렬을 동시에 할 수 있습니다. 

```java
Pageable pageable = PageRequest.of(0, 10, Sort.by("name").ascending());
Page<User> users = userRepository.findAll(pageable);
```

이렇게 하면, 이름으로 오름차순 정렬된 결과를 10개까지만 가져옵니다.

## 요약

Spring Data JPA를 사용하면 `findAll`과 `OrderBy`를 간편하게 사용할 수 있습니다. 메서드 명명 규칙을 따르거나, `Sort` 객체와 `Pageable` 객체를 파라미터로 사용하여 정렬과 페이징을 쉽게 구현할 수 있습니다.