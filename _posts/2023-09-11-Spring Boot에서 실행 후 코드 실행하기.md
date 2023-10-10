---
title: Spring Boot에서 실행 후 코드 실행하기
date: 2023-09-11 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 오류: 코드가 Spring Boot 앱 시작 후 실행되지 않음

대부분의 개발자가 처음으로 Spring Boot를 사용할 때 겪는 문제 중 하나는 애플리케이션이 시작한 뒤에 특정 코드를 실행시키는 것입니다. 이 문제에 대한 일반적인 질문은 `Running code after Spring Boot starts`라고 할 수 있습니다. 이 문제는 초기화 작업, 데이터베이스 연결 또는 사용자 정의 설정과 관련이 있을 수 있습니다.

## ApplicationContext와 ApplicationRunner, CommandLineRunner

Spring Boot에서 애플리케이션이 시작된 후 특정 코드를 실행시키는 방법은 여러 가지가 있지만, 주로 `ApplicationContext`를 사용하거나 `ApplicationRunner` 또는 `CommandLineRunner` 인터페이스를 구현합니다. 

### ApplicationContext 이용하기

`ApplicationContext`는 Spring 애플리케이션에서 컴포넌트들이 상호 작용하는 방법을 제어합니다. 이것을 사용하여 `ApplicationReadyEvent`라는 이벤트를 감지하고, 이 이벤트가 발생하면 원하는 코드를 실행할 수 있습니다.

```java
@Component
public class MyApplicationReadyEventListener implements ApplicationListener<ApplicationReadyEvent> {

    @Override
    public void onApplicationEvent(ApplicationReadyEvent event) {
        // 여기에 코드를 넣습니다.
    }
}
```

### ApplicationRunner 또는 CommandLineRunner 구현하기

`ApplicationRunner`와 `CommandLineRunner`는 Spring Boot에서 제공하는 인터페이스로, 애플리케이션 시작 후 실행되는 `run` 메소드를 가지고 있습니다.

```java
@Component
public class MyApplicationRunner implements ApplicationRunner {

    @Override
    public void run(ApplicationArguments args) {
        // 여기에 코드를 넣습니다.
    }
}
```

## 결론

Spring Boot 애플리케이션에서 초기화 작업이나 다른 코드를 실행하기 위해 `ApplicationContext`, `ApplicationRunner`, `CommandLineRunner` 중 하나를 선택할 수 있습니다. 각 방법에는 장단점이 있으므로, 애플리케이션의 요구 사항에 따라 적절한 방법을 선택하면 됩니다. 이렇게 하면 Spring Boot 애플리케이션에서 앱이 완전히 시작된 후에도 원하는 동작을 수행할 수 있습니다.