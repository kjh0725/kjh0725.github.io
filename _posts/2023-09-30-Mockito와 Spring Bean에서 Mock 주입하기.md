---
title: Mockito와 Spring Bean에서 Mock 주입하기
date: 2023-09-30 20:00:00 +0900
categories:
  - Spring
tags:
  - Mockito
  - SpringBean
---
# Mockito와 Spring Bean에서 Mock 주입하기

## Mock이란 무엇인가?

Mock은 실제 객체를 흉내 내는 가짜 객체입니다. 테스트에서 외부 시스템이나 복잡한 로직 없이 특정 객체의 기능만을 검사하기 위해 사용됩니다. Mockito는 Java에서 널리 사용되는 Mocking 프레임워크 중 하나입니다.

## Spring Framework에서의 Bean

Spring Framework에서 Bean은 객체를 의미하며, Spring 컨테이너에 의해 관리됩니다. 이러한 Bean은 다양한 설정과 라이프사이클을 가질 수 있습니다.

## Mock 객체를 Spring Bean에 주입하는 방법

Spring과 Mockito를 함께 사용할 때 종종 Mock 객체를 Spring Bean에 주입해야 하는 경우가 있습니다. 이를 위한 몇 가지 방법이 있습니다:

### 1. `@MockBean` 애노테이션 사용
Spring Boot에서 제공하는 `@MockBean` 애노테이션을 사용하면 Spring 컨텍스트에 Mock 객체를 자동으로 주입할 수 있습니다.

```java
@RunWith(SpringRunner.class)
public class SomeServiceTest {

    @MockBean
    private SomeDependency someDependency;
    
    // 테스트 코드
}
```

### 2. `@Autowired`와 함께 사용
`@Autowired` 애노테이션과 함께 Mock 객체를 직접 생성하고 주입할 수 있습니다.

```java
@RunWith(SpringRunner.class)
public class SomeServiceTest {

    @Autowired
    private SomeService someService;

    @Before
    public void setup() {
        SomeDependency someDependency = Mockito.mock(SomeDependency.class);
        ReflectionTestUtils.setField(someService, "someDependency", someDependency);
    }
    
    // 테스트 코드
}
```

### 3. Java 설정 파일 사용
Java 설정 파일을 사용하여 빈을 명시적으로 설정할 수 있습니다.

```java
@Configuration
public class TestConfig {

    @Bean
    public SomeDependency createMock() {
        return Mockito.mock(SomeDependency.class);
    }
}
```

각 방법은 특정 상황과 요구 사항에 따라 유용할 수 있습니다. 이렇게 하면 Spring과 Mockito를 더 효과적으로 활용하여 견고한 테스트 코드를 작성할 수 있습니다.