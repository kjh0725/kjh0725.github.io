---
title: Spring Boot 초기 데이터 로딩 방법
date: 2023-10-02 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - 초기데이터
---
## 문제 개요

Spring Boot 프로젝트를 시작할 때 초기 데이터를 로딩해야 하는 상황이 있다. 이 데이터는 데이터베이스에 저장되어 있는 정보가 될 수도 있고, 설정 파일이나 다른 외부 리소스에서 가져올 수도 있다. 이 글에서는 여러 방법으로 Spring Boot에서 초기 데이터를 로딩하는 방법에 대해 자세히 알아본다.

## `ApplicationRunner`와 `CommandLineRunner` 활용하기

Spring Boot에서 제공하는 `ApplicationRunner` 또는 `CommandLineRunner` 인터페이스를 구현할 수 있다. 이들 인터페이스의 `run` 메서드 내에서 초기 데이터 로딩 로직을 작성하면 애플리케이션 시작 시 자동으로 실행된다.

```java
@Component
public class DataLoader implements CommandLineRunner {
    @Override
    public void run(String... args) {
        // 초기 데이터 로딩 로직
    }
}
```

## `@PostConstruct` 어노테이션 사용하기

`@PostConstruct` 어노테이션은 Spring 빈이 생성된 후에 실행되는 메서드에 붙일 수 있다. 이 방법을 사용하면, 빈이 초기화된 후에 데이터 로딩 작업을 할 수 있다.

```java
@Component
public class DataLoader {
    @PostConstruct
    public void loadData() {
        // 초기 데이터 로딩 로직
    }
}
```

## 데이터베이스 마이그레이션 도구 활용하기

Flyway나 Liquibase 같은 데이터베이스 마이그레이션 도구를 사용하여 초기 데이터를 로딩할 수 있다. `db/migration` 폴더 내에 SQL 스크립트를 작성하여 애플리케이션 시작 시 자동으로 실행되도록 설정할 수 있다.

## `import.sql` 파일 사용하기

JPA(Hibernate)를 사용하는 경우, `src/main/resources` 디렉터리에 `import.sql` 파일을 생성하여 SQL 쿼리를 작성할 수 있다. 애플리케이션 시작 시 `import.sql` 내의 쿼리가 자동으로 실행된다.

## 정리

Spring Boot에서 초기 데이터를 로딩하는 방법은 다양하다. 프로젝트의 필요에 따라 가장 적합한 방법을 선택하여 구현하면 된다. 각 방법은 그 자체로 완전하므로, 복잡한 로직 없이도 초기 데이터를 효과적으로 로딩할 수 있다.