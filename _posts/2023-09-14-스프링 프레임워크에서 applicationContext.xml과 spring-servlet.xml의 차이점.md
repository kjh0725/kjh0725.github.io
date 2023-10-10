---
title: 스프링 프레임워크에서 applicationContext.xml과 spring-servlet.xml의 차이점
date: 2023-09-14 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - Framework
---
## 스프링 프레임워크와 XML 설정 파일

스프링 프레임워크는 자바 기반의 웹 애플리케이션 개발을 위한 도구입니다. 이 프레임워크에서는 주로 XML 파일을 이용해 애플리케이션 설정을 관리합니다. applicationContext.xml과 spring-servlet.xml은 스프링 프레임워크에서 사용하는 두 가지 주요 XML 설정 파일입니다. 이 두 파일은 유사해 보이지만 역할과 사용처가 다릅니다.

## applicationContext.xml의 역할

applicationContext.xml은 애플리케이션 전반에 걸쳐 사용되는 빈(Bean)을 설정합니다. 빈이란 스프링에서 관리하는 자바 객체를 의미합니다. 이 파일은 데이터베이스 연결, 보안 설정, 서비스 레이어 설정 등 애플리케이션의 전반적인 설정을 담당합니다. 특히, 스프링 프레임워크의 핵심 컨테이너인 ApplicationContext가 이 파일을 읽어 들여 애플리케이션의 빈 설정을 초기화합니다.

## spring-servlet.xml의 역할

spring-servlet.xml은 웹 관련 설정을 담당하는 파일입니다. DispatcherServlet, 웹 애플리케이션에서 HTTP 요청을 처리하는 컨트롤러, 은 이 파일을 이용하여 뷰 리졸버(View Resolver), 핸들러 맵핑(Handler Mapping) 등 웹 관련 설정을 초기화합니다.

## 두 파일의 차이점

1. **범위(Scope)**: applicationContext.xml은 애플리케이션 전체 설정을 관리하고, spring-servlet.xml은 웹 관련 설정만을 관리합니다.
2. **초기화 시점(Initialization Time)**: ApplicationContext는 애플리케이션 시작 시 applicationContext.xml을 로드합니다. 반면 DispatcherServlet은 첫 HTTP 요청이 발생했을 때 spring-servlet.xml을 로드합니다.
3. **빈 등록(Bean Registration)**: applicationContext.xml에 정의된 빈은 전체 애플리케이션에서 사용할 수 있습니다. 반면 spring-servlet.xml에 정의된 빈은 웹 계층에서만 사용할 수 있습니다.

## 정리

applicationContext.xml과 spring-servlet.xml은 각각 애플리케이션의 전반적인 설정과 웹 관련 설정을 담당하는 스프링의 설정 파일입니다. 이 두 파일은 범위, 초기화 시점, 빈의 사용 범위 등에서 차이점을 보입니다. 이러한 차이를 이해하면 스프링 프레임워크를 더 효율적으로 사용할 수 있습니다.