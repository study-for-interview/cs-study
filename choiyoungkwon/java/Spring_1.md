# Sevlet

## 개념

서블릿은 예전에는 정적 페이지로만 웹 서버에서 응답이 가능했습니다

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1jzUt%2FbtrkaOnnHLt%2Fe3C0HxFs938uzxU9PXNjFK%2Fimg.png)

그렇게 되면 사용자의 상태라던가 게시글 추가 등의 시간의 흐름에 따라서 동적으로 변경되는 상태를 표현하는 것이 불가능 했는데요. 이런 한계점을 극복하고 해결하기 위해서 웹 서버에 프로그램을 붙여서 동적인 페이지를 생성할 수 있게 되었는데 그 중에서 자바에서 동적인 웹페이지를 개발하기 위한 기술 중 하나가 서블릿입니다.

그래서 요약을 하면 서블릿은 웹 서버로부터 요청을 받아서 처리하고 서버에 다시 응답을 하는 하나의 자바 프로그램이라고 할 수 있습니다.


## tomcat

## Servlet Container

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FckhLZ5%2FbtrkiJSnggd%2FAlPrMC7m4c3mRUsGhYqDDK%2Fimg.png)

그리고 서블릿 컨테이너는 말 그대로 서블릿들을 보관하는 그릇(컨테이너)라고 생각하면 되는데요.

서버에 만들어진 서블릿이 스스로 작동하는 것이 아니라, 서블릿을 관리 해주는 것이 필요한데, 이러한 역할을 하는 것이 바로 서블릿 컨테이너이고 대표적으로 오픈소스인 톰캣이 있습니다.

1. 웹서버와의 통신 지원

서블릿 컨테이너는 서블릿과 웹서버가 손쉽게 통신할 수 있게 해주어, 소켓을 만들고 listen, accept 등을 API로 제공하여 복잡한 과정을 생략할 수 있게 해준다.

2. 서블릿 생명주기(Life Cycle) 관리

서블릿 컨테이너는 서블릿의 탄생과 죽음을 관리한다.
서블릿 클래스를 로딩하여 인스턴스화
초기화 메소드를 호출
요청이 들어오면 적절한 서블릿 메소드를 호출합니다.
서블릿 소멸 시 Garbage Collection(가비지 컬렉션)을 진행

3. 멀티쓰레드 지원 및 관리

서블릿 컨테이너는 요청이 올 때 마다 새로운 자바 쓰레드를 하나 생성
HTTP 서비스 메소드를 실행하고 나면, 쓰레드는 자동으로 소멸
원래는 쓰레드를 관리해야 하지만 서버가 다중 쓰레드를 생성 및 운영해주니 쓰레드의 안정성에 대해서 걱정하지 않아도 된다.

4. 선언적인 보안 관리

서블릿 컨테이너를 사용하면 개발자는 보안에 관련된 내용을 서블릿 또는 자바 클래스에 구현해 놓지 않아도 됩니다.
일반적으로 보안관리는 XML 배포 서술자에 다가 기록하므로, 보안에 대해 수정할 일이 생겨도 자바 소스 코드를수정하여 다시 컴파일 하지 않아도 보안관리가 가능합니다.

## 동작과정

1. 사용자가 서블릿에 대한 링크를 클릭한다.(HTTP 요청)

2. 컨테이너는 들어온 요청에 대해서 HttpServletRequest와 HttpServletResponse를 생성

3. 사용자가 보낸 URL를 분석해서 어떤 서블릿에 대한 요청인지 알아내고 스레드에 서블릿을 할당해서 실행하고 Request와 Response를 인자로 넘깁니다.

4. 컨테이너는 서블릿 Service()를 호출하고 Http메서드에 따라 doGet(), doPost()등을 호출

5. 그러면 서블릿은 요청 처리에 대한 응답을 생성해서 Response객체와 같은 곳에 실어서 응답을 보냅니다.

6. 응답이 이뤄지면 모든 작업이 끝난거고 컨테이너는 사용했던 request, response 객체를 소멸시키거나 쓰레드에 할당했던 서블릿을 해제하는 등의 일을 합니다.

# 스프링 기본

## Spring vs Spring MVC vs Spring Boot

## Spring

스프링은 자바 기반의 웹 어플리케이션을 만들 수 있는 프레임워크입니다. 

- 프로젝트를 진행하다 보면 분명 중복되는 코드가 있기 마련이다.  Spring은 이런 중복코드의 사용률을 줄여주고, 비즈니스 로직에 집중해서 작성할 수 있게 해준다.

- Spring을 사용하면 다른 사람의 코드를 참조하여 쓰기 편리한데 이말의 의미는 오픈소스를 좀더 효율적으로 가져다 쓰기 좋은 구조라는 것이다.

- 결론적으로 Spring이란 JAVA 기술들을 더 쉽게 사용할 수 있게 해주는 오픈소스 프레임 워크이다.

## Spring-Boot
스프링 부트(Spring Boot)는 스프링(Spring)을 더 쉽게 이용하기 위한 도구라고 볼 수 있습니다. 스프링 이용하여 개발을 할 때, 이것저것 세팅을 해야 될 요소들이 많습니다. 

Spring Boot는 매우 간단하게 프로젝트를 설정할 수 있게 하여, Spring 개발을 조금 더 쉽게 만들어주는 역할을 하고 있습니다.



## MVC1 vs MVC2

MVC 패턴은 Mode, View, Controller의 앞 글자를 따서 만든 디자인 패턴입니다.

사용자는 얻고자 하는 정보나 기능을 컨트롤러에게 요청한다.

컨트롤러는 사용자의 요청을 수신하고 그에 맞는 비즈니스 로직을 수행한다.

비즈니스 로직을 수행하면서 컨트롤러는 필요에 따라 모델을 호출하여 데이터를 요청한다.

요청을 모두 처리하면 뷰를 통해 사용자가 원하는 정보를 시각적으로 보여준다. (화면으로 출력)

### MVC 모델 1

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FI1UUx%2FbtqEZ0IhZ6O%2FqzvwssYAAkEltNqYd3Kpik%2Fimg.png)

MVC 모델 1은 뷰와 컨트롤러의 역할이 합쳐져 있다.

흔히 웹 개발을 하면 Jsp가 뷰 역할을 하는데, MVC 1에서 Jsp는 뷰와 컨트롤러의 역할을 모두 감당한다.

위와 같이 Jsp가 뷰와 컨트롤러 역할을 모두 수행하면, Jsp에 Java 코드와 Html, css 등의 코드가 섞여 있어, 소스가 복잡해지고 읽기가 어려워져 유지보수가 힘들어 진다.

하지만 상대적으로 설계가 간단하여 개발 속도가 빠르고 작은 프로젝트에 알맞다.

### MVC 모델 2

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbgbhsb%2FbtqE0BOnWqs%2FGhoRjVi90P1dYSBjRHSo91%2Fimg.png)

MVC 모델 2은 모델 1에서 유지보수가 힘들다는 단점을 보완하기 위해 나온 모델이다.

기존에 뷰와 컨트롤러의 역할을 모두 수행하던 JSP는 뷰의 역할만 하게 하고, 대신 컨트롤러 역할을 Servlet이 수행한다.

모델은 기존 MVC 1 방식과 동일하다.

MVC 2에서는 컨트롤러 역할을 수행하는 Servlet이 요청을 받아준다. 

Servlet이 비즈니스 로직을 수행하며 모델을 호출하여 데이터를 요청하며, 최종적으로 뷰 역할인 Jsp를 제어하여 화면을 출력한다.

MVC 2로 개발하게 되면 Html과 Java 코드가 분리되어 확장에 용이하고 유지보수가 수월해진다.

### Spring MVC

![image](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F183bb42c-2998-4362-ade1-b7d75f75a851%2FUntitled.png&blockId=209ecc2e-d659-4a44-a519-675c16309d89)



## dispatcher servlet

### FrontController 패턴
사용자의 요청을 Servlet에게 전달하기 위해서는 web.xml에 servlet을 등록하고 mapping하는 과정이 필요합니다. 하지만 수 많은 요청이 필요한 어플리케이션의 경우 계속해서 servlet을 등록하고 mapping하는 과정이 필요로하게 됩니다. web.xml을 별도로 관리해주어야 하는 불편함이 있습니다. 이 때문에  새로운 패턴이 생겨났는데요 그것이 바로 FrontController 패턴입니다. 아래의 그림을 보면 조금 더 수월하게 이해하실 수 있을것 같습니다.

### 기존의 Servlet 
![image](https://t1.daumcdn.net/cfile/tistory/99E1DD3D5CC05AD331)

### FrontController 패턴

![image](https://t1.daumcdn.net/cfile/tistory/99806B4B5CC05AD829)

FrontController 패턴을 적용하면 하나의 서블릿에서 모든 요청을 받아들여 적절한 Controller로 요청을 위입해줍니다.

### 장점 
기본적으로 사용자의 모든 요청에 대해서 인코딩처리, 에러 페이지 처리, 공지 등에 대한 처리를 한곳에서 할 수 있습니다.

## Dispatcher Servlet
Spring에서는 위와 같은 Front Controller 패턴을 취하는 Servlet을 미리 만들어 두었습니다.

그것이 바로 Dispatcher Servlet입니다.

즉, 모든 요청을 한곳에서 받아서 필요한 처리를 한 뒤, 요청에 맞는 handler로 요청을 dispatch하고, 해당 handler의 실행 결과를 Http Response형태로 만드는 역할을 합니다.


[ Dispatcher-Servlet(디스패처 서블릿)의 동작 방식 ]
앞서 설명한대로 디스패처 서블릿은 적합한 컨트롤러와 메소드를 찾아 요청을 위임해야 합니다. Dispatcher Servlet의 처리 과정을 살펴보면 다음과 같습니다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FY5nZW%2FbtrsHGTIP02%2FO3ff3AhmLzkCkknoImVTK0%2Fimg.png)

1. 클라이언트의 요청을 디스패처 서블릿이 받음
2. 요청 정보를 통해 요청을 위임할 컨트롤러를 찾음
3. 요청을 컨트롤러로 위임할 핸들러 어댑터를 찾아서 전달함
4. 핸들러 어댑터가 컨트롤러로 요청을 위임함
5. 비지니스 로직을 처리함
6. 컨트롤러가 반환값을 반환함
7. HandlerAdapter가 반환값을 처리함
8. 서버의 응답을 클라이언트로 반환함


## IoC

IoC(Inversion of Control)란 "제어의 역전" 이라는 의미로, 말 그대로 메소드나 객체의 호출작업을 개발자가 결정하는 것이 아니라, 외부에서 결정되는 것을 의미한다.

IoC는 제어의 역전이라고 말하며, 간단히 말해 "제어의 흐름을 바꾼다"라고 한다.

객체의 의존성을 역전시켜 객체 간의 결합도를 줄이고 유연한 코드를 작성할 수 있게 하여 가독성 및 코드 중복, 유지 보수를 편하게 할 수 있게 한다.

기존에는 다음과 순서로 객체가 만들어지고 실행되었다.

1. 객체 생성

2. 의존성 객체 생성
클래스 내부에서 생성

3. 의존성 객체 메소드 호출

하지만, 스프링에서는 다음과 같은 순서로 객체가 만들어지고 실행된다.

1. 객체 생성

2. 의존성 객체 주입
스스로가 만드는것이 아니라 제어권을 스프링에게 위임하여 스프링이 만들어놓은 객체를 주입한다.

3. 의존성 객체 메소드 호출

스프링이 모든 의존성 객체를 스프링이 실행될때 다 만들어주고 필요한곳에 주입시켜줌으로써 Bean들은 싱글턴 스코프 특징을 가지며, 제어의 흐름을 사용자가 컨트롤 하는 것이 아니라 스프링에게 맡겨 작업을 처리하게 된다.


## DI

DI(Dependency Injection)란 스프링이 다른 프레임워크와 차별화되어 제공하는 의존 관계 주입 기능으로, 객체를 직접 생성하는 게 아니라 외부에서 생성한 후 주입 시켜주는 방식이다.

![image](https://velog.velcdn.com/images%2Fgillog%2Fpost%2F08489bda-549e-4dae-851b-8ae1734bf85e%2F21373937580AEF9B37.jpg)

두번째 방식이 의존성 주입의 예시인데,
A 객체에서 B, C객체를 사용(의존)할 때 A 객체에서 직접 생성 하는 것이 아니라 외부(IOC컨테이너)에서 생성된 B, C객체를 조립(주입)시켜 setter 혹은 생성자를 통해 사용하는 방식이다.

![image](https://velog.velcdn.com/images%2Fgillog%2Fpost%2F41f2eb24-fce2-4b7e-b9ac-d5c3ce97d213%2F22535642580C4AF12C.jpg)

스프링에서는 객체를 Bean이라고 부르며, 프로젝트가 실행될때 사용자가 Bean으로 관리하는 객체들의 생성과 소멸에 관련된 작업을 자동적으로 수행해주는데 객체가 생성되는 곳을 스프링에서는 Bean 컨테이너라고 부른다.

## Bean, Component

Spring IoC 컨테이너가 관리하는 자바 객체를 **빈(Bean)**이라고 부릅니다

실제 빈을 등록하기 위한 방법은 클래스에 @Component 어노테이션으로 등록하는 방법과 Configuration 클래스에 @Bean으로 등록하기 위한 방법

## @component @service @controller

@Component, @Service, @controller, @Repository 전부 스프링에서 해당 클래스를 빈으로 등록하기 위해서 사용하는 어노테이션입니다.

차이점은 @Component는 모든 Spring 설정에 대한 일반적인 스테레오 타입입니다.

@Service는 서비스 계층에서 클래스에 어노테이션을 사용합니다.

@Repository 는 데이터베이스 저장소 역할을 하는 persistence 계층에서 클래스에 주석을 답니다.
@Repository 의 작업은 Persistent 관련 특정 예외를 포착하여 Spring의 통합된 확인되지 않은 예외 중 하나로 다시 throw하는 것 입니다.
이를 위해 Spring은 애플리케이션 컨텍스트에 추가해야 하는 PersistenceExceptionTranslationPostProcessor 를 제공합니다(Spring Boot를 사용하는 경우 이미 포함됨).

@Controller MVC 패턴에서 컨트롤러 역할을 합니다. 디스패처는 @RequestMapping 주석을 감지하여 매핑된 메서드에 대해 주석이 달린 클래스를 스캔합니다.

## Container
Container 는 Spring 의 핵심입니다. Container 는 개발자를 대신하여, Bean 을 생성 / 관리 / 제거합니다. Container 가 Bean 을 관리해주기 때문에, 개발자는 모듈 간에 의존 및 결합으로 인해 발생하는 문제로부터 자유로워 졌습니다. 아래와 같이 독립적인 코드를 작성해서 Annotaion 만 남겨주면 Container 가 개발자가 원하는 상황에 코드를 실행합니다. 따라서 개발자는 메서드가 언제, 어디서 호출되어야 하는지 그리고 메서드를 호출하기 위해 필요한 매개 변수를 준비해서 전달하지 않습니다. Container 가 개발자 대신 알아서 호출합니다.

스프링에서는 IoC를 담당하는 컨테이너를 빈 팩토리 또는 애플리케이션 컨텍스트라고 부릅니다.

오브젝트의 생성과 오브젝트 사이의 관계를 설정하는 DI관점에서 볼 때는 IoC 컨테이너를 빈 팩토리라고도 하는데 사실 스프링 컨테이너는 DI 작업보다 더 많은 일을 하고 이에 해당하는 필요한 여러가지 컨테이너 기능을 추가한 것을 애플리케이션 컨텍스트라고 부릅니다.



## VO vs DTO vs DAO

DAO(Data Access Object) 는 데이터베이스의 data에 접근하기 위한 객체입니다. DataBase에 접근 하기 위한 로직 & 비지니스 로직을 분리하기 위해 사용합니다.

DTO(Data Transfer Object) 는 계층 간 데이터 교환을 하기 위해 사용하는 객체로, DTO는 로직을 가지지 않는 순수한 데이터 객체(getter & setter 만 가진 클래스)입니다.
유저가 입력한 데이터를 DB에 넣는 과정을 보겠습니다.
유저가 자신의 브라우저에서 데이터를 입력하여 form에 있는 데이터를 DTO에 넣어서 전송합니다.
해당 DTO를 받은 서버가 DAO를 이용하여 데이터베이스로 데이터를 집어넣습니다.

VO(Value Object) 값 오브젝트로써 값을 위해 쓰입니다. read-Only 특징(사용하는 도중에 변경 불가능하며 오직 읽기만 가능)을 가집니다.
DTO와 유사하지만 DTO는 setter를 가지고 있어 값이 변할 수 있습니다.
