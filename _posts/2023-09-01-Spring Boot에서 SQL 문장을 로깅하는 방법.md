---
title: Spring Boot에서 SQL 문장을 로깅하는 방법
date: 2023-09-01 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - SQL
---
## 개요

Spring Boot를 사용하다 보면 데이터베이스와의 상호작용을 추적하고 싶을 때가 많습니다. 이 글에서는 Spring Boot에서 SQL 문장을 로깅하는 방법에 대해 자세히 알아보겠습니다.

## 로깅 레벨 설정하기

먼저, `application.properties` 또는 `application.yml` 파일에 로깅 레벨(logging level)을 설정해야 합니다. 로깅 레벨이란 로그의 상세성을 결정하는 설정입니다.

```
logging.level.org.hibernate.SQL=DEBUG
```

이 설정은 Hibernate(하이버네이트)라는 JPA 구현체가 실행하는 SQL 문장을 디버그 레벨로 출력하도록 합니다.

## 로깅 포맷 조정하기

추가적으로 SQL 로그의 형식을 좀 더 가독성 있게 만들고 싶다면, 다음과 같은 설정을 추가할 수 있습니다.

```
logging.level.org.hibernate.type.descriptor.sql=trace
```

이 설정은 SQL 문장에 사용된 파라미터의 값도 함께 로깅합니다. 'trace'는 로깅 레벨 중에서 가장 상세한 정보를 제공합니다.

## 스프링 부트 로거 사용하기

Spring Boot는 자체적으로 로거를 가지고 있습니다. 이를 사용하여 SQL 로깅을 활성화할 수도 있습니다.

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class YourClass {
    Logger logger = LoggerFactory.getLogger(YourClass.class);

    public void yourMethod() {
        logger.debug("Your SQL statement");
    }
}
```

이렇게 하면, `YourClass`에서 SQL 문장이 실행될 때 로그를 출력할 수 있습니다.

## 주의사항

SQL 로깅은 성능에 영향을 줄 수 있으므로, 개발 환경에서만 활성화하는 것이 좋습니다. 또한, 로깅 설정은 애플리케이션을 재시작할 때 적용됩니다.

## 결론

Spring Boot에서 SQL 로깅을 설정하는 것은 복잡하지 않습니다. `application.properties` 파일에 몇 가지 설정을 추가하고 필요한 경우 Java 코드에서 로거를 사용하여 SQL 로깅을 쉽게 할 수 있습니다. 이를 통해 데이터베이스와의 상호작용을 효과적으로 모니터링할 수 있습니다.