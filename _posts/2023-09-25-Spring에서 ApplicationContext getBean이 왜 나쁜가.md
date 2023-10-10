---
title: Spring에서 ApplicationContext getBean이 왜 나쁜가
date: 2023-09-25 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - ApplicationContext
  - getBean
---
## ApplicationContext와 getBean의 이해

먼저, Spring Framework에서 `ApplicationContext`는 모든 빈(bean)을 관리하는 중앙 저장소입니다. `getBean` 메서드는 이 저장소에서 특정 빈을 가져오는 기능을 합니다. 하지만 이 방법은 여러 가지 문제를 야기할 수 있습니다.

## 타입 안전성 문제

`getBean` 메서드를 사용할 때 가장 큰 문제는 타입 안전성(type safety)입니다. 타입 안전성이란 코드에서 예상한 데이터 타입과 실제 데이터 타입이 일치하는지를 확인하는 것입니다. `getBean`은 반환 타입을 명시적으로 알려주지 않기 때문에, 잘못된 타입으로 캐스팅(casting)할 위험이 있습니다.

## 의존성 주입의 위반

Spring은 의존성 주입(Dependency Injection, DI)을 권장하는데, `getBean`을 사용하면 이 원칙이 무시됩니다. 의존성 주입은 객체가 필요로 하는 의존성을 외부에서 주입해주는 디자인 패턴입니다. `getBean`을 사용하면 객체가 직접 의존성을 가져오게 되어, 코드의 유연성과 테스트 용이성이 떨어집니다.

## 코드 가독성 저하

`getBean`을 사용하면 코드 가독성이 떨어집니다. 이 메서드를 통해 빈을 가져오면, 어떤 빈이 필요한지 명확하게 파악하기 어려울 수 있습니다. 이로 인해 코드를 읽고 이해하는 데 시간이 더 걸릴 수 있습니다.

## 결론: 더 나은 대안 사용하기

`getBean` 대신에 의존성 주입을 활용하는 것이 더 나은 방법입니다. 이를 통해 타입 안전성을 보장하고, 코드의 유연성과 가독성을 높일 수 있습니다. 따라서 가능하면 `ApplicationContext.getBean` 사용을 피하고, Spring의 강력한 의존성 주입 기능을 활용해보세요.