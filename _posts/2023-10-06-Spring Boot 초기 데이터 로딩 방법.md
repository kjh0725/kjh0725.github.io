---
title: Spring Boot 초기 데이터 로딩 방법
date: 2023-10-06 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 문제 상황: Spring Boot에서 데이터 미리 로딩하기

Spring Boot를 사용할 때, 애플리케이션을 시작할 때 일부 데이터를 데이터베이스에 미리 로드하는 것이 필요할 수 있습니다. 이러한 초기 데이터 로딩은 테스트 환경 뿐만 아니라 실제 환경에서도 유용하게 사용될 수 있습니다. StackOverflow에 올라온 이 질문에서는 `ApplicationRunner`와 `CommandLineRunner`를 사용하는 방법을 다룹니다.

## ApplicationRunner 사용하기

`ApplicationRunner` 인터페이스를 구현하면, Spring Boot 애플리케이션 시작 시점에 로직을 실행할 수 있습니다. 예를 들어, 데이터베이스에 초기 데이터를 삽입할 수 있습니다.

```java
@Component
public class DataLoader implements ApplicationRunner {

    @Autowired
    private UserRepository userRepository;

    @Override
    public void run(ApplicationArguments args) {
        userRepository.save(new User("John", "Doe"));
        userRepository.save(new User("Jane", "Doe"));
    }
}
```

## CommandLineRunner 사용하기

`CommandLineRunner`도 마찬가지로 Spring Boot 애플리케이션 시작 시점에 로직을 실행합니다. 차이점은 `CommandLineRunner`는 문자열 배열을 파라미터로 받는다는 것입니다.

```java
@Component
public class DataLoader implements CommandLineRunner {

    @Autowired
    private UserRepository userRepository;

    @Override
    public void run(String... args) {
        userRepository.save(new User("John", "Doe"));
        userRepository.save(new User("Jane", "Doe"));
    }
}
```

## 어떤 것을 선택할까?

`ApplicationRunner`와 `CommandLineRunner` 둘 다 유사한 기능을 제공하지만, 입력 파라미터의 형태가 다릅니다. 특별한 이유가 없다면 두 가지 중 하나를 선택하여 사용하면 됩니다.

## 주의할 점

데이터 로딩 과정에서 발생할 수 있는 오류를 사전에 예방하기 위해서는 트랜잭션을 잘 관리해야 합니다. 또한, 이 과정에서 발생하는 예외를 잘 처리해야 애플리케이션의 안정성을 높일 수 있습니다.

## 결론

Spring Boot에서는 `ApplicationRunner` 또는 `CommandLineRunner`를 사용하여 애플리케이션 시작 시점에 데이터를 로딩할 수 있습니다. 이를 통해 테스트 환경이나 실제 환경에서 필요한 초기 설정을 쉽게 할 수 있습니다.