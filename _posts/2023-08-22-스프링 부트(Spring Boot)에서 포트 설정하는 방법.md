---
title: 스프링 부트(Spring Boot)에서 포트 설정하는 방법
date: 2023-08-22 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 개요

스프링 부트는 웹 애플리케이션을 쉽게 개발할 수 있도록 도와주는 프레임워크입니다. 이러한 웹 애플리케이션은 특정 포트를 사용해야 하는데, 이 글에서는 스프링 부트에서 어떻게 포트를 설정하는지 상세하게 알려드립니다.

## `application.properties` 파일을 이용한 설정

스프링 부트 애플리케이션에서 가장 일반적으로 사용되는 포트 설정 방법은 `application.properties` 파일을 이용하는 것입니다. 이 파일은 `src/main/resources` 디렉토리에 위치합니다. 이 파일을 열고 다음과 같이 입력하면 됩니다.

```plaintext
server.port=8081
```

여기서 `8081`은 설정하려는 포트 번호입니다. 이 번호를 원하는 값으로 변경할 수 있습니다.

## 자바 코드로 포트 설정하기

프로그램 코드 내에서 포트를 동적으로 설정하려면 `SpringApplication.setDefaultProperties` 메서드를 사용할 수 있습니다. 이는 `main` 메서드에서 설정 가능합니다.

```java
public static void main(String[] args) {
    SpringApplication app = new SpringApplication(MyApplication.class);
    Map<String, Object> properties = new HashMap<>();
    properties.put("server.port", "8082");
    app.setDefaultProperties(properties);
    app.run(args);
}
```

이 방법을 사용하면 프로그램 실행 시점에서 포트를 설정할 수 있습니다. 

## 환경 변수를 이용한 설정

환경 변수(`Environment Variable`)를 통해 포트를 설정하는 것도 가능합니다. 이 방법은 클라우드 환경에서 유용하게 사용될 수 있습니다.

```shell
export SERVER_PORT=8083
```

환경 변수를 설정한 후에 스프링 부트 애플리케이션을 실행하면 설정한 포트로 애플리케이션을 실행할 수 있습니다.

## 요약

스프링 부트에서는 여러 가지 방법으로 포트를 설정할 수 있습니다. `application.properties` 파일 수정, 자바 코드에서의 설정, 환경 변수를 통한 설정 등 다양한 방법을 알아보았습니다. 이를 통해 원하는 포트에서 애플리케이션을 실행할 수 있습니다.