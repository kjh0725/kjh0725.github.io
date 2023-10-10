---
title: JSONMappingException 해결 방법
date: 2023-09-02 20:00:00 +0900
categories:
  - Spring
tags:
  - JSONMappingException
---
## 오류의 본질: No Suitable Constructor Found for Type

먼저, `JSONMappingException: No Suitable Constructor Found for Type` 오류가 어떤 상황에서 발생하는지 알아보겠습니다. 이 오류는 Java에서 Jackson 라이브러리를 사용하여 JSON을 객체로 변환할 때 나타납니다. 주로 이 오류는 대상 클래스에 기본 생성자가 없거나, 해당 생성자가 `private`로 선언되어 있을 때 발생합니다.

## 해결 방안 1: 기본 생성자 추가

가장 쉬운 해결 방법은 대상 클래스에 기본 생성자를 추가하는 것입니다. 기본 생성자란 매개변수가 없는 생성자를 의미합니다.

```java
public class MyClass {
    public MyClass() {
        // 기본 생성자
    }
}
```

## 해결 방안 2: @JsonCreator 애노테이션 사용

만약 기본 생성자를 추가할 수 없는 상황이라면, `@JsonCreator`와 `@JsonProperty` 애노테이션을 사용할 수 있습니다. 이 애노테이션은 Jackson 라이브러리에서 제공하며, 특정 생성자를 사용하여 JSON을 객체로 변환하는 방법을 명시합니다.

```java
public class MyClass {
    private final String myField;

    @JsonCreator
    public MyClass(@JsonProperty("myField") String myField) {
        this.myField = myField;
    }
}
```

## 해결 방안 3: @NoArgsConstructor 애노테이션 사용

Lombok 라이브러리를 사용하고 있다면, `@NoArgsConstructor` 애노테이션을 사용하여 기본 생성자를 자동으로 추가할 수 있습니다.

```java
@NoArgsConstructor
public class MyClass {
    private String myField;
}
```

이러한 해결 방안들을 통해 `JSONMappingException: No Suitable Constructor Found for Type` 오류를 효과적으로 해결할 수 있습니다. 여기서 중요한 것은 대상 클래스의 생성자 설정이 JSON 객체로의 변환과 어떻게 연관되는지 이해하는 것입니다.