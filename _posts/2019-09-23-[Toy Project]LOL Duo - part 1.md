---
title: "2019-09-23-[토이프로젝트]LOL Duo - part 1"
subtitle: "기본 구조 및 web.xml 설정 파헤치기(Encoding, Dispatcher-Servlet)"
categories: [Spring Framework]
tags:
  - Spring Framework [스프링]
published: true
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
![_config.yml]({{ site.baseurl }}/images/20191008-1.png){: width="50%"}

Controller, Service, DAO class 들을 기능 별로 묶었고 root context와 servlet context를 볼 수 있다. 두 context config에 대해서는 차차 다루기로 하고 먼저 web.xml을 들여다 보자. 먼저 전체 코드이다.

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

  <context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath*:config/spring/context-*.xml</param-value>
  </context-param>
```

최대한 자세히 설명하고자 하니 첫번째 줄 부터 보자.

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app version="2.5" xmlns="http://java.sun.com/xml/ns/javaee"         
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee https://java.sun.com/xml/ns/javaee/web-app_2_5.xsd">
```

이는 서블렛 버전에 따라 다르다. 현재 필자가 쓰고 있는 서블렛 버전은 2.5 이고 아는 바로는 4.0까지 있는 걸로 알고 있다. 따라서 원하는 설정에 따라 위의 헤더를 바꾸어주면 될 것 같다.

```
<welcome-file-list>
  <welcome-file>/WEB-INF/jsp/member/main/main.jsp</welcome-file>
</welcome-file-list>
```

사실 있어도 되고 없어도 되는 코드이다. 맨 처음 프로젝트를 실행했을 때 나오는 jsp 파일을 지정해 준 것인데 이는 컨트롤러로 처리가 가능하기 때문에 없어도 무방하다. 필자는 그냥 만들어놨다.

```
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
```

이 부분은 중요하다.
필터를 설정하는 것인데 스프링은 인코딩 처리를 위해 CharacterEncodingFilter를 제공한다.
(org.springframework.~~~이걸 보면 아 ~ 스프링은 이걸 제공해주는구나~라고 생각해라) 대한민국은 한글을 쓰고 있기 때문에 utf-8 인코딩이 반드시 필요하다. 모든 페이지에 인코딩을 적용하고 싶기 때문에 `<url-pattern>`에 `/*`을 넣는다. `*`의 뜻은 뒤에 무엇이 오든 모든 것을 포함한다라는 뜻이다. 이렇게 되면 /뒤에 오는 어떤 url 오든지 간에 다 인코딩이 적용된다.

```
<listener>
  <listener-class>
    org.springframework.web.context.ContextLoaderListener
  </listener-class>
</listener>

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

<context-param>
  <param-name>contextConfigLocation</param-name>
  <param-value>classpath*:config/spring/context-*.xml</param-value>
</context-param>
```

먼저 ContextLoaderListener의 역할에 대해 알아보자. DispatcherServlet에 의해 생성된 Beans은 ContextLoaderLisener에 의해 생성된 Bean을 참조할 수 있다. 또 Controller가 공유하는 Bean들(DAO, DataSource, Service)을 포함하는 Spring Container를 생성한다.

조금 더 깊이 들어가보자. 예를 들어 다음과 같은 설정 코드가 있다.

```
<servlet>
  <servlet-name>aController</servlet-name>
  <servlet-class>
    org.springframework.web.servlet.DispatcherServlet
  </servlet-class>
  <init-param>
	  <param-name>contextConfigLocation</param-name>
	  <param-value>/WEB-INF/a-servlet.xml</param-value>
  </init-param>
  <load-on-startup>1</load-on-startup>
</servlet>

<servlet>
  <servlet-name>bController</servlet-name>
  <servlet-class>
    org.springframework.web.servlet.DispatcherServlet
  </servlet-class>
  <init-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>/WEB-INF/b-servlet.xml</param-value>
  </init-param>
  <load-on-startup>1</load-on-startup>
</servlet>
```

위의 경우는 DispatcherServlet은 각각 별도의 `WebApplicationContext`를 사용한다. 따라서 두 context는 독립적이므로 각각의 설정 파일에서 생성한 빈을 공유할 수 없다.

만약 각각 생성한 빈을 공유하고 싶다면 앞서 언급했듯이 `ContextLoaderListener`를 사용하여 공통으로 사용할 빈을 설정할 수 있다. web.xml에 들어가있는 코드가 이에 해당하는 코드다. ContextLoaderListener와 DispatcherServlet은 각각 webapplicationcontext를 생성한다. ContextLoaderListener가 생성한 context가 `root WebApplicationContext`가 되고 DispatcherServlet이 생성한 인스턴스는 `Servlet WebApplicationContext`가 된다. Servlet WebApplicationContext들은 root WebApplicationContext의 설정 빈을 사용할 수 있다.

그림으로 보면 다음과 같다.
![_config.yml]({{ site.baseurl }}/images/20191008-2.png)
출처:[Heee's Development Blog](https://gmlwjd9405.github.io/)

따라서 현 프로젝트의 Servlet WebApplicationContext는 `/WEB-INF/config/*-servlet.xml` 여기에 해당하는 모든 xml 파일들이 되고 dispatcherServlet이 만든 Root WebApplicationContext는 `classpath*:config/spring/context-*.xml` 여기에 해당하는 모든 xml들이 되겠다. 이들에 관해서는 보다 자세히 다음 포스트에서 설명하도록 하겠다.

***
이 포스트에서는 web.xml에 대해서 알아보았다. 생각보다 더 오래걸려서 놀랐지만 끝까지 해보도록 하겠다. 포스팅하고 싶은게 너무 많아서 고민을 많이했는데 프로젝트에 대한 포스팅은 잘한 결정인 것 같다.

***

참고: [흔한개발자](https://addio3305.tistory.com/), [Amor Fati](https://nice2049.tistory.com/entry/spring-rootContext-%EA%B7%B8%EB%A6%AC%EA%B3%A0-servletContext-%EB%8C%80%ED%95%B4%EC%84%9C), [랄라라](https://unabated.tistory.com/entry/%EC%8A%A4%ED%94%84%EB%A7%81-ContextLoaderListener-%EC%9D%98-%EC%97%AD%ED%95%A0)
