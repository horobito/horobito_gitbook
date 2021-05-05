# CGI Servlet

만든이  
1. 김지환 : odkfu1@gmail.com - 나   
2. 장재혁 : obg2546@naver.com

## 00. 이전내용 복습

### 1 . CGI

* 동적으로 요청을 받고 응답을 하기 위해 자바에서 사용하는 기술 
* 과거에는 이를 위해서 xml을 이용해서 서블릿의 정의와 매핑을 엄청나게 때려넣음 
* cf\)
  * 서블릿
    * 자바를 사용하여 웹페이지를 동적으로 생성하는 서버측 프로그램 
* cf2\)
  * xml
    * W3C에서 개발된, 다른 특수한 목적을 갖는 마크업 언어를 만드는데 사용하도록 권장하는 다목적 마크업 언어



* 심지어 서블릿은 느리다. 
* 이렇기 때문 자바EE 기반의 서블릿에서 벗어나서 가벼운 것을 사용하기로 함
* 이로서 탄생한 것이 \[ 스프링 웹 애플리케이=Spring Web Application \] 
* 스프링 프레임워크의 요소들 중 Web에 대하여 볼 것 
* cf\) JDBC\[Java Database Connectivity\]
  * **자바에서 데이터베이스에 접속할 수 있도록 하는 자바 API**



* cf\) ORM\[Object Relational Mapping\]
  * 객체 관계 맵핑 - 나중에 알아볼 것 



* cf\) JSP\[Java Server Page\]
  * 자바서버 페이지
  * HTML내에 자바 코드를 삽입하여 웹 서버에서 동적으로 웹 페이지를 생성하여 웹 브라우저에 돌려주는 언어, 도구 
  * Java 언어를 기반으로 하는 Server Side 스크립트 언어



* cf\) MVC \[Model - View - Controller\]
  * 개발 할 때, 3가지 형태로 역할을 나누어 개발하는 방법론
  * 모델 
    * 핵심 기능 및 데이터 보관
  * 뷰 
    * 사용자에게 정보를 표시
  * 컨트롤러 
    *  사용자로부터 요청을 입력받아 처리 
    * 

## 02. Spring MVC\(스프링 기반의 웹어플리케이션 개발방법\)  

### 1. Model1

![](../.gitbook/assets/image%20%283%29.png)

* JSP를 이용한 아키텍쳐
* 동작과정
  * 브라우저에서 [**www.daum.net**](http://www.daum.net/) **이라는 요청**을 보냄
  * 해당되는 **JSP에서 안에 로직으로 javaBean 호출**
  * **javaBean은 repository\(저장소\)에 있는 데이터\(user\)를 꺼내오고**, **JSP에 오브젝트\(userDao로 따지면 user오브젝트\) 전달**
  * **JSP**에서 **javaBean**으로부터 받은 데이터 \(user 오브젝트\)를 **활용해서 작업을 처리하** response\(반응\)
  * 그 response를 브라우저에 전달하 www.daum.net의 화면을 보여줌 cf\) javaBean: DB에 접근하여 데이터를 가져오는 객체, 앞에서 배운내용으로 UserDao 같은 놈임

 =

* 이를 서버- 클라이언트 구조로 
  * 클라이언트에서 서버에 요청
  * JSP에서 요청을 받는다
  * JSP에서 요청을 처리하고 \( ← 처리에 필요한 데이터는 DB와 연동된 JavaBean에서 받아옴 \)
  * 처리한 응답을 보여주기 까지 한다 
* **즉 JSP에서 요청,처리, 응답 등 다양한 과정들을 혼자서 처리했다.**



* 웹이 확장되기 시작하면서 웹 속의 비지니스 로직도 굉장히 복잡하게 변화하고 화면도 굉장히 다양하게 변하게 되었다. → **JSP파일은 점점 복잡해졌다.**



### 2. MODEL2\(MVC\)

* 역할과 책임을 분리한 것
* Jsp는 순수하게 보여주는것\(**View**\)만하고
* 요청 처리는 **서블릿**\(**Controller**\)에서 하자
* JavaBean은 빵셔틀\(**Model**\), DB로부터 데이터 가져오는 역할 → 역할을 나눔으로서 유지보수가 더 쉬워지고 코드가 깔끔해짐
* 기존에 Model1에서 JSP안에 있던 각종 복잡한 로직들은 Controller에 빼버리고 jsp에는 결과만 전달하는 형식으로 바뀜

![](../.gitbook/assets/image%20%284%29.png)

\*\*\*\*

* **Model+View+Controller=MVC 패턴**
* 단일 책임의 원칙 - 하나의 객체는 하나의 책임만을 가진다.
* 저 위 JSP와 Datasource 사이의 JavaBean. 즉 DB로부터 받아온 모델인 Model이 우리가 쓰게 될 DB의 것들, 
* 보통 DB entity\[DB 객체\], 라고 많이 불린다.
* 동작 
  1. 브라우저에서 www.daum.net이라고 **요청**
  2. 맨처음 **요청을 받는 것은 Controller\(servlet클래스\)**
  3. **javaBean\(Model\)에 들어있는 비지니스 로직**들을 **controller에서 처리** cf\)제어해야되는 단순한 로직 이외의 로직들\(path나 화면과 관련된\)을 Controller에서 처리한다.
  4. Controller에서 **처리가 끝난 것을 Model에 담아서** **jsp\(View\)에 전달**
  5. **jsp는** 이 서블릿이 전달한 모델\(오브젝트\)만 **화면에 꺼내서 브라우저에 전송**해줌\(화면에 결과가 뜸\)



* ex\)
  * JavaBean : 주방 보조

    * – DB에 가서 재료를 가져와서 controller에 전달

  * Controller: 요리사

    * 받은 재료를 요리 후 JSP에 전달

  * JSP : 서버

    * 받은 요리를 손님\(Browser\)에 전달

  * =&gt; 분업화가 잘 되어있다.
  * =&gt; SRP, 즉 단일책임의 원칙을 잘 따른다.



* 정리해서 말하자면, javaBean에서 비지니스 로직을 Controller가 받아와서 처리를 하고, 결과를 model에 감싸서 jsp에 전달하는 구조 -&gt; **보다 화면 부분을 깔끔하게 처리한 것**

 

* **Spring MVC도 Model2를 기반으로 한다** 
* MODEL1에서는 모든 일들을 JSP에서 다했다. 
* 이후 웹의 확장으로 인해 JSP를 해결하기 위해 MODEL2가 나왔고 MODEL에서는 역할을 분리해서  Model, View, Controller로 나뉘었다. 
* 그리고 Spring MVC는 이 MODEL2를 기반으로 나왔다.

### 3. Spring MVC

* 처리하는 Servlet이 하나\(DispatherServlet\)만 존재함 
* Dispather Servlet이 모든 Controller역할 다함- MVC중 C 
* ApplicatonContext는 계층구조를 가질 수 있다. 
* DispatherServlet 안에는 Servlet WebApplicatonContext와 Root WebApplicatonContext가 존재함
  *  * Servlet WebApplicatonContext: Bean들을 관리함
    * Root WebApplicatonContext: 상위 WebApplicatonContext 
* 모든 요청\(request\)이 들어오면 그에 맞는 매핑을 찾아서 던져준다.

![](../.gitbook/assets/image%20%287%29.png)



* Q. 어떻게???
* A. Servlet WebApplicationContext 안에 들어있는 Handler Mapping & View Resolver & Controller 를 찾아서 작동

### 4. Spring MVC Controller LifeCycle \[동작 구조\]

![](../.gitbook/assets/image%20%285%29.png)

* 동작과정 예

1. 클라이언트에서 www.daum.net이라는 요청
2. Controller에 해당하는 Dispatcher Servlet이 모든요청을 받음 특정 path는 어떻게 실행할지에 대한 부분들은 Dospatcher Servlet이 Handler Mapping을 통해서 Controller, 즉 특정 url path에 해당되는 것을 실행하는 역할을 하는 HandlerAdapter를 매핑함 \(자바 웹애플리케이션에서 servlet의 역할을 하는 놈\)
3. Controller가 비지니스 로직을 잘 수행하고 감싼다.
4. View Resolver- 물리적인 jsp파일이나 템플릿 엔진을 통한 화면에 표현해주는 파일과 매핑해주는 역할 -&gt; 매핑된결과가 화면에 뜸

\*\*\*\*

* **Handler Mapping**: 요청을 처리해줄 **컨트롤러를 찾아주는 역할**
* **ViewResolver**: JSP등 화면을 표현해주는 파일과 처리결과를 **매핑해주는 역할**
* **HandlerAdapter:** 
  * 사용자의 요청을 처리할 Controller를 찾는다
  * 컨트롤러에 **알맞은 메소드 실행 처리를 요청하는** 할
  * 요청 url에 해당하는 Controller 정보를 저장하는 table을 가진다. [https://gmlwjd9405.github.io/2018/12/20/spring-mvc-framework.html](https://gmlwjd9405.github.io/2018/12/20/spring-mvc-framework.html)
* **root-context.xml**
  * context.xml의 계층구조를 보이기위해 가져다 놓은것
  * 여러 웹애플리케이션이 활용할만한 빈들을 넣는 곳
* **dispatcher-sevlet.xml**
  * 빈을 관리해주는 xml기반의 Spring web ApplicationContext 정의하는 부분
  * Spring MVC에 관한 정의들에 특화시켜놓음

이후는 실습 내용

* 서블릿을 3개만 추가했는데 web.xml파일 줄 수가 매우 많다.

=&gt; 서블릿이 커지면 커질수록 그 줄 수가 비례

* 이제 이걸 바꿀 예정
* &gt; Q. 어떻게?

A. build.gradle에서 코드를 추가해서

implementation "org.springframework:spring-core:${springVersion}"

implementation "org.springframework:spring-context:${springVersion}"

implementation "org.springframework:spring-jdbc:${springVersion}"

implementation "org.springframework:spring-webmvc:${springVersion}“

Q. 왜 이렇게 하는가?

A. 의존성을 추가해서 스프링의 기능을 서버가 하도록??

+ group 위에다가 스프링 버전을 나타내는 코드 추가

ext {

springVersion = '5.1.6.RELEASE'

}

Q. 스프링은 서블릿이 몇 개? A. 1개

Q. 그 서블릿의 이름은? A. Dispatcher Servlet

cf\) 요즘은 Dispatcher Servlet말고

Dispatcher Handler 라는 것이 존재

Dispatcher Handler : Reactive 한 스프링

방법

1. 일단 web.xml 내 서블릿을 다 밀어버린다.

* 주의할 점
* &gt; Spring MVC에서

Root WebApplication Context 와

Servlet WebApplication Context가

어떻게 상호작용하는지 주의깊과 관찰해라

1. Root Web Application을 만들 때,

context param 이라는 것을 사용하여

xml을 분리시킬 수 있다. - ???

1. 서블릿 등록

web.xml에서`1<context-param> 2 <param-name>contextConfigLocation</param-name> 3 <param-value>/WEB-INF/root-context.xml</param-value> 4</context-param>`

* web ApplicationContext= servletContext가 로딩이 되면서 특정한 파라미터를 받는것을 보이는 예시코드 이다.
* 위에 예시는 WEB-INF/root-context.xml에 있는 빈들을 ApplicationContext로 로딩해오는 것이다.

web.xml`1<context-param> 2 <param-name>contextConfigLocation</param-name> 3 <param-value>/WEB-INF/root-context.xml</param-value> 4</context-param>`

* web ApplicationContext,즉 servletContext가 로딩이 되면서 특정한 파라미터를 받는 것을 나타내는 코드이다.
* 위의 예시는 **WEB-INF/root-context.xml에 있는 빈들을 ApplicationContext로 로딩**해오는 것이다.

**dispatcher 서블릿 정의 및 매핑**`1<servlet> 2 <sevlet-name>dispatcherServlet</sevlet-name> 3 <sevlet-class>org.springframework.web.sevlet.DispatcherServlet</sevlet-class>// 실제 컨트롤러(MVC패턴의 컨트롤러, Spring에서의 개념과 다른 거임) 4 <init-param>//dispatcherServlet이 처음 init될 때 로딩을 할 때 빈과 관련 된 정의들을 로딩하는 것 5 <param-name>contextConfigLocation</param-name> 6 <param-value>/WEB-INF/dispatcher-servlet.xml</param-value> 7 </init-param> 8 <load-on-startup>1</load-on-startup>//서블릿은 요청이 될 때 init이 되어야함// 이부분은 처음부터 로딩하라는 의미임 안에 숫자는 우선순위(1이 제일 높음) 9</servlet> 10<sevlet-mapping> 11 <sevlet-name>dispatcherServlet</sevlet-name> 12 <url-pattern>/</url-pattern> 13</sevlet-mapping>`

####  ApplicationContext의 계층구조 <a id="ApplicationContext&#xC758;-&#xACC4;&#xCE35;&#xAD6C;&#xC870;"></a>

* root-context와 dispatcher-sevlet **둘다 ApplicationContext**이다
* sevlet안에는 이러한 dispatcher-sevlet이 여러개가 존재할 거임
* 계층구조를 이용해서 공통되는 것들은 root- context에 정의하고 하위에 의존되는 것들은 하위에 정의하는 식
* 그러나 root-context는 거의 사용되지 않는다.-&gt; 대부분의 웹애플리케이션은 단독으로 존재하기 때문

-&gt; 이건 그냥 **계층구조를 보여주기 위한 예시**임

위에 코드까지 작성하면 LifeCycle중 **dispatcher sevlet부분**이 끝난 것

#### Spring의 Controller <a id="Spring&#xC758;-Controller"></a>

`1public class SimpleController implments Controller{// 이것을 상속받아서 구현하면됨 2 @override 3 public ModelAndView handlerRequest(HttpServletRequest request,HttpServletResponse response ) throws Exception{ 4 return null; 5 } 6}`

* 이것을 구현만 하면 Spring의 Controller역할을 수행하는 것
* 실제 비지니스 로직을 연결해주는 역할을 담당\(HandlerAdapter\) cf\) Conroller를 implement할 때 받아온 handlerRequest메소드를 HandlerAdapter라고 한다.

 `1@Controller 2@RequestMapping 3public class HelloController { 4 5 @RequestMapping("/hello") 6 public ModelAndView hello(){ 7 ModelAndView modelAndView= new ModelAndView("index"); 8 modelAndView.addObject("title", "제하"); 9 modelAndView.addObject("hello", "서버키고싶당"); 10 return modelAndView; 11 } 12}`

* 여기서 ModelAndView는 Spring에서 제공하는 모델을 담는 그릇이자, 뷰\(view\)를 정의하는 그릇
* 데이터를 전달하고, 어떤 뷰에 그릴거야 라는 것을 한꺼번에 정의할 수 있는 것

컨트롤러를 만들면 dispatcher servlet.xml에서 위에서 만든 컨트롤러 정의해주고 viewResolver를 정의해준다.

dispatcher-servlet.xml`1<context:component-scan base-package="springhello"/>//어노테이션 기반으로 빈을 정의한 것을 읽어오는 역할`

Spring에서 제공하는 Spring MVC의 Controller는 이름이 바로 패스가 된다.`1 <beans:bean name="/index" class="springhello.HelloController"> 2 <beans:constructor-arg name="userDao" ref="userDao"/> 3 </beans:bean>`

ViewResolver 정의하는 코드`1 <beans:bean name="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver"> 2 <beans:property name="prefix" value="/WEB-INF/views/" /> 3 <beans:property name="suffix" value=".jsp"/> 4 </beans:bean>`

* 위의 코드처럼 할 경우, 요청을 한 패스의 이름을 가진 jsp파일에 결과를 전달하게 된다.
* 예시의 경우 “/index“가 패스 이기때문에 index.jsp파일을 찾아서 결과를 전달한다.

WEB-INF하위에 views라는 디렉토리를 만들고 jsp파일 생성한다.

index.jsp 파일`1<%@ page contentType="text/html;charset=UTF-8" language="java" %> 2<html> 3<head> 4 <title>${title}</title> 5</head> 6<body> 7${name}님 하이여 ㅇ 8<form action="/hi" method="post"> 9 <input type="text" name="moron"> 10 <input type="text" name="idiot"> 11 <input type="submit"> 12</form> 13</body> 14</html>`

ViewResolver?

* Controller를 수행한 결과 오브젝트를 /WEB-INF/views/ 밑에 있는 index.jsp에 전달을 해줘\(“/index”라는 url을 타고왔을 때 이러한 반응을 한다.\)
* Controller에서 처리한 결과를 적절한 View에 **매핑해주는 역할**

path가 view의 이름이 될 것이고 이에 해당이 되는 .jsp에 전달하는 식이다.

* /WEB-INF/views 밑에 index.jsp가 viewResolver에 의해 전달이 되고, 거기에 데이터까지 전달이되서 클라이언트에 결과가 나옴
* viewResolver가 특정 리소스를 매핑해주고 그 리소스가 실행이 되서 화면이 나옴

지금부터는 4가지 기능을 하나씩 살펴보자

#### Handler Mapping-&gt; 어떤 컨트롤러 클래스를 실행할 것인지를 url을보고 판단을 내리는것 <a id="Handler-Mapping-&gt;-&#xC5B4;&#xB5A4;-&#xCEE8;&#xD2B8;&#xB864;&#xB7EC;-&#xD074;&#xB798;&#xC2A4;&#xB97C;-&#xC2E4;&#xD589;&#xD560;-&#xAC83;&#xC778;&#xC9C0;&#xB97C;-url&#xC744;&#xBCF4;&#xACE0;-&#xD310;&#xB2E8;&#xC744;-&#xB0B4;&#xB9AC;&#xB294;&#xAC83;"></a>

* BeanNameUrlHandlerMapping\(Default\)-앞에 예시에서 썼던 Handler Mapping
* SimpleUrlHandlerMapping
* RequestMethodHandlerMapping\(Default\)- 3.1 → 현재 가장 중점적으로 사용되는 놈
  * DefaultAnnotationHandlerMapping\(Deprecated\) 3.0버전까지 사용하던 거

SimpleUrlHandlerMapping -&gt; 내가 지정한 여러개의 url들을 직접 Controller라고하는 bean에 property정의로 매핑을 해줌`1 <context:component-scan base-package="springhello"/> 2<beans:bean name="/user" class="springhello.HelloController"> 3 <beans:constructor-arg name="userDao" ref="userDao"/> 4</beans:bean> 5<beans:bean class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping"> 6 <beans:property name="mappings">// handlerMapping을 url에 매핑하는 것 7 <beans:props> -> 여러개 url을 집어 넣을 수 있음 8 <beans:prop key="/getuser">/user</beans:prop>// 안에다가 넣은것은 위에서 정의한 빈의 이름이다. 9 </beans:props> 10 </beans:property> 11</beans:bean>`

이걸 그대로 실행하면 오류가 나는데

두가지 해결방법이 있다.

1. &lt;beans:property name="prefix" value="/WEB-INF/views/" /&gt;여기에 있는 View name을 이용해서 url이랑 연결이 되는데, 이때 Controller에서 ModelAndView에다가 View name을 정의하게 되면 위에 파일이 정상작동한다  ModelAndView modelAndView= new ModelAndView\("user"\);  
2. getuser.jsp라는 새로운 jsp파일을 만든다.

SimpleUrlHandlerMapping는 앞으로 **자주 안쓰게 될 거다.**  
**진짜 옛날 레거시에서 사용하는 방식이란다.**

**RequestMethodHandlerMapping\(Default\)- 3.1** -&gt;**가장많이쓰는 매핑**

* 어노테이션 기반의 HandlerMapping - RequestMethodHandlerAdapter와 항상 연결해서 같이 써야한다.

RequestMethodHandlerAdapter와 묶어서 설명할 예정

#### Handler Adapter <a id="Handler-Adapter"></a>

* SimpleServletHandlerAdapter
* HttpRequestHandlerAdapter\(Default\)-&gt; 거의 안씀
* SimpleControllerHandlerAdapter\(Default\)- 앞에서 사용해봄 implements Controller한 거
* RequestMappingHandlerAdapter\(Default\)- 3.1 -AnnotaionMethodHandlerAdapter\(Deprecated\)

**HttpRequestHandlerAdapter**

* SimpleControllerHandlerAdapter와의 차이는 HttpRequestHandlerAdapter는 return이 void이다
* ModelAndView같은 리턴값을 쓰지 않는 옛날방식

**SimpleServletHandlerAdapter**-&gt; **잊어버려도 상관없다.**

* 정의한 서블릿자체를 빈으로 정의해서 서블릿코드를 변경하지 않고 코드를 그대로 가져다가 쓰는 놈 -기존에 sevlet으로 개발된 코드들을 MVC코드로 전환시 코드수정이 너무 많이 일어남-&gt; 그 서블릿들을 그대로 사용하기 위함
* View와 ViewResolver연결해주는게 필요없음 ,모든게 HandlerAdapter로 끝남

**RequestMethodHandlerMapping와 RequestMappingHandlerAdapter**`1@Controller 2@RequestMapping("/user") 3public class UserController { 4 5}`

* @RequestMapping\("/user"\)처럼 하게되면 “/user”라는 path 요청이 들어왔을 때 RequestMethodHandlerMapping에 의해서 해당 Controller가 찾아짐

`1@Controller 2@RequestMapping("/hello") 3public class HelloController { 4// RequestMappingHandlerAdapter에 의해서 매핑된 메서드 선택됨 5 @RequestMapping 6 public ModelAndView hello(){ 7 ModelAndView modelAndView= new ModelAndView("index"); 8 modelAndView.addObject("title", "제하"); 9 modelAndView.addObject("hello", "서버키고싶당"); 10 return modelAndView; 11 } 12}`

아래 코드 처럼도 가능하다`1@Controller 2@RequestMapping 3public class HelloController { 4// RequestMappingHandlerAdapter에 의해서 매핑된 메서드 선택됨 5 @RequestMapping("/hello") 6 public ModelAndView hello(){ 7 ModelAndView modelAndView= new ModelAndView("index"); 8 modelAndView.addObject("title", "제하"); 9 modelAndView.addObject("hello", "서버키고싶당"); 10 return modelAndView; 11 } 12}`

 `1@Controller 2@RequestMapping("/simple") 3public class HelloController { 4// RequestMappingHandlerAdapter에 의해서 매핑된 메서드 선택됨 5 @RequestMapping("/hello") 6 public ModelAndView hello(){ 7 ModelAndView modelAndView= new ModelAndView("index"); 8 modelAndView.addObject("title", "제하"); 9 modelAndView.addObject("hello", "서버키고싶당"); 10 return modelAndView; 11 } 12}`

이렇게 될경우 /simple/user일 때 해당메서드가 실행이 된다.

@RequestParam

* 알아서 타겟팅해서 파라미터값을 받아옴 -&gt; 조사좀 해보는 걸로

 어떤 컨트롤러를 실행해야하는가? HandlerMapping  
 어떤 메소드를 실행해야 하는 가? HandlerAdapter  
 결과를 view\(.jsp\)와 매핑하기위한 ViewResolver

View Resolver

* InternalResouceViewResolver-&gt;jsp파일에 리소스를 매핑해주는 놈  
* ThymeleafViewResolver
* VelocityViewResolver
* FreeMarkerViewResolver  Thymeleaf,Velocity,FreeMarker 등 템플릿엔진이 있는데, jsp처럼 각 엔진에 적합하게 해석해주는 역할  
* ResourceBundleViewResolver -&gt; view가 해석해주는 정보를 property파일에 담는 것
* XmlViewResolver -&gt; view와 연결해주는 컨트롤러 매핑을 xml에 데이터를 정의하는 것

위에 두개는 별로 활용 안함

* **ContentNegotiatingViewResolver** -&gt; **겁나 많이 활용되는 놈**\*
  * 특정 요청이 왔을 때 **xml,json, jsp 어떤걸로 연결**을 할거냐 **협상**하는 놈
  * 어떤걸로 할지 **판단해주는 Resolver**

`1 2 <beans:bean class="org.springframework.web.servlet.view.ContentNegotiatingViewResolver"> 3 <beans:property name="contentNegotiationManager"> 4 <beans:bean class="org.springframework.web.accept.ContentNegotiationManagerFactoryBean"> 5 <beans:property name="mediaTypes">// 여기서 정의된 것들은 협상이 필요한 것들 6 <beans:props> 7 <beans:prop key="js">application/json</beans:prop>//.js라는 확장자를 가진녀석을 json데이터에대한 컨텐츠 타입을 반환하길 원하는 요청으로 판단할거다 8 <beans:prop key="xml">application/xml</beans:prop>//.xml이라는 확장자를 가진 녀석을 xml데이터에대한 컨텐츠 타입을 반환하길 원하는 요청으로 판단할거다 9 </beans:props> 10 </beans:property> 11 </beans:bean> 12 </beans:property> 13 <beans:property name="defaultViews">// 확장자가 있을 때 반응하는 곳 14 <beans:list> 15 <beans:bean class="org.springframework.web.servlet.view.json.MappingJackson2JsonView" />//json으로 반응 16 <beans:bean class="org.springframework.web.servlet.view.xml.MappingJackson2XmlView" />//xml로 반응 17 </beans:list> 18 </beans:property> 19 <beans:property name="viewResolvers">// 확장자가 없을 때 반응해줌 20 <beans:list> 21 <beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"> 22 <beans:property name="prefix" value="/WEB-INF/views/" /> 23 <beans:property name="suffix" value=".jsp" /> 24 </beans:bean> 25 </beans:list> 26 </beans:property> 27 </beans:bean>`

어떤요청에 따라 어떤 뷰와 연결해주는 형식으로 협상을 해주는 Resolver가 ContentNegotiatingViewResolver

/////////////////////////////////////////////////////////////////////////////////////////////////////

1. 이후 context Listener 추가해줌

cf\) context Listener

: 요청이 들어왔을 때, 그 요청에 대한 처리를 listen하는 것

Q. \[요청에 대한 처리를 listen하는 것\] - 무슨 의미??

&lt;listener&gt;

&lt;listener-class&gt;org.springframework.web.context.ContextLoaderListner&lt;/listener-class&gt;

&lt;/listener&gt;

여기까지가 web.xml에 등록된 스프링 MVC의 기본적인 내용

여기에

dispatcher servlet,

root web application context,

context loader listener

이 3개가 들어가야 한다.

* 그 전 spring mvc lifecycle 그림에 대한 설명
* Q. 어떻게 우리 코드가 돌아갈까?

A. 돌아가는 원리가 이 lifecycle 구조

여기서 controller\[조작부\]가 우리가 구현할 것

위 view resolver도 dispatcher servlet에 오면 된다.

Q. 무슨 말이지??????

cf\) jsp : Java 언어를 기반으로 하는 Server Side 스크립트 언어

* jsp기반으로 설명하자면

xml기반으로 bean을 등록할 것이다.

Q. 어떤 bean을 등록할 것인가?

A. &lt;beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"&gt;

&lt;/beans:bean&gt;

Q. 왜 등록하는 거지?

InternalResourceViewResolver 라는 것을 찾으려고

Q. InternalResourceViewResolver 가 뭘까?

A. 위 life cycle에 나온 그것

* 앞에서 말한대로 view resolver는 위 하나만 있는 것이 아니다

Q. 이런 말을 안했는데...?

Q. view Resolver의 정확한 역할이 뭐지???????

진짜 처리 결과를 보내주는 역할인가????

* 그래서 추가하는 것들

&lt;beans:property name="prefix" value="/WEB-INF/views/" /&gt;

// view라는 폴더에 넣어주는 것

&lt;beans:property name="suffix" value=".jsp"/&gt;

// suffix는 jsp라는 확장자로 할 것

이렇게 한 후 WEB-INF안에 views라는 폴더를 만듬

위의 의미

* 말그대로 어떤 뷰를 찾을 것인지

Q. 무슨 의미지??????

정리

* dispatcher servlet에서

handler mapping을 통해

controller를 찾는다.

* 실제로 돌아가는 Handler Mapping 요소들의 목록은 다음과 같다.

1. BeanNameUrlHandlerMapping\(Default\)

: Bean의 이름이 Url이고,

이 url을 기반으로 handler mapping을 하는 것임

1. SimpleUrlHandlerMapping

: 간단하게 url로 handler mapping 하는 것

1. RequestMethodHandlerMapping

: 이것이 오늘날의 스프링의 기본,

스프링 3.1에서 쓰이는 기본적인 매핑

실제로 어떻게 쓰이는지에 대해서는 위

simpleUrlHandlerMapping 과

RequestMethodHandler Mapping 2가지를 이용하여

알아볼 것이다.

단계

1. Dispatcher servlet에서 요청을 받으면

handler Mapping을 찾는다

이후 handler mapping이

컨트롤러를 찾고,

1. 찾은 controller

handler adapter를 통해서 컨트롤을 하여

로직을 수행 후

돌아와서 view를 찾고,

1. view resolver를 통해서 view를 해결해주고

Q. \[view를 해결해준다\]의 의미가 무엇인가???

view를 넘겨준다.

이때 view가 흔히 말하는 jsp, html

* view의 종류는 굉장히 많다.

이제 할 것

servlet 기반의 서버를 spring으로 바꾸는 것을 해볼 것이다.

이제

handler mapping과 handler adapter 2개가 필요

1. handler mapping

&lt;beans:bean class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping"&gt;

&lt;beans:property name="mappings"&gt;

&lt;beans:props&gt;

// 값을 넣어줄 것임

&lt;/beans:props&gt;

&lt;/beans:property&gt;

&lt;/beans:bean&gt;

Q. 뭔 값을 넣어준다는 거지??

Q2. 저 property와 props는 무슨 의미지?

이제 서블릿 기반으로 동작된 것들을

바로 스프링으로 쓰기 위해서는 다음과 같이 써야 한다.

Q. 왜 이렇게 써야 하나??

A. 네이버만 하더라도 엄청난 페이지가 있고,

페이지의 수와 비례해서 서블릿이 존재한다.

만약 이러한 서블릿들을 스프링으로 바꾸려면

엄청난 비용이 필요

그래서 개발자들은

서블릿이라는 클래스 자체는 바꾸지 말고,

dispatcher servlet이라는 것으로 처리를 할 수 있게 해준다.

이렇게 나온 것이 simpleServletAdapter

여기다가 urlhandlermapping을 통해서

메핑을 해준다.

&lt;beans:bean id="hi" class="HelloServlet" /&gt;

&lt;beans:bean id="hi2" class="HelloServlet" /&gt;

&lt;beans:bean id="hi3" class="HelloServlet" /&gt;

&lt;beans:bean class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping"&gt;

&lt;beans:property name="mappings"&gt;

&lt;beans:props&gt;

&lt;beans:prop key="/hello"&gt;hi&lt;/beans:prop&gt;

&lt;beans:prop key="/hello2"&gt;hi2&lt;/beans:prop&gt;

&lt;beans:prop key="/hello3"&gt;hi3&lt;/beans:prop&gt;

&lt;/beans:props&gt;

&lt;/beans:property&gt;

&lt;/beans:bean&gt;

&lt;beans:bean class="org.springframework.web.servlet.handler.SimpleServletHandlerAdapter"&gt;

&lt;/beans:bean&gt;

이렇게 서블릿을 변경하지 않고, xml만 가지고도 수정할 수 있었다.

이번에는 bean으로 등록한 서블릿

&lt;beans:bean id="hi" class="HelloServlet" /&gt;

&lt;beans:bean id="hi2" class="HelloServlet" /&gt;

&lt;beans:bean id="hi3" class="HelloServlet" /&gt;

을 없애고 사용해본다.

즉, 서블릿을 빈으로 등록하지 않고, 해볼 것이다.

Q. 무엇을 사용하여?

A. @Controller라는 Annotation을 이용하여

먼저 \[java\] 폴더 안에대가 패키지 하나\(ex. hello\)를 생성하여

그 아래에 서블릿 클래스들을 넣어준다.

이후`1<context:component-scan base-package="hello"/>`

처럼 코드 안에 패키지 이름을 적어준다.

 그런 이후 각 서블릿 클래스에

@Controller\(“이름”\) 을 붙인다.

ex.

 @Controller\(“hi”\)

@Controller\(“hi2”\)

 etc….

이런 방식으로 Annotation을 인식할 수 있다.

사실 @Component로도 할 수 있지만,

굳이 @Controller를 사용한 이유는

MVC패턴의 컨트롤러라는 것을 정의해주기 위해 넣어준 것

근데 완벽하게 스프링으로 바꾼 것은 아니다.

스프링으로 바꿨지만 아직까지는 서블릿에 종속적임

근 미래에 서블릿이라는 것을 완벽하게 제거해야 한다.

즉, 서블릿이란 것을 controller로부터 가리고,

스프링에서 지원하는 것을 써야한다.

이유

: 스프링 안에 서블릿은 단 하나밖에 필요하지 않기 때문

어쨌거나 저쨌거나.

위 내용들은 서블릿에서 스프링으로 넘어오는 사람들을 위한

임시방편

그래서`1 <context:component-scan base-package="hello"/> 2 <beans:bean class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping"> 3 <beans:property name="mappings"> 4 <beans:props> 5 <beans:prop key="/hello">hi</beans:prop> 6 <beans:prop key="/hello2">hi2</beans:prop> 7 <beans:prop key="/hello3">hi3</beans:prop> 8 </beans:props> 9 </beans:property> 10 </beans:bean> 11 <beans:bean class="org.springframework.web.servlet.handler.SimpleServletHandlerAdapter"> 12 </beans:bean>`

를 다 지우고,

서블릿 클래스 안의 어노테이션들을 다 지운다.

이후, java 폴더 안에 새로운 패키지\(ex. springhello\)를 만든다.

그리고, dispatcher servlet.xml 의 base-package를

방금 만든 것으로 바꿔준다.

즉, bean을 인식할 수 있는 패키지를

방금 만든 것으로 바꿔준것

그리고 그 패키지 내에 새로운 controller\(ex.HelloController\)를 만들 것

근데 이 컨트롤러는 HttpRequestHandler를 implements한 것이다.`1public class HelloController implements HttpRequestHandler { 2 @Override 3 public void handleRequest(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { 4 5 } 6}`

그리고 기존에 만든 서블릿 클래스 바디의 내용을 붙여넣는다.`1public class HelloController implements HttpRequestHandler { 2 @Override 3 public void handleRequest(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { 4 int number = Integer.parseInt(request.getParameter("number")); 5 response.getWriter().println("Hello world"+ " " + (number)); 6 } 7}`

이후 Controller라는 것을 알려주기 위해

위에 @Controller를 추가해준다.`1@Controller("/hello") 2public class HelloController implements HttpRequestHandler { 3 @Override 4 public void handleRequest(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { 5 int number = Integer.parseInt(request.getParameter("number")); 6 response.getWriter().println("Hello world"+ " " + (number)); 7 } 8}`

이때 hello2 나 hello3 는 없기 때문에 뜨지 않는다.

지금까지 이런 방식으로

Servlet을 Controller로 Migration한 작업까지 해보았다.

\[HttpRequestHandlerAdapter를 해본 것\]

그렇지만,

 서블릿조차 보기 싫을 경우

스프링3.1에서 지원하는 기능을 사용해본다.

\[RequestMethodHandlerAdapter를 해볼 것임\]

완벽하게 Annotation 기반으로…

먼저

아까 만들어준 views 폴더 안에

index.jsp를 만들어준다.

이후 이 안에`1<%@ page contentType="text/html;charset=UTF-8" language="java" %> 2<html> 3<head> 4 <title>${title}</title> 5</head> 6<body> 7${hello} 8</body> 9</html>`

붙여 넣어준다.

그리고

HelloController 에 가서 HttpRequestHandlerAdapter를 사용하지 않고,

RequestMethodHandlerAdapter 사용해볼 것이다.

먼저 HelloController 바디 내부를 다 밀어버린다

+ 컨트롤러 안의 이름도 뺌`1@Controller 2public class HelloController { 3}`

이후 완벽하게 Annotation할 것

어떻게?

@RequestMapping을 넣어준다.`1@Controller 2@RequestMapping 3public class HelloController { 4} 5`

이후 바디 안에 다시

@RequestMapping을 넣어준 후

그 안에 이름을 넣어줌`1@Controller 2@RequestMapping 3public class HelloController { 4 @RequestMapping("/hello") 5} 6`

그 다음 String을 반환하는 메소드를 만들어 볼 것이다.

이때 반환되는 String은 아까 만든

jsp파일의 이름이다.`1@Controller 2@RequestMapping 3public class HelloController { 4 @RequestMapping("/hello") 5 public String hello(){ 6 return "index"; 7 } 8}`

이렇게 쓰면

아까 dispatcher-servlet.xml에서`1 <beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"> 2 <beans:property name="prefix" value="/WEB-INF/views/" /> 3 <beans:property name="suffix" value=".jsp"/> 4 </beans:bean> 5`

에서의

InternalResourceViewResolver 가

/WEB-INF/views/ 안에 있는

확장자가 .jsp 인 애들 중 index를 찾아서 넣어줄 것

바로 그 viewResolver가 어떤 view일지를 찾아주는 것

이후에는 index.jsp의`1<html> 2<head> 3 <title>${Title}</title> 4</head> 5<body> 6${hello} </body> 7</html>`

에서${Title} 과 ${hello} 라는 변수에 값을 넣는 것을 해볼것

만약`1<html> 2<head> 3 <title>${Title}</title> 4</head> 5<body> 6${hello} hi google 7</body> 8</html> 9`

라면

그냥 hi google만 뜰 것임

아무튼`1@Controller 2@RequestMapping 3public class HelloController { 4 @RequestMapping("/hello") 5 public String hello(){ 6 return "index"; 7 } 8}`

와 같은 방식이 실무에서 가장 많이 쓰이는 방식임

다음 예고

1. Controller를 이용한 간단한 서버 구현

ex. 파일 업로드, 간단한 세션 관리 등등.

2. web\_app 폴더 안에 있는 ㅈ같은 xml 파일 지우기

