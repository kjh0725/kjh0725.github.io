---
title: IntelliJ에서 Spring Boot 프로필 활성화실행하기
date: 2023-10-07 20:00:00 +0900
categories:
  - Spring
tags:
  - IntelliJ
  - SpringBoot
---
## 개요

Spring Boot는 각각 다른 환경에서 애플리케이션을 실행할 수 있게 해주는 프로필(Profile)이라는 기능을 제공합니다. 이 글에서는 IntelliJ IDE에서 Spring Boot 프로필을 어떻게 활성화하는지에 대해 자세히 알아보겠습니다.

## IntelliJ에서 프로필 설정 방법

### Run/Debug Configurations 열기

IntelliJ 상단 툴바에서 'Run' 메뉴를 찾아 'Edit Configurations'를 선택합니다. 이를 통해 실행 설정을 조정할 수 있는 창이 나타납니다.

### VM Options 설정하기

Run/Debug Configurations 창에서 왼쪽 패널을 통해 Spring Boot 애플리케이션을 선택합니다. 그 다음 'VM options'란에 다음과 같이 입력합니다.

```plaintext
-Dspring.profiles.active=your-profile-name
```

여기서 `your-profile-name`은 활성화하려는 프로필의 이름입니다.

### 환경변수(Environment variables) 사용

'Environment variables' 섹션에서도 프로필을 설정할 수 있습니다. 해당 영역에 `SPRING_PROFILES_ACTIVE=your-profile-name`을 입력하면 됩니다.

## 주의사항

### 프로필 충돌

여러 방법으로 프로필을 설정할 경우, 가장 나중에 설정한 프로필이 적용됩니다. 예를 들어 VM options과 환경변수 모두 설정했다면, 환경변수가 우선적으로 적용됩니다.

### IntelliJ 재시작

설정을 변경한 후에는 IntelliJ를 재시작해야 변경 사항이 적용될 수 있습니다.

## 마무리

Spring Boot 프로필은 개발부터 배포까지 다양한 환경에서 코드를 유연하게 관리할 수 있게 해줍니다. IntelliJ 환경에서도 이를 쉽게 설정할 수 있으니, 본 글을 참고하여 여러분의 작업을 더 효율적으로 만들어 보세요.