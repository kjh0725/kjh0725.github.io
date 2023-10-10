---
title: Spring Bean 속성 주입 방법
date: 2023-09-28 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - bean
---
## XML 구성을 이용한 Spring Bean 설정

Spring Framework에서 Bean을 설정하는 방법 중 하나는 XML 파일을 이용하는 것입니다. XML 파일에 `<bean>` 태그를 사용하여 Bean의 클래스와 속성을 정의할 수 있습니다. 그러나 때로는 동적으로 또는 프로그래밍 방식으로 Bean의 속성을 변경해야 할 경우도 있습니다. 이러한 경우에 어떻게 해야 할까요?

## Property Placeholder를 활용한 속성 주입

Spring Framework에서는 `PropertyPlaceholderConfigurer` 또는 `PropertySourcesPlaceholderConfigurer` 클래스를 사용하여 외부 프로퍼티 파일로부터 Bean에 속성을 주입할 수 있습니다. 이 클래스들은 `${...}` 형식의 플레이스홀더를 Bean 속성 값으로 대체합니다.

```xml
<bean class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
    <property name="locations">
        <value>classpath:application.properties</value>
    </property>
</bean>

<bean id="myBean" class="com.example.MyBean">
    <property name="someProperty" value="${someValue}" />
</bean>
```

위의 예제에서 `someProperty`는 `application.properties` 파일에 정의된 `someValue`로 대체됩니다.

## `@Value` 어노테이션을 이용한 속성 주입

`@Value` 어노테이션은 Java 클래스 내에서 직접 속성을 주입할 수 있게 해주는 Spring 어노테이션입니다. 이를 사용하면 XML 구성 없이도 속성을 주입할 수 있습니다.

```java
@Component
public class MyBean {
    @Value("${someValue}")
    private String someProperty;

    // ...
}
```

여기에서 `someValue`는 외부 프로퍼티 파일이나 환경 변수에서 가져온 값이 될 것입니다.

## 오류 처리: `BeanDefinitionStoreException`

때로는 속성 파일이나 환경 변수에서 `someValue` 같은 키가 찾을 수 없을 경우 `BeanDefinitionStoreException`이 발생할 수 있습니다. 이런 경우, Spring 구성을 검토하거나 해당 키가 올바르게 정의되어 있는지 확인해야 합니다.

## 결론

Spring Framework에서는 여러 가지 방법으로 Bean 속성을 동적으로 주입할 수 있습니다. `PropertyPlaceholderConfigurer`, `PropertySourcesPlaceholderConfigurer`, 그리고 `@Value` 어노테이션은 이러한 작업을 쉽고 효율적으로 수행할 수 있는 도구입니다. 이를 통해 더 유연하고 관리하기 쉬운 애플리케이션을 구축할 수 있습니다.