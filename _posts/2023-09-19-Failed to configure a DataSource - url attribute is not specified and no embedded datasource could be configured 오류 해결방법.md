---
title: Failed to configure a DataSource - url attribute is not specified and no embedded datasource could be configured 오류 해결방법
date: 2023-09-19 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 오류 개요

Spring Boot 프로젝트에서 데이터베이스와 연동을 하려고 할 때, 다음과 같은 오류 메시지가 나타나는 경우가 있습니다.

```
Failed to configure a DataSource: 'url' attribute is not specified and no embedded datasource could be configured
```

이 오류는 일반적으로 `application.properties` 또는 `application.yml` 파일에 데이터베이스 연결 정보가 올바르게 설정되지 않았을 때 발생합니다.

## 원인 파악

Spring Boot는 데이터베이스 연결을 위해 `DataSource` 객체를 설정하려고 시도합니다. 이 설정 정보는 `application.properties` 또는 `application.yml` 파일에서 가져오는데, 이 파일에 필요한 정보가 누락되거나 잘못되었을 경우 위의 오류가 발생합니다.

### 필요한 속성들

- `spring.datasource.url`: 실제 데이터베이스의 위치(URL)
- `spring.datasource.username`: 데이터베이스 접속 사용자 이름
- `spring.datasource.password`: 데이터베이스 접속 비밀번호
- `spring.datasource.driver-class-name`: JDBC 드라이버 클래스 이름 (예: `com.mysql.cj.jdbc.Driver`)

## 해결 방법

### `application.properties` 파일 수정

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/your_database
spring.datasource.username=your_username
spring.datasource.password=your_password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

### `application.yml` 파일 수정

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/your_database
    username: your_username
    password: your_password
    driver-class-name: com.mysql.cj.jdbc.Driver
```

이렇게 설정 파일을 수정하면, 'Failed to configure a DataSource: 'url' attribute is not specified and no embedded datasource could be configured' 오류를 해결할 수 있습니다.

## 추가 팁

만약 `H2` 같은 내장 데이터베이스를 사용한다면, `spring.datasource.url`과 같은 설정은 생략 가능합니다. 이 경우에는 Spring Boot가 자동으로 내장 데이터베이스를 구성합니다.

## 결론

Spring Boot에서 'Failed to configure a DataSource: 'url' attribute is not specified and no embedded datasource could be configured' 오류는 주로 데이터베이스 연결 정보의 누락이나 오류 때문에 발생합니다. `application.properties` 또는 `application.yml` 파일을 정확하게 설정함으로써 이 문제를 쉽게 해결할 수 있습니다.