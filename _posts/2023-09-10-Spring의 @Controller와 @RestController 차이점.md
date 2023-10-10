---
title: Spring의 @Controller와 @RestController 차이점
date: 2023-09-10 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - Controller
  - RestController
---
## 서론
Spring Framework에서는 웹 애플리케이션을 개발하기 위해 여러 어노테이션을 제공합니다. 이 중에서도 `@Controller`와 `@RestController`는 매우 중요한 역할을 합니다. 이 두 어노테이션은 비슷해 보이지만, 사실은 명확한 차이점이 있습니다. 이 글에서는 이 두 어노테이션의 차이점에 대해 자세히 알아보겠습니다.

## @Controller의 역할
`@Controller`는 Spring MVC에서 가장 기본적인 컨트롤러 어노테이션입니다. 이 어노테이션을 사용하면 클라이언트의 요청을 처리하고, 적절한 응답을 돌려줄 수 있습니다. 주로 HTML 페이지를 반환하는 웹 애플리케이션에서 사용됩니다.

### 예시 코드
```java
@Controller
public class MyController {
    @RequestMapping("/hello")
    public String hello(Model model) {
        model.addAttribute("message", "Hello, World!");
        return "hello";
    }
}
```

## @RestController의 특징
`@RestController`는 `@Controller`와 유사하지만, 주로 RESTful 웹 서비스를 개발할 때 사용됩니다. 이 어노테이션을 사용하면 리턴 타입에 따라 자동으로 JSON 혹은 XML과 같은 형식으로 변환됩니다.

### 예시 코드
```java
@RestController
public class MyRestController {
    @GetMapping("/hello")
    public Map<String, String> hello() {
        Map<String, String> result = new HashMap<>();
        result.put("message", "Hello, World!");
        return result;
    }
}
```

## 주요 차이점
1. **응답 형식**: `@Controller`는 주로 뷰 페이지를 반환하며, `@RestController`는 데이터를 반환합니다.
2. **어노테이션 조합**: `@Controller`는 `@ResponseBody`를 함께 사용하여 `@RestController`와 유사한 기능을 수행할 수 있습니다.
3. **용도**: `@Controller`는 HTML 기반의 웹 페이지를, `@RestController`는 RESTful API를 개발할 때 주로 사용됩니다.

## 결론
`@Controller`와 `@RestController`는 각각 다른 목적과 용도에 맞게 설계되었습니다. 알맞은 어노테이션을 선택하여 효율적인 웹 애플리케이션을 개발하면 됩니다. 이를 통해 개발자는 더 유연하고 확장성 있는 애플리케이션을 만들 수 있습니다.