---
title: "2019-10-11-[토이프로젝트]LOL Duo - part 2"
subtitle: "기본 구조 및 web.xml 설정 파헤치기"
categories: [Spring Framework]
tags:
  - Spring Framework [스프링]
published: true
---

***
저번 포스트를 보니 Dispatcher Servlet에 대한 설명이 부족한 것 같아 그 부분을 조금 더 다루고 root context와 자식 context의 역할에 대해 알아보고자 한다. 이번 포스트를 하면서 깨달은 점은 내가 쓰고 있던 설정들과 코드들을 100% 완벽히 이해하지 못했다는 점이다. 아직 갈길이 멀다.

***

먼저 `web.xml`을 다시 적어보겠다.
```
<?xml version="1.0" encoding="UTF-8"?>
<web-app version="2.5" xmlns="http://java.sun.com/xml/ns/javaee"         
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee https://java.sun.com/xml/ns/javaee/web-app_2_5.xsd">

	<welcome-file-list>
		<welcome-file>/WEB-INF/jsp/member/main/main.jsp</welcome-file>
	</welcome-file-list>

  <filter>
		<filter-name>encodingFilter</filter-name>
    	<filter-class>
			  org.springframework.web.filter.CharacterEncodingFilter
      </filter-class>
    <init-param>
    	<param-name>encoding</param-name>
      <param-value>utf-8</param-value>
    </init-param>
  </filter>
	<filter-mapping>
	  <filter-name>encodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>

  	<listener>
    	<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
  	</listener>

    <context-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath*:config/spring/context-*.xml</param-value>
    </context-param>

  <servlet>
		<servlet-name>action</servlet-name>
		<servlet-class>
			org.springframework.web.servlet.DispatcherServlet
		</servlet-class>
		<init-param>
			<param-name>contextConfigLocation</param-name>
			<param-value>
				/WEB-INF/config/*-servlet.xml
			</param-value>
		</init-param>
		<load-on-startup>1</load-on-startup>
	</servlet>
	<servlet-mapping>
		<servlet-name>action</servlet-name>
		<url-pattern>/</url-pattern>
	</servlet-mapping>


```

## Dispatcher-Servlet

먼저 Dispatcher Servlet이 무엇인지 알아보자. Spring MVC은 다른 웹 프레임워크 처럼 front controller pattern을 사용한다. 클라이언트(브라우저)로부터 어떠한 요청이 오면 Tomcat과 같은 Servlet Container가 요청을 받는데 이때 제일 앞에서 요청을 처리하는 프론트 컨트롤러를 spring에서 정의하여 이를 Dispatcher Servlet이라고 한다.

Dispatcher Servlet은 request를 처리하면서 공유되는 알고리즘을 제공하고 실제 처리 과정은 지정된 components에서 발생한다. Dispatcher Servlet은 Java Configuration이나 web.xml에서 선언이 되고 mapping이 된다. 그 후 Request Mapping, view resolution, exception handling 등을 처리한다.

![_config.yml]({{ site.baseurl }}/images/20191011-2.png){: width="70%"}

지금 당장은 와닿는 그림은 아니지만 일단 보면서 확인할 수 있는 부분은 Dispatcher Servlet이 중추역할을 하면서 처리와 응답을 관리한다. 이 그림은 한번 더 사용하면서 추후 설명하겠다.

## Context Hierarchy

이 전 포스트에서 언급한것 처럼 Context, 쉽게 말해 설정 파일에도 계층 구조가 있다. 이렇게 계층 구조를 가지는 설정파일을 만드는 이유는 각각 생성한 빈들을 공유할 수 있게 하기 위해서이다. 계층구조에는 바로 root WebApplicationContext와 servlet WebApplicationContext가 계층 구조로 이루어져 있다. 쉽게 구분하자면 ContextLoaderListener가 지정하는 파일은 Servlet WebApplicationContext이고 DispatcherServlet이 지정하는 파일은 root WebApplicationContext이 된다.

이들은 부모와 자식 관계를 가지고 있는데 Root WebApplicationContext는 모든 Servlet WebApplicationContext에서 사용이 가능하다. 말 그대로 root는 뿌리가 되는 느낌이랄까?

그림으로 보면 이러하다.

![_config.yml]({{ site.baseurl }}/images/20191011-3.png){: width="70%"}

단순 설정 빈을 공유하기 위한 이유 말고도 그 목적에도 차이가 난다.
ServletContext의 경우 Entry Point로써 클라이언트의 요청을 처리해 줄 controller의 mapping 설정과 요청 처리 후 view 처리를 어떻게 할 것인가에 대한 설정등을 포함한다.
RootContext의 경우 web application의 실제 비즈니스 혹은 목적을 위한 service layer와 해당 service layer에서 조회 및 처리에 필요한 database와 연결되는 bean들에 대한 설정을 포함한다.

따라서 context component scan을 통한 controller, service, repository의 bean 등록 설정을 할 때 주의를 기울여야 한다. 물론 다 한번에 스캔해버려도 상관은 없지만 불필요한 bean 등록이 발생하게 되어 낭비가 발생한다. 따라서 bean 등록 시 include 와 exclude를 적절히 사용하여 불필요한 중복 bean 등록을 피하는 것이 좋다.

***
최대한 정리를 해보려고 썼지만 글이 영 엉성한 느낌이다. 앞으로 계속해서 수정해나가야 할 것 같다. 다음 포스트가 언제가 될지는 모르겠지만 아직 설정단계가 끝나지 않았다. 스프링은 설정이 반이라더니 그 말이 맞다. 혹시 틀리거나 부족한 부분은 댓글로 남겨주시면 바로바로 수정해나가려고 노력하겠다. 
참고: [흔한개발자](https://addio3305.tistory.com/), [Spring by Pivotal](https://nice2049.tistory.com/entry/spring-rootContext-%EA%B7%B8%EB%A6%AC%EA%B3%A0-servletContext-%EB%8C%80%ED%95%B4%EC%84%9C)
