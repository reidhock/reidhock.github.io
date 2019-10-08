---
title: "2019-09-23-[토이프로젝트]LOL Duo - part 1"
subtitle: "리그 오브 레전드 api를 이용해서 롤 듀오 매칭 사이트를 만들어보자"
categories: [Spring Framework]
tags:
  - Spring Framework [스프링]
published: false
---

***
처음 프로젝트를 진행했을 때 나온 아이디어 중 하나를 가지고 두번째 프로젝트를 시작하려고 한다. 그동안 [흔한개발자](https://addio3305.tistory.com/)의 블로그를 보고 프로젝트를 진행했는데 몇몇 스프링 설정이나 다른 소소한 부분들을 디테일하게 이해하지 못한 부분이 있었다. 그래서 이번 기회에 두번째 프로젝트를 진행하면서 스프링 설정들의 개념이나 그 밖의 요소들을 복습할 겸 포스트할 계획이다.

***

먼저 개발환경이다.
```
Server: Tomcat 7.0
Tool: STS 3.99, GIT, SQL Developer
DB: Oracle 10g
Language: Java(jdk 1.8), JSP, HTML, Javascript, jQuery, ajax
Framework: Spring Framework
```

이미 프로젝트가 진행이 된 상태이기 때문에 조금 조잡해보일지도 모르겠지만 하나하나 정리해나가면서 설명해나가려고 한다.

먼저 전체적인 구조이다.
