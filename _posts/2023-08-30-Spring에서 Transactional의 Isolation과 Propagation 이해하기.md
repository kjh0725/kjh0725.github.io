---
title: Spring에서 Transactional의 Isolation과 Propagation 이해하기
date: 2023-08-30 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - transcational
  - Isolation
---
## Isolation(고립성)이란 무엇인가

Isolation은 데이터베이스 트랜잭션에서 한 트랜잭션이 다른 트랜잭션에 영향을 주지 않도록 보장하는 성질입니다. 이를 통해 여러 트랜잭션이 동시에 실행될 때 문제가 발생하지 않도록 합니다. Spring에서는 `@Transactional` 애너테이션을 사용해 Isolation 레벨을 설정할 수 있습니다.

## Propagation(전파) 정의와 종류

Propagation은 트랜잭션이 어떻게 전파될 것인지를 정의합니다. Spring에서는 `REQUIRED`, `REQUIRES_NEW`, `NESTED` 등 여러 타입의 전파 옵션을 제공합니다.

- `REQUIRED`: 이미 존재하는 트랜잭션이 있다면 참여하고, 없다면 새로운 트랜잭션을 생성합니다.
- `REQUIRES_NEW`: 항상 새로운 트랜잭션을 생성합니다.
- `NESTED`: 이미 존재하는 트랜잭션이 있다면 중첩 트랜잭션을 생성합니다.

## `@Transactional`에서 Isolation과 Propagation 설정하기

Spring에서는 `@Transactional` 애너테이션을 사용하여 트랜잭션의 Isolation과 Propagation을 설정할 수 있습니다. 예를 들어, 아래와 같이 설정할 수 있습니다.

```java
@Transactional(isolation = Isolation.SERIALIZABLE, propagation = Propagation.REQUIRED)
public void myMethod() {
  // ... 코드 구현
}
```

## 자주 발생하는 오류와 해결법

### `Could not open JPA EntityManager for transaction`

이 오류는 JPA EntityManager가 트랜잭션을 위해 열리지 않았을 때 발생합니다. 이 문제를 해결하기 위해선 데이터베이스와의 연결을 확인해야 할 수도 있습니다.

### `Deadlock found when trying to get lock`

이 오류는 두 트랜잭션이 서로의 자원을 기다리며 무한 대기 상태에 빠질 때 발생합니다. 이를 해결하기 위해서는 트랜잭션의 실행 순서를 잘 조절해야 합니다.

## 정리

Isolation과 Propagation은 데이터베이스 트랜잭션을 안전하고 효과적으로 관리하기 위한 중요한 설정입니다. Spring에서는 `@Transactional` 애너테이션을 통해 이러한 세부 사항을 쉽게 설정할 수 있습니다. 여러 옵션을 이해하고 올바르게 적용하면 데이터의 일관성과 효율성을 높일 수 있습니다.