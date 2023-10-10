---
title: Spring에서 Component와 Bean의 차이
date: 2023-08-26 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - Component
  - bean
---
## Component와 Bean의 정의

Spring Framework에서 "Component"와 "Bean"은 빈 컨테이너에 등록되는 객체를 지칭합니다. 하지만 둘 사이에는 미묘한 차이가 있습니다. `@Component` 어노테이션은 클래스에 붙여서 그 클래스의 객체를 자동으로 빈으로 등록하는 것입니다. 반면 `@Bean`은 메소드에 붙이며, 해당 메소드의 반환 값이 빈이 됩니다.

## Component의 사용법과 장점

`@Component`는 클래스 레벨에서 사용됩니다. 이것을 붙인 클래스는 Spring이 자동으로 Bean으로 관리해줍니다. 이 방법의 장점은 설정이 단순하고 직관적이라는 것입니다.

```java
@Component
public class MyComponent {
    // ...
}
```

위와 같이 코드에 `@Component`를 붙이면 Spring이 이를 인식하고 빈으로 등록합니다.

## Bean의 사용법과 장점

`@Bean`은 메소드 레벨에서 사용되며, 보통 `@Configuration` 클래스 내부에 위치합니다. `@Bean`을 사용할 때의 장점은 빈의 생성 과정을 상세하게 제어할 수 있다는 것입니다.

```java
@Configuration
public class MyConfig {
    @Bean
    public MyClass myClass() {
        return new MyClass();
    }
}
```

여기서 `MyClass` 타입의 빈을 생성하고 있습니다. 이런 방식으로 빈을 등록하면 메소드 안에서 빈의 초기화 과정 등을 더 세밀하게 제어할 수 있습니다.

## 둘 사이의 주된 차이점

1. **어노테이션 위치**: `@Component`는 클래스에, `@Bean`은 메소드에 사용됩니다.
2. **제어 레벨**: `@Bean`은 빈의 생성과 초기화 등을 더 세밀하게 제어할 수 있습니다.

## 언제 무엇을 사용할까?

- 간단한 빈 등록만 필요하면 `@Component`를 사용하세요.
- 빈의 생성 과정에 특별한 로직이 필요하면 `@Bean`을 사용하세요.

이상으로 `@Component`와 `@Bean`의 차이점과 사용 시점에 대해서 알아보았습니다. 두 방법은 상황에 따라 적절히 활용하면 됩니다.