---
title: Spring RestTemplate GET 요청과 파라미터 다루기
date: 2023-09-15 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - RestTemplate
  - GET요청
---
## GET 요청의 기본 이해

`Spring`의 `RestTemplate`은 HTTP 호출을 위한 클래스입니다. 여기서는 `GET` 요청을 보낼 때 어떻게 URL 파라미터를 추가할 수 있는지 살펴봅니다. `GET` 요청은 웹 서버에 정보를 요청할 때 사용하는 가장 기본적인 HTTP 메소드입니다.

## URI Components Builder 사용
`UriComponentsBuilder`라는 클래스를 사용하면 URL을 효율적으로 생성할 수 있습니다. 이 클래스를 사용하면 파라미터를 쉽게 추가할 수 있으며, 이는 URL 생성 시 실수를 줄여줍니다.

```java
UriComponentsBuilder builder = UriComponentsBuilder.fromUriString(url)
  .queryParam("key1", value1)
  .queryParam("key2", value2);
```

이렇게 하면 `builder.toUriString()` 메소드를 통해 완성된 URL을 얻을 수 있습니다.

## getForObject 메소드 사용
`getForObject` 메소드는 URL과 반환할 객체의 클래스 타입을 인자로 받습니다. 이 메소드를 사용하면 HTTP GET 요청을 보내고, 응답을 객체로 변환할 수 있습니다.

```java
String result = restTemplate.getForObject(builder.toUriString(), String.class);
```

## 오류 처리: HttpStatusCodeException
코드 실행 중에 문제가 발생하면 `HttpStatusCodeException`이라는 예외가 발생할 수 있습니다. 이 예외는 서버에서 전달되는 HTTP 상태 코드를 담고 있어 어떤 문제인지 파악하기 쉽습니다.

## 정리
Spring의 RestTemplate은 HTTP 호출을 쉽게 만들어줍니다. GET 요청을 보낼 때 URL 파라미터를 추가하는 방법으로는 UriComponentsBuilder를 사용하거나 `getForObject` 메소드를 사용할 수 있습니다. 이러한 방법을 사용하면 서버와 효율적으로 데이터를 주고받을 수 있습니다.