---
description: '- 정리한 사람 : 장재혁: obg2546@naver.com -> 고마워요 째스!!!'
---

# DI 와 각종 패턴

## 1.  프레임 워크란?

* 코딩을 하다가 나온  개발자들의 노하우들 을 모아서 잘 정의된 이론으로 만들어 놓은 것이

   **패턴,** **디자인 패턴**이다  

* 이렇게 만들어진 여러가지 패턴들을 중복되지 않게 모아서

   잘 구현된 구현체로 만든 것이 **프레임 워크**이다.  

* **개발을 함에 있어서 우리는 특정언어를 선택하고,**

   **그 도메인에 맞게 프레임워크를 사용하게 된다.**  

* 우리가 개발할 언어는 자바이고 우리가 배우게 될 프레임워크는 Spring이다.

## Known to Unknown

## 2.개발 방법론

### 1. Object Oriented\(객체지향\)-&gt; 객체지향 자체 원리를 다룬것

1\)캡슐화

* **비슷한 역할**을 하는 속성과 메소드들을 하나의 클래스로 모은 것
* 은닉: 캡슐 내부의 로직이나 변수들을 감추고 외부에는 기능만을 제공하는 것

2\)추상화

* 복잡한 자료, 모듈, 시스템 등으로부터

   핵심적인 개념 또는 기능을 간추려 내는 것을 말한다\(TMI적인 요소는 최대한 줄이는 것\)

* 어떤 실체로부터 공통적인 부분이나 관심 있는 특성들만 한곳에 모은 것

3\)상속

* 상위 클래스의 특성을 하위 클래스에서 물려받는 것
* 상위 클래스를 하위 클래스에서 상속받게 되면 클래스의 멤버변수나 메소드를 그대로 물려 받음
* 클래스를 재사용, 확장
* 코드 재활용이 가능하고 생산성 높으며 유지보수하기 좋아짐

4\)다형성

* 하나의 변수명, 함수명 등이 상황에 따라 다른 의미로 해석될 수 있다는 것
* 오버라이딩과 오버로딩으로 나뉨 
* 오버로딩:하나의 클래스에서 같은 이름의 메소드들을 여러 개 가지고 있는 것
* 오버라이딩: 상위 클래스의 메소드를 하위 클래스에서 똑같은 이름\(메서드 시그니처\)으로 재정의 하는 것

### 2. Object Oriented Design Principle\(객체지향 설계원칙\) - SOLID원칙

### → **\[객체 지향을 사용해서 어떻게 하면 잘 개발할 수 있을 까\]**    라는 노하우를 담은   어찌보면 패턴과 유사한 원칙\(객체지향 개발을 하면서 반드시 숙지해야하는 원칙\)

1. **SRP\(Single Responsibility Principle, 단일 책임성 원칙\)**
   * 의미 : **하나의 객체**는 **한가지 일에 집중**해야 한다
   * 컴포넌트\(구성요소\)마다 하나의 잘 정의된 책임을 가지며,

      관련 없는 기능을 합치지 않는다.

     즉 **하나의 관심사에만 집중하도록** 설계한 것

   * 응집도 높게 → 내가 **맡은 일을 내가 꽉쥐고** 있는 것
   * 결합도 낮게 → 두 객체 사이의 **coupling 상태를 느슨**하게 하는 것
   * **의존성 낮아짐**
   * decoupling을 극대화한 것, decoupling을 극대화할 시 성능에 영향을 줄 수 있다 
2. **OCP\(Open/Closed Principle, 개방/폐쇄 원칙\)**
   * 의미:수정에는 닫혀있고, 확장에는 열어두어라
   * 클래스는 **확장에는 개방적** → 클래스는 **추상적**으로 만들어야 한다.\(추상→구체 확장\)
   * **수정에는 폐쇄적**이어야 한다. **\(기존의 코드수정x\)**
   * Q. 왜 이렇게 해야 하는가?

      A, 만약 어떤 메소드를 수정해서 사용할 때,

      그 메소드가 직접 수정이 되면

      나중에 필요할 때 골치아파지기 때문 ,

      **수정이 일어나면 전파되기 쉽기 때문이다.**  
3. **LSP\(Liscov Substitution Principle, 리스코프 치환 원칙\)**
   * 의미 :어떤 객체는 그것의 상위클래스로 치환되었을 때에도 올바르게 작동되어야 한다.
   * 논란점

      : ‘올바르게’라는 의미가 2가지로 갈림

     1. 코드 자체가 변하지 않는다는 의미
     2. 코드가 문제없이 작동한다는 의미 
4. **ISP\(Interface Segregation Principle, 인터페이스 분리 원칙\)**
   * 인터페이스는 깔끔하고 간결해야 한다.
   * 의미:거대한 하나의 범용 인터페이스 X

     —&gt; 한 가지 책무가 잘 정의된 여러 인터페이스

   * 인터페이스: 추상메소드들의 집합 
5. **DIP\(Dependency Inversion Principle, 의존성 뒤집기/역전 원칙\)**
   * 의미:인터페이스로 의존 관계를 역전시킨다.
   * 객체에 의존하지 않고, 객체들 사이에 인터페이스를 만들어 인터페이스에 의존하게 함
   * 의존성 주입\(DI\)은 의존성 역전 원칙\(DIP\)을 구현하기 위한 방법 중 하나

A. 고수준\(High-Level\)의 모듈은 저수준\(Low-Level\)의 모듈에 의존하면 안된다. 둘다 추상화에 의존해야한다. B. 추상은 세부사항\(Details\)에 의존해서는 안된다.

B. 세부사항은 추상에 의존해야 한다.

1,4,5 원칙\(필수\)\*/3,4 원칙\(선택\)

### 3. TDD\(켄트벡, Test Driven Development\) → 기존의 개발 패러다임을 많이 바꾼 개발방식

핵심 패러다임 두개 애자일 환경에서 개발하기 위한 두가지 패러다임

* Known To Unknown\(아는 것에서 모르는 것으로\)
* Separate of Concern\(관심사의 분리\)

**애자일**이란?

* 애자일은 기존에 소프트웨어 개발을 할 때 사용하던 '구닥다리 일 하는 방식'을

  오랜 기간에 걸쳐 소프트웨어 제품을 만들어오던 거장들이 소프트웨어의 소프트 한 면을

  살려서 정의 한 일종의 '유연하게 일하는 방식' 이라고 볼 수있음.

* 애자일 이라는 용어 자체가 '기민한', '재빠른', '민첩한' 이라는 뜻을 가지고 있음
* 간단하게 말하자면 **빠르게 변화하는 개발환경**이라는 것

### Known To Unknown

* 알고 있는 것과 모르고 있는 것을 판단한다.
* 모르고 있는 것을 알고 있는 것으로 부터 도출한다.

ex\)

알고 있는 것? -요구사항

-디자인

모르고 있는 것?

-어떤 툴로 개발할까?

-어떤언어로 개발할까?

-어떤 플랫폼에서 서비스가 되어야하는가?

이런 상태라면

알고 있는 것? 요구사항 기획 디자인 어떤 플랫폼에서 서비스가 되어야하지? 앱? 웹?  
 =&gt;  
    1\) 웹 어떤언어로 개발하지? java  
    2\) 어떤 툴로 개발할까? intelliJ  
    3\) 어떤 framework으로 개발하지? Spring

모르고 있는 것?

이런식으로

알고 있는 것으로 모르고 있는 것을 도출하여 알고 있는 것으로 바꾸는게

**Known To Unknown**

### 관심사의 분리

* 기존 테스트를 통과할 수 있도록 로직을 유지하면서 기능을 추상화하면서 구조를 짜아 나간다. 
* 이렇게 테스트를 통과할 수 있도록 만들면서

   코드의 관심사를 분리하는 단계를

   리펙터\(Refactor\) 단계 라고 한다. \(블루 단계\)  

* 구현된 부분은 테스트를 돌려 잘돌아가는 것을 확인 했으니,

  구현되지 않은 부분으로 관심사가 이전됨

정리하자면 우리가 알고있는 지식을 테스트 코드에 넣음  
 그리고 그 테스트코드를 완성시키는 과정에서 우리가 모르고있는 지식들을 알게끔 도출함,  
 테스트코드가 완성된 순간에 새롭게 알게된 지식과 우리가 알고있는 지식에 대한 결합을 함  
  그리고 우리가 모르고 있는 부분을 다시찾아서 해당되는 부분에 관심사를 이전시키고  
   다시 테스트코드를 작성하는 과정을함

//////////////////////////여기까지가 기초지식과 TDD방법론///////////////////////////////////////////

## Dao 실습한 내용들 정리

### 실습하면서 나온 내용들

### 1. Design Pattern

* Template Method pattern
* Factory Method Pattern
* Strategy Pattern
* Template/Callback Pattern

### 2.DI\(IoC\)

* Inversion Of Control\(제어의 역전\)
* Dependency Injection\(의존성주입\)
* Dependency Lookup

### 테스트코드에서 해야할일

* 알고있는 것을 테스트코드로 구현

  그리고 검증

PreparedStatement와 statement의 차이 =&gt; PreparedStatement는 쿼리문장의 재활용 가능

요구사항

* 이미 저장되어잇는 사용자 정보를 ID를 주면

  이름과 패스워드를 가지고 오는 프로그램을 만들어줘

지금 우리가 알고 있는 것 - 요구사항 하나만 알고 있음

우리가 사용할 언어는 ? java

우리가 사용할 툴은? Intellij

    
  
  
  cf\)   
  Q. Dao란?  
  A.  DB에 접근하는 객체

1. TDD로 개발할 것이기 때문에 UserDaoTest클래스를 하나 만든다

우리가 알고있는 도메인은 뭔가?  
 -&gt;  ID를 주면 가져온다

```text
public class UserDaoTest {
    public void get(){

    }
}
```

```text
import org.junit.Test;

public class UserDaoTest {
    // 이미 저장되어잇는 사용자 정보를 ID를 주면 
    // 이름과 패스워드를 가지고 오는 프로그램을 만들어줘
    @Test
    public void get(){
        //우리가 알고있는 도메인
        //DB에 접근하는 Dao를 만들고
        UserDao userDao = new UserDao();
        //ID를 주면 사용자 정보를 가져오는
        User user = userDao.get(id);
    }
}
```

테스트를 해야하니까 검증하는 코드 작성

```text
    public void get(){
        //실제로 DB안에 들어있는 테스트 가능한 데이터
        Integer id=1;
        String name="hi";
        String password="jihwan";
        UserDao userDao = new UserDao();
        User user = userDao.get(id);
        //검증하는 코드 
        assertThat(user.getId(), is(id)); <-우리가 테스트하려는 id와 같아야해
        assertThat(user.geName(), is(name)); <-우리가 테스트하려는 name과 같아야해
         assertThat(user.getPassword(), is(password)); <-우리가 테스트 하려는 password와 같아야해
    }
public class User {
    private Integer id;
    private String name;
    private String password;

    public Integer getId() { return id; }
    public void setId(Integer id) { this.id = id; }
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public String getPassword() { return password; }
    public void setPassword(String password) { this.password = password; }
}
```

우리가 알고있는 도메인과 그 도메인의 행위와 그것을 테스트할 수 있는 코드를 짰다.

우리의 관심사는 UserDao get메소드에 이전됨

자바에서 DB에서 데이터를 받아오는 코드

```text
import java.sql.*;

public class UserDao {
    public User get(Integer id) throws ClassNotFoundException, SQLException {
    
        //데이터는 어디에 있지? =>mysql
        //mysql driver 로딩
        Class.forName("com.mysql.cj.jdbc.Driver");
        
        // connection 맺고
        Connection connection
               = DriverManager
                 .getConnection("jdbc:mysql://localhost/hellooo", "root", null);
        
        // query만들고
        PreparedStatement preparedStatement=connection.prepareStatement("select id, name, password from user where id=?");
        preparedStatement.setInt(1, id);
        
        // query를 실행하고
        ResultSet resultSet=preparedStatement.executeQuery();
        resultSet.next();
        
        // 결과를 User 에 잘 매핑하고
        User user = new User();
        user.setId(resultSet.getInt("id"));
        user.setName(resultSet.getString("name"));
        user.setPassword(resultSet.getString("password"));
        
        // 자원을 해지하고
        resultSet.close();
        preparedStatement.close();
        connection.close();
        
        // 결과를 리턴
        return user;
    }
}
```

우리는 get이라는 메소드만 제공을 할 것이고 코드가 중복없이 깔끔하기 때문에 현재 코드에는 아무런 문제가 없다.

★요구사항 해결★

우리는 지금 jar 파일로만들어서 배포해야 하는 상황

### 배포하는 방법

### Bulid\(배포하기 위한 과정\)

### → 자동화가 필요함\(저걸 언제 수동으로 합니까\)

### → Ant\(빌드를 자동화하기위한 툴\)

* clean:기존에 컴파일되어 있던 오래된 클래스들을

  지우고

* javac: 자바로된 소스코드를 컴파일하고
* test:테스트코드를 통해 검증을 하고
* packaging\(jar, war, ear\)
* deploy:만든파일을 전달하는 과정\(고객에게 전달, 서버에 올리기\)Maven\(xml 기반 빌드툴\)

### Gradle → 영상다시보기

* Groovy Based\(Language\) - Groovy 기반으로 되어 있음
* Easy Extension 
* Wrapper\(Remove Gradle Dependency\)
* Support Maven, Ant, Ivy - Maven, Ant, Ivy를 지원함

요구사항

* DB에 직접 사용자 등록하니까 불편해. 사용자 추가기능 만들어줘

```text
public class UserDaoTest {
 // 필드 같이 쓰는 걸로
        String name="hi";
        String password="jihwan";
    @Test
    public void get() throws SQLException, ClassNotFoundException {
        Integer id=1;

        UserDao userDao = new UserDao();
        User user = userDao.get(id);

        assertThat(user.getId(), is(id));
        assertThat(user.getName(), is(name));
        assertThat(user.getPassword(), is(password));
    }
    @Test
    public  void insert() throws SQLException, ClassNotFoundException {
        //확인해보니 해당되는 DB는 자동으로 아이디기 할당되는 형식임

        //등록할 user를 만들고
        User user = new User();
        user.setName(name);
        user.setPassword(password);
        // Dao 생성하고
        UserDao userDao=new UserDao();
        //추가기능 사용
        userDao.insert(user);
        assertThat(user.getId(), greaterThan(0));
        // 검증하기
        User insertUser= userDao.get(user.getId());<-할당된 아이디 불러오기
        assertThat((insertUser.getName(), is(name));
        assertThat(insertUser.getPassword(), is(password));
    }
}
```

개발자가 가장 잘하는 습관 ctrl+C and ctrl+V → userDao의 get에 있는 부분 insert에 복붙

```text
public void insert(User user) throws ClassNotFoundException, SQLException {
    Class.forName("com.mysql.cj.jdbc.Driver");
    Connection connection= DriverManager.getConnection("jdbc:mysql://localhost/hellooo", "root", null);

    // Statement.RETURN_GENERATED_KEYS:  Resultset에 키값을 받아올 수 있게 함

    PreparedStatement preparedStatement=connection.prepareStatement("insert into user(name, password)  values(?,?) ",Statement.RETURN_GENERATED_KEYS);
    preparedStatement.setString(1, user.getName());
    preparedStatement.setString(2,user.getPassword());
    preparedStatement.executeUpdate();

    ResultSet resultSet=preparedStatement.getGeneratedKeys();
    user.setId(resultSet.getInt(1));

    resultSet.close();
    preparedStatement.close();
    connection.close();
}
```

개발자는 게을러야 한다.

복붙을 했기 때문에 코드 중복이 포함되었을 것

→여기서 적용하는 리팩토링 방법 

* 정확히 똑같은 것을 찾아보자
* mysql드라이버를 로드하고 connection을 맺는 부분, 자원을 해지하는 부분이 똑같다

```text
//이부분이 정확히 똑같기 때문에 메소드를 추출해서 중복되는 부분을 제거한다.
Class.forName("com.mysql.cj.jdbc.Driver");
Connection connection= DriverManager.getConnection("jdbc:mysql://localhost/hellooo", "root", null);
```

   즉, **메소드 추출\[Method Extract\]**을 한다. 

```text
import java.sql.*;
public class UserDao {
    private Connection getConnection() throws ClassNotFoundException, SQLException {
        Class.forName("com.mysql.cj.jdbc.Driver");
        return DriverManager.getConnection("jdbc:mysql://localhost/hellooo", "root", null);
    }
    public User get(Integer id) throws ClassNotFoundException, SQLException {
        Connection connection = getConnection();
        PreparedStatement preparedStatement=connection.prepareStatement("select id, name, password from user where id=?");
        preparedStatement.setInt(1, id);
        ResultSet resultSet=preparedStatement.executeQuery();
        resultSet.next();

        User user = new User();
        user.setId(resultSet.getInt("id"));
        user.setName(resultSet.getString("name"));
        user.setPassword(resultSet.getString("password"));

        resultSet.close();
        preparedStatement.close();
        connection.close();
        return user;
    }

    public void insert(User user) throws ClassNotFoundException, SQLException {
        Connection connection = getConnection();

        PreparedStatement preparedStatement=connection.prepareStatement("insert into user(name, password)  values(?,?) ",Statement.RETURN_GENERATED_KEYS);
        preparedStatement.setString(1, user.getName());
        preparedStatement.setString(2,user.getPassword());
        preparedStatement.executeUpdate();

        ResultSet resultSet=preparedStatement.getGeneratedKeys();        
        resultSet.next();

        user.setId(resultSet.getInt(1));

        resultSet.close();
        preparedStatement.close();
        connection.close();
    }
}
```

요구사항

* 현재는 제주대학교 에서 사용하고 있는데 한라대에다가 납품해야한데...

  거기는 DB가 달라.. 어떡하지? 

```text
//이부분이 정확히 똑같기 때문에 메소드를 추출해서 중복되는 부분을 제거한다.
Class.forName("com.mysql.cj.jdbc.Driver");<-여기와
Connection connection= DriverManager.getConnection("jdbc:mysql://localhost/hellooo", "root", null)<-여기가 다름
```

* DB의 위치와  DB조차 다른 상황임
* 우선 getConnection 부분에서 나는 뭐가들어올지 모른다.
* 뭐가 들어올지 모르니까 일단 추상화를 해보자

```text
 public abstract  Connection getConnection() throws ClassNotFoundException, SQLException; /*{
        Class.forName("com.mysql.cj.jdbc.Driver");
        return DriverManager.getConnection("jdbc:mysql://localhost/hellooo", "root", null);
    }*/
```

**특정한 메소드에 뭐가 들어가야될 지 모르는 상황**

→ 이럴때는 **추상화**를 하면 된다. 결정을 스스로 못하는 상황이니 뭐가 들어올지 모름

### 추상화 기법

* 특정한 메소드에 뭐가 들어가야할지 모름

  모르면 뭐? 그때 추상화를 함

  추상화하는 방법은? 그때 abstract메소드를 만듬

메소드가 abstract이기 때문에 클래스도 추상클래스여야함

```text
public abstract class UserDao{
```

UserDaoTest쪽에서는 클래스가 추상클래스이기 때문에 **UserDao를 상속받은 Dao를 삽입**해줘야함

```text
   UserDao userDao = new jejuUserDao();
```

제주UserDao

```text
public class jejuUserDao extends UserDao {
    @Override
    public Connection getConnection() throws ClassNotFoundException, SQLException {
        Class.forName("com.mysql.cj.jdbc.Driver");
        return DriverManager.getConnection("jdbc:mysql://localhost/hellooo", "root", null);
    }
}
```

한라 UserDao

```text
public class HallaUserDao extends UserDao {
    @Override
    public Connection getConnection() throws ClassNotFoundException, SQLException {
        Class.forName("com.mysql.cj.jdbc.Driver");
        return DriverManager.getConnection("jdbc:mysql://localhost/hellooo", "root", null);
    }
}
```

요구사항 전부 클리어

추상화를 했더니 **Template Method pattern**과 **Factory Method Pattern**이 저절로 적용이됨

### Template Method pattern

```text
public abstract class Super{
  public void templateMethod(){
  //기본알고리즘 코드
  hookMethod();
  
  abstractMethod;
  ....
  }
}

public class Sub1 extends Super{
  protected void hookMethod(){
.....
  }
  public void abstractMethod(){<-행위에 대한 결정을 자식이 해줌
  }
}
```

* **상속 기반**의 추상화 패턴
* **클래스가 abstract되는 패턴**
* 구체적인 것은 자식이 결정해준다.
* **메소드 행위에 대한 결정을 자식이 해준다**.&lt;- **Template Method pattern**

### Factory Method Pattern

* **상속 기반의 추상화 패턴**
* **템플릿 메소드 패턴의 생성자판**이라고 생각하면 이해하기 쉬울 것
* UserDao의 getConnectionMethod\(\)는 **Connection을 생성해서 반환**해주는 메소드
* **생성되는 Connection은 UserDao의 자식들이 결정**해줌
* **특정 오브젝트를 결정하는 것을 자식 오브젝트가 해준다.**
* dependency된 오브젝트를 자식이 결정해준다.

요구사항

* 상품을 조회, 등록했으면 좋겠어.

요구사항 분석

* 사용자를 조회, 등록하는 UserDao가 있으니
* 상품을 조회, 등록하는 ProductDao도 있을 것
* 그렇게 되면 테스트 하는 ProductDaoTest도 만들어야 할 것이고HalloProductDao와 jejuProductDao도 만들어야 할 것임

그러고 봤더니

상품을 조회하는 Dao를 만들면 HallaUserDao의 getConnection과 HallaProductDao의 getConnection의 **중복이 일어남** 코드중복 발생

어떻게 리팩토링 해야할 것인가?

-&gt;메소드 추상화 하기 전 과거로 돌아가보자

* getConnection메소드는 UserDao뿐만아니라 ProductDao 도 같이 사용함
* **Extract를 메소드에 의해서가 아닌 클래스로 해야한다. - Q. why? A.**둘이 같이 써야하기 때문에 -&gt;getConnection을 리팩토링 → Extract Delegate을 한다. -&gt;클래스로 만들어 따로 빼낸다.

  ```text
  public class ConnectionMaker {
      public connectionMaker() {
      }

      public Connection getConnection() throws ClassNotFoundException, SQLException {
          Class.forName("com.mysql.cj.jdbc.Driver");
          return DriverManager.getConnection("jdbc:mysql://localhost/hellooo", "root", null);
      }
  }
  ```

-&gt;ProductDao와 UserDao는 connectionMaker를 사용하면 해결됨 하지만, 직전의 요구사항을 다시 해결해야함

* 한라대 납품하는 것은 어떻게 할 것인가?
* 다시 메소드 안에 뭐가 들어갈 지 모르기 때문에 추상화

  ```text
  public class ConnectionMaker {
      public connectionMaker() {
      }

        abstract public Connection getConnection() throws ClassNotFoundException, SQLException;
     /*{
          Class.forName("com.mysql.cj.jdbc.Driver");
          return DriverManager.getConnection("jdbc:mysql://localhost/hellooo", "root", null);
      }*/}
  ```

* 추상화된 메소드만 존재하고 있음\(추상클래스는 추상화된 것과 추상화 안된 부분으로 구성됨\)
* 인터페이스로 바꿈

```text
public interface ConnectionMaker {

    public Connection getConnection() throws ClassNotFoundException, SQLException; /*{
        Class.forName("com.mysql.cj.jdbc.Driver");
        return DriverManager.getConnection("jdbc:mysql://localhost/hellooo", "root", null);
    }*/
}
```

특정 객체에서 다른 객체에 대해 new를 사용하게되면 dependency\(의존성\)가 발생함

```text
private final ConnectionMaker conntionMaker =new JejuConnectionMaker();
```

* UserDao와 jejuConnectionMaker간에 dependency\(의존성\)가 발생
* 나는 ConnectionMaker의 기능만 사용하고 싶고JejuConnectionMaker에 대한 의존성을 가지고 싶지 않음

  new 한 부분을 UserDao가 직접하고 싶지않아

```text
`private final ConnectionMaker conntionMaker;
 public UserDao(ConnectionMaker conntionMaker){
       this.conntionMaker=conntionMaker;
 }
```

생성자를 통해 conntionMaker를 받아올거야 → userDao를 사용하는 쪽에 conntionMaker에 대한 의존성을 던진다 → 클라이언트\(UserDaoTest\)에 의존성을 던짐-&gt; 클라이언트\(UserTest\)가 의존성을 주입해 주어야한다.

정리하면

1. UserDao와 ProductDao가 getConnection을 같이 쓰기 위해서 메소드단위가 아닌 클래스 단위로Extract함
2. 제주대와 한라대의 getConnection이 다르기 때문에 추상화시킴\(인터페이스화\)
3. UserDao가 new HallaConnectionMaker와

   new JejuConnectionMaker를 결정하는 상황이 나옴

    →  UserDao가 의존성을 가지는 안좋은 상황

    →  의존성을 주입받는 방식으로 변경한 것\(생성자를 통해\)

   나를 생성해주는 놈이 결정해줘\(클라로 의존성 짬때리기\)

이렇게 리팩토링을 하다보니 자연스럽게 Strategy Pattern을 사용한게 됨

### Strategy Pattern

* 개발할 때 가장 많이 사용하는 패턴
* Context\(변하지 않는 것\)와 Strategy\(변하는 것\)을 구분하고

  실제로 변하는 것을 각각에 전략에 맞게 꽂아주는 패턴

* 변하지 않는 것을 그대로 두고

   변하는 것의 구현체를 상황에 따라 바꿔주는 필요에 따라 전략을 바꿔주는 패턴

다시 실습으로 돌아가서

* 클라이언트 입장에서도 dependency를 가지고 싶지 않을 수 있음
* new JejuConnection하는 부분이 너무 많음
* 만약에 변하게 될 경우 다 바꿔줘야되니까
* 클라에서 의존성 짬때리기 

```text
    public void get() throws SQLException, ClassNotFoundException {
        Integer id=1;
//        ConnectionMaker connectionMaker=new Jejuconnectionmaker();
//        UserDao userDao = new UserDao(connectionMaker);
        DaoFactory daoFactory=new DaoFactory();
        UserDao userDao=daoFactory.userDao();
          <- 나는 daoFactory에서 UserDao를 받아서 쓰겠다
        User user = userDao.get(id);

        assertThat(user.getId(), is(id));
        assertThat(user.getName(), is(name));
        assertThat(user.getPassword(), is(password));
    }
public class DaoFactory {

    public UserDao userDao() {
        return new UserDao(connectionMaker());
    }


    public ConnectionMaker connectionMaker() {
        return new Jejuconnectionmaker();
    }
}
```

### DaoFactory ← 오브젝트 생성을 짬때린 것

* 오브젝트를

   생성하는 쪽과

   사용하는 쪽의

   역할과 책임을 분리하는 목적으로 사용됨

* 남들이 갖기싫어 하는 의존성을 전문적으로 관리해주는 녀석
* DaoFactory는 각 오브젝트들에게 **의존성을 주입**해준다. 이것이 DI\(의존성 주입\)
* new 한 것을 받아서 쓴다. \(DI\)
* 클라이언트UserDaoTest\)쪽에서는 이제 UserDao가 어떻게 만들어지는지 어떻게 초기화가 되는지에 대해 신경 쓰지 않고 팩토리로 부터 UserDao 오브젝트를 받아다가, 자신의 관심사인 테스트를 위해 활용만 하면됨
* 의존성을 관리해주는 역할이 필요한데,  이런 DaoFactory역할을 해주는 것이 Spring

Spring의 기본이자 코어

* 의존성을 알아서 관리해주는 것

  ////////////////2020.8.20.오전 12시 45여기까지

기존의 팩토리 코드

```text
public class DaoFactory(){

   public UserDao getUserDao(){
     return UserDao(getConnectionMaker());
   }

   private JejuConnectionMaker getConnectionMaker(){
     return new JejuConnectionMaker();
   }
}
```

Spring방식으로 바꾼 코드

Configuration:설정

```text
@Configuration
public class DaoFactory(){
//빈이 하는 역할 : [UserDao를 new하는 역할]
@Bean
public UserDao userDao(){
return new UserDao(getConnectionMaker());
  }
//private를 public으로 바꿈(다른 곳에서 사용할 수 있으니까)
@Bean
public ConnectionMaker connectionMaker(){
return new JejuConnectionMaker();
  }
 }
}
public class UserDaoTest {
    String name = "hi";
    String password = "jihwan";
    private static UserDao userDao;

    @BeforeAll
    private void setup() {
        ApplicationContext applicationContext = new AnnotationConfigApplicationContext(DaoFactory.class);
        userDao = applicationContext.getBean("userDao", UserDao.class);
    }

    @Test
    public void get() throws SQLException, ClassNotFoundException {
        Integer id = 1;
        User user = userDao.get(id);

        assertThat(user.getId(), is(id));
        assertThat(user.getName(), is(name));
        assertThat(user.getPassword(), is(password));
    }


    @Test
    public void insert() throws SQLException, ClassNotFoundException {
        User user = new User();
        userDao.insert(user);
        assertThat(user.getId(), greaterThan(0));

        User insertUser = userDao.get(user.getId());
        assertThat(insertUser.getName(), is(name));
        assertThat(insertUser.getPassword(), is(password));
    }
}
```

Bean: 스프링이 new해주는 오브젝트 인스턴스

Spring이 new를 해주었고 우리는 그 Bean을 가져다 쓰면됨

@BeforeAll : 아래 코드가 돌아가기전에 수행되어야 한다는 어노테이션

### Spring에서 Bean을 꺼내 쓰는 방법

* ApplicationContext

  :  Bean들을 관리하는 녀석

```text
//여기서도 전략패턴 적용됨
// ApplicationContext는 인터페이스요
// AnnotationConfigApplicationContext는 갈아끼울수 있는 전략이다
ApplicationContext applicationContext = new AnnotationConfigApplicationContext(DaoFactory.class);
```

어노테이션의 정의가 빈으로 되어있다.

```text
//빈의 이름이 메소드명
//파라미터 두개 각각: 가져올 Bean의 이름, Bean의 타입
userDao = applicationContext.getBean("userDao", UserDao.class)
```

* 인스턴스를 new해줘서 Dependency를 관리해주는 녀석이 있고, 그녀석한테 특정 의존성 주입이 완료된 것을 look up해온다. → Dependency Look up

### 환경변수에 의존성 짬때리기

* DB환경이 다른 곳에 납품하기 위해서 우리는 클래스를 고쳐야했었고, 클래스가 서로 다르게 관리되어야 한다는 불편함이 있었다
* 배포하는 환경에 따라 달라지기 때문에 배포하는 환경의 환경변수로 값을입력받을 수 있게 만들면된다. → Spring에서 제공하는 property주입 이용한다.

  ```text
  @Value("${db.classname}")
  private String className;
  @Value("${db.url}")
  private String url;
  @Value("${db.username}")
  private String userName;
  @Value("${db.password}")
  private String password;
  ```

-&gt; 환경변수를 통해서 원하는값을 입력받는 거임 -&gt; 모든 의존성 제거 성공

* **환경변수**에서는 **변수명을 대문자**로 **“.”는 “\_”로 인지**한다.
* db.classname → DB\_CLASSNAME

Edit Configuation 클릭하고 환경변수 입력하는 곳이있음

| NAME | VLUE |
| :--- | :--- |
| DB\_CLASSNAME | com.mysql.cj.jdbc.Driver |
| DB\_URL | jdbc:mysql://localhost/hellooo |
| DB\_USERNAME | root |
| DB\_PASSWORD |  |

-&gt; 이런식으로 하면 매핑이 됨

장애발생

* dao 를 사용하는데, 가끔 서버가 죽어 어떻게 된거야?

→ 뭐가 서버를 죽일까?

1. Connection을 맺은 상태에서 예외가 발생하면 프로그램이 끝날거임
2. Connection을 close하지 않고 끝나버렸기 때문에 Connection이 쌓이게 됨
3. DB에서 설정한 MaxConnection에 도달하여 서버가 죽은 것

```text
→ 예외처리를 해서 예외가 일어나도 close를 하게 만든다.
```

요구사항

* 사용자 삭제하는거 만들어줘
* 사용자 수정하는거 만들어줘

수정 테스트

```text
@Test
public void update() throws SQLException, ClassNotFoundException {
    String updatedName="jiha";
    String updatedPassword="babo";
    User user = new User();
    user.setName(name);
    user.setPassword(password);

    userDao.insert(user);

    user.setName(updatedName);
    user.setPassword(updatedPassword);
    userDao.update(user);

    User updatedUser=userDao.get(user.getId());

    assertThat(updatedUser.getName(),is(updatedName));
    assertThat(updatedUser.getPassword(),is(updatedPassword));
}
```

수정 구현

```text
public void update(User user) throws SQLException, ClassNotFoundException {
    Connection connection = connectionMaker.getConnection();
    PreparedStatement preparedStatement=connection.prepareStatement("update user set name=?, password=? where id=? ");
    preparedStatement.setString(1, user.getName());
    preparedStatement.setString(2,user.getPassword());
    preparedStatement.setInt(3, user.getId());
    preparedStatement.executeUpdate();

    preparedStatement.close();
    connection.close();
}
```

삭제 테스트

```text
@Test
public void delete() throws SQLException, ClassNotFoundException {
    User user = new User();
    user.setName(name);
    user.setPassword(password);
    userDao.insert(user);

    userDao.delete(user.getId());
    User deletedUser=userDao.get(user.getId());
    assertNull(deletedUser);
}
```

삭제 구현

```text
public void delete(Integer id) throws SQLException, ClassNotFoundException {
    Connection connection = connectionMaker.getConnection();
    PreparedStatement preparedStatement=connection.prepareStatement("delete from user where id=?");
    preparedStatement.setInt(1, id);
    preparedStatement.executeUpdate();
    preparedStatement.close();
    connection.close();
}
```

하던 도중 변경사항

```text
public User get(Integer id) throws ClassNotFoundException, SQLException {
    Connection connection = connectionMaker.getConnection();
    PreparedStatement preparedStatement
       =connection.prepareStatement("select id, name, password from user where id=?");
    preparedStatement.setInt(1, id);

    ResultSet resultSet
       = preparedStatement.executeQuery();

    User user = null;
    if (resultSet.next()) {
        user = new User();
        user.setId(resultSet.getInt("id"));
        user.setName(resultSet.getString("name"));
        user.setPassword(resultSet.getString("password"));
    }

    resultSet.close();
    preparedStatement.close();
    connection.close();
    return user;
}
```

요구사항 만족

여기서 부터는 리팩토링

리팩토링은 update와 delete를 중심으로 보면 될 것

insert와 get은 비슷한 방향으로 진행될 예정

### 변하지 않는 부분이 반복이 되는데 여기를 변하는 부분이 방해함\(쿼리 작성하고 실행하는 부분\)

1. 변하는 부분과 변하는 부분 캐치
2. 변하는 부분은 추상화할것

우리가 배운 추상화 방법

1. **메소드 단위**의 추상화\(**템플릿 메소드 패턴,** **팩토리 메소드 패턴** 등\)
2. **클래스 단위**의 추상화\(**전략 패턴**\)

   첫번째 방법부터 적용

→ 메소드로 따로 빼내고 추상화\(abstract 키워드\)

* update와 delete 에서 쿼리를 실행 하는 부분에서 makeStatement의 로직은 각자 별도의 로직이 필요함

  상속기반의 추상화가 안되니 더 큰 추상화 레벨 클래스 단위의 추상화를해야함

2번방법 적용

* Strategy 패턴 사용\(변하는 부분을 전략으로 처리\)
* makeStatement를 인터페이스로 추상화하고 구현체로 연결함
* 파라미터 부분이 각 전략마다 다르기 때문에 Object로 값을 받아서 

  각 전략에 맞게 타입변환해서 사용할 수 있게 함 

변하는 부분은 따로 위로 빼내고

파라미터를 구현체에 넘김 why?

* id와 user는 각각 makeStatement에서만 활용하고 있음, 생성자를 통해 user와 id를 받게하여 코드가 비슷하게 만듬

각 메소드에 중복되는 부분 존재

→ 중복되는 부분 extract method\(메소드로 추출\)

→ 변하는 것\(Strategy\)과 변하지 않는 것\(context\)을 분리

변하지 않는 부분을 따로 모아서 클래스로 분리함 **JdbcConext**클래스에 변하지 않는 것을 분리해냄

Strategy패턴을 사용 했더니

GetStatementStrategy같은 구현 클래스들이 많아지고 클래스가 많아지니 부담스럽고 관리하기 힘듬

인터페이스를 바로 익명객체로 바로 구현해서 사용하자

### 템플릿 콜백 패턴

* **인터페이스를 직접 코드에서 구현하는 패턴**이 템플릿 콜백패턴
* **인터페이스 자체가 템플릿이 되고**

  **그안에서 구현되는 메소드 자체가 콜백메소드**임

* 인터페이스를 직접구현해서

   전략을 직접구현하여

   개발하는 패턴이 템플릿 콜백 패턴

* 전략패턴을 쓰는 많은 곳에서는

  주로 전략 자체가 구현되는 전략이 메소드가 하나인 경우가 많음

  템플릿 콜백패턴을 하고 람다를 사용하면 굉장히 편하게 쓸 수 있음

### 리팩토링 과정 요약

* 코드를 만들어나가는 과정이 추상화부터 시작
* 변하는 것과 변하지 않는 것들을 분리
* 변하지 않는 것을 context로 빼고

   변하는 것을 strategy로 분리

* 여기까지 리팩토링하는 과정에서 많은 패턴들이 적용됨 
* 깔끔한 코드가 완성됨

Dao팩토리는 Spring의 핵심적인 기능

Bean을 꺼내쓰기 위한 ApplicationContext. Spring이 잘 new연산을 해준 DI까지 해준 Bean 반환해줌

ApplicationContext에 대해서 좀더 깊게 다룰 예정

ApplicationContext

* extends BeanFactory\(빈을 관리해주는 팩토리 빈팩토리 상속받음\)
* StaticApplicationContext

```text
StaticApplicationContext applicationContext = new StaticApplicationContext();
BeanDefiniton jdbcContextBeanDefiniton = new RootBeanDefiniton(JdbcTemplate.class);
jdbcContextBeanDefiniton.getConstructorArgumentValues().addGenericArgumentValue(new RuntimeBeanReference("dataSource"));
applicationContext.registerBeanDefinition("jdbcContext", jdbcContextBeanDefiniton);BeanDefiniton beanDefiniton = new RootBeanDefiniton(UserDao.class)
beanDefiniton.getConstructorArgumentValues().addGenericArgumentValue(new RuntimeBeanReference("jdbcContext"));
applicationContext.registerBeanDefinition("userDao", beanDefinition);
```

이렇게 코드로 빈을 정의하고 등록하는 것이 StaticApplicationContext\(거의 사용 안함/이리 등록되는 거만 알고 있어라\)

* GenericXmlApplicationContext\(Xml 파일을 설정 정보로 사용하는 컨테이너 구현클래스\)
* ClassPathXmlApplicationContext\(ClassPath기준으로 활용가능\)
* GenericGroovyApplicationContext
* AnnotationConfigApplicationContext
* 각각의 WebApplicationContext
  * StaticWebApplicationContext
  * XmlWebApplicationContext
  * AnnotationConfigWebApplicationContext

### ApplicationContext 계층구조

/

```text
                       root
  ___________  ApplicationContext_______                    
 |                                                  |
```

### A1                                          A2 ApplicationContext                   ApplicationContext \| B1

### ApplicationContext

* 주로 웹어플리케이션에서 사용
* 하나의 wars에 여러개의 웹어플리케이션이 등록이 가능함
* ApplicationContext은 계층구조가 가능하다
* 부모는 자식의 Bean을 참조할 수 없고 자식만 부모의 Bean을 참조할 수 있는 구조로 설계되어있음

### Bean을 등록하는 방법

* .....\(xml사용\)
* @Configuration....@Bean...@Bean
* @Component /Component를 제외 한 나머지 어노테이션은 Component를 상속받은 자식 클래스/@Controller @ Service @Repsitory

### DI 설정하는 법

* ...&lt;/constructor-arg&gt;

  ex\)

```text
<bean name="jdbcTemplate" class"org.springframework.jdbc.core.JdbcTemplate">
<constructor-arg ref="dataSource"/>
</bean>
```

* ...

```text
<bean name="jdbcTemplate" class"org.springframework.jdbc.core.JdbcTemplate">
<property name="dataSource" ref="dataSource"/>
</bean>
```

* @Resource\(name="jdbcTemplate"\)
  * 해당되는 이름으로 DI를 수행함
* @AutoWired
  * @Component된 곳은 생성자가 있으면 DI가 자동적으로됨
  * property쪽에서는 @AutoWired를 통해서 DI를 설정할 수 있음
  * 타입을 보고 DI를 수행함

### Value 설정

* * @Value
  * @Value\("value"\) String str;
  * @Value\("2.3"\) double rate;
  * @Value\("1,2,3,4"\) int\[\] intarr;

### Bean Scope

* singleton\(Dafault\)-&gt; 주로 사용하는 스코프,정석
  * 스프링이 관리하는 빈은 인스턴스를 하나만 생성한다.
  * 공유하는 property 가 없는, 메소드 기반으로 된 클래스만 bean으로 관리
* prototype
* request
* session
* applicaion
* websocket

나머지는 제대로 이해안하고 쓰면 독이 됨 가능하면 사용하는 것을 지양하자

빈의 이름 :**@Bean 메소드 이름이 빈의 이름**이다. getBean\(\)에서 사용

* &gt;자바에서는 @Bean methodName\(\)

빈의 클래스:빈 오브젝트를 어떤 클래스를 이용해서 만들지 정의

* class="a.b.c...BeanClass"&gt;  -&gt;&gt;return new BeanClass\(\); 

빈의 의존 오브젝트 : 빈의 생성자나 수정 메소드를 통해 의존 오브젝트 주입,

의존 오브젝트로 하나의 빈이므로 이름 존재, 그 이름에 해당하는 메소드 호출해서 의존오브젝트 가져옴

스프링 개발자가 수정자 메소드를 선호하는 이유 중에서는 XML로 의존관계 정보를 만들 때 편리하다는 점도 있음 자바빈의 관례를 따라서 수정자 메소드는 프로퍼티가 된다. 프로퍼티 이름은 메소드 이름에서 set을 제외한 나머지 부분을 사용함

XML 에서는  태그를 사용해 의존 오브젝트와의 관계를 정의한다.

 태그는 name과 ref라는 두 개의 애트리뷰트를 갖는다.

* name은 property의 이름
* ref는 수정자 메소드를 통해 주입해줄 오브젝트의 빈이름이다

userDao.setConnectionMaker\(connectionMaker\(\)\); =&gt;

