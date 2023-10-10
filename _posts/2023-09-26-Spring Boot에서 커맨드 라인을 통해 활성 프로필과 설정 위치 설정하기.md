---
title: Spring Boot에서 커맨드 라인을 통해 활성 프로필과 설정 위치 설정하기
date: 2023-09-26 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBott
---
## 오류명: N/A (해당 정보가 URL에 제공되지 않았습니다)

Spring Boot는 자바 기반의 웹 프레임워크로, 빠르고 쉽게 웹 애플리케이션을 개발할 수 있습니다. 이러한 개발 과정에서 환경 설정을 다루는 것이 중요한데, 특히 활성 프로필(Active Profile)과 설정 파일의 위치를 정의하는 방법에 대해 알아보겠습니다.

## 활성 프로필 설정 방법

활성 프로필은 실행 환경에 따라 다르게 적용할 설정들을 구분해 놓은 것입니다. 예를 들어 개발 환경과 배포 환경에서 데이터베이스의 정보가 다를 수 있습니다. 활성 프로필을 커맨드 라인에서 설정하기 위해서는 아래와 같은 명령어를 사용합니다.

```bash
java -jar your-app.jar --spring.profiles.active=prod
```

여기서 `prod`는 사용하고 싶은 프로필의 이름입니다.

## 설정 위치 설정 방법

설정 위치는 설정 파일(`application.properties`나 `application.yml`)이 저장된 위치를 말합니다. 이 위치를 커맨드 라인에서 지정하기 위해 아래의 명령어를 사용할 수 있습니다.

```bash
java -jar your-app.jar --spring.config.location=/your/path/
```

`/your/path/`는 설정 파일이 위치한 경로입니다.

## 둘 다 설정하는 방법

활성 프로필과 설정 위치를 동시에 설정하려면 아래와 같이 명령어를 실행하면 됩니다.

```bash
java -jar your-app.jar --spring.profiles.active=prod --spring.config.location=/your/path/
```

## 정리

Spring Boot에서 활성 프로필과 설정 위치를 커맨드 라인으로 설정하는 방법은 매우 간단합니다. 이를 통해 다양한 실행 환경에 유연하게 대응할 수 있으며, 애플리케이션의 관리가 편리해집니다. 이러한 기능은 개발자가 애플리케이션을 더 효율적으로 관리할 수 있게 도와줍니다.