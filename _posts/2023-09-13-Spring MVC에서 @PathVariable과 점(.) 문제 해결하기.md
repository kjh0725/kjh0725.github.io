---
title: Spring MVC에서 @PathVariable과 점(.) 문제 해결하기
date: 2023-09-13 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringMVC
  - PathVariable
---
## 문제 상황: 점(.)이 잘리는 현상

Spring MVC에서 URL 경로에 있는 변수를 가져오기 위해 `@PathVariable` 어노테이션을 사용할 때, 점(.)을 포함한 변수가 잘려 나오는 문제가 있습니다. 특히, 파일 확장자와 같은 데이터를 처리하려고 할 때 이 문제가 발생할 가능성이 높습니다. 예를 들어, `/files/myfile.txt` 같은 URL에서 `myfile.txt`를 전체로 가져오려고 하면 `myfile`만 가져오게 됩니다. 이 문제의 에러 이름은 "PathVariable with dot is getting truncated".

## 원인: Spring 설정의 디폴트 값

Spring MVC는 기본적으로 URL에서 마지막 `.` 이후의 문자열을 잘라버립니다. 이는 파일 확장자를 제거하기 위한 Spring의 기본 설정 때문입니다. 이러한 동작은 특히 RESTful API를 구성할 때 문제가 될 수 있습니다.

## 해결 방법 1: 정규식을 이용한 설정 변경

`@RequestMapping` 어노테이션 내에서 정규식을 사용하여 이 문제를 해결할 수 있습니다.

```java
@RequestMapping(value = "/files/{fileName:.+}")
public String handleFile(@PathVariable("fileName") String fileName) {
  // 로직
}
```

`.+` 정규식은 하나 이상의 어떤 문자라도 매치되도록 합니다. 이렇게 하면 점(.)과 그 뒤에 오는 문자들도 포함해서 `fileName` 변수에 저장됩니다.

## 해결 방법 2: web.xml 설정 변경

`web.xml` 파일에서 다음과 같이 설정을 변경할 수도 있습니다.

```xml
<servlet-mapping>
  <servlet-name>dispatcher</servlet-name>
  <url-pattern>/</url-pattern>
  <url-pattern>*.do</url-pattern>
</servlet-mapping>
```

이 설정은 `.do` 확장자를 가진 URL만 Dispatcher Servlet에 매핑하도록 합니다. 그러면 다른 확장자를 가진 URL은 문제없이 처리될 수 있습니다.

## 결론: 설정을 통한 문제 해결

Spring MVC에서 `@PathVariable`과 점(.)을 함께 사용하면서 발생하는 문제는 적절한 설정과 정규식을 이용하여 해결할 수 있습니다. 위의 두 가지 방법 중 하나를 선택하여 적용하면, URL의 점(.) 이후의 문자들이 잘리는 문제를 해결할 수 있습니다. 이렇게 하면 파일 확장자나 다른 중요한 데이터도 누락되지 않고 안전하게 처리할 수 있습니다.