---
title: Spring에서 ContextConfiguration과 ContextComponentScan의 차이점
date: 2023-08-25 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - ContextConfiguration
  - ContextComponentScan
---
## 무엇이 다른가요?

Spring 프레임워크에서는 테스트 환경을 구성할 때 사용하는 여러 어노테이션들이 있습니다. 이 중에서도 `@ContextConfiguration`과 `@ContextComponentScan`은 비슷해 보이지만 명확한 차이점을 가지고 있습니다. 이 두 어노테이션은 컨텍스트 설정과 관련된 작업을 할 때 주로 사용되지만, 사용 목적과 방법이 다릅니다.

## @ContextConfiguration의 역할

`@ContextConfiguration` 어노테이션은 Spring 테스트 컨텍스트 프레임워크를 위한 설정 클래스나 설정 파일을 지정하는 데 사용됩니다. 예를 들어, XML 파일이나 Java 설정 클래스를 이 어노테이션을 통해 로드할 수 있습니다.

```java
@ContextConfiguration(locations = "classpath:/applicationContext.xml")
```
또는

```java
@ContextConfiguration(classes = AppConfig.class)
```

이렇게 사용하면 테스트 실행 시 지정한 설정을 로드하여 사용합니다.

## @ContextComponentScan의 역할

`@ContextComponentScan`은 존재하지 않는 어노테이션입니다. 일반적으로 사용되는 것은 `@ComponentScan`이며, 이것은 주로 Spring 애플리케이션의 메인 설정 클래스에서 사용됩니다. `@ComponentScan`은 지정한 패키지 내에서 Spring 컴포넌트를 스캔하여 빈으로 등록하는 역할을 합니다.

```java
@ComponentScan(basePackages = "com.example")
```

이렇게 사용하면 `com.example` 패키지와 그 하위 패키지에서 `@Component`, `@Service`, `@Repository` 등의 어노테이션이 붙은 클래스를 찾아 빈으로 등록합니다.

## 주요 차이점

1. **설정 로드 vs 컴포넌트 스캔**: `@ContextConfiguration`은 테스트 설정을 로드하는 데 사용되며, `@ComponentScan`은 빈을 찾아 등록하는 데 사용됩니다.
2. **사용 범위**: `@ContextConfiguration`은 테스트 클래스에서 주로 사용되며, `@ComponentScan`은 메인 설정 클래스에서 주로 사용됩니다.

## 결론

`@ContextConfiguration`과 `@ComponentScan`은 비슷해 보이지만, 각각 다른 목적과 사용 케이스에 적합하므로 주의 깊게 선택하여 사용해야 합니다.