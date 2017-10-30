
# **Spring Framework** 

`Spring Framework`는 Java PlatForm 을 위한 `OpenSource Application Framework` 로서 간단하게 `Spring` 이라고 합니다. 

Spring의 용도는 동적인 웹 사이트 개발을 위한 것입니다.

* [Maven](#Maven)
* [DI](#DI(Dependency Injection))
* [Autowired Annotation](#Autowired Annotation)
  </br>  


## Maven

`Maven`은 Java 라이브러리 관리 및 빌드 기능 역할을 하는 관리 도구이다. Java로 개발을 하다보면 필요한 Mysql, JDBC 등의 라이브러리들이 필요한데 `pom.xml`을 통해 편하게 이러한 라이브러리를 쓸 수 있습니다.

또한 Build 또한 가능하여, 소스 들을 Build 하여 실행또한 가능하다.

```java
// pom.xml 에서 이러한 의존성을 작성하는 것만으로도 라이브러리 사용이 가능하다.	
<!-- AspectJ -->
	<dependency>
		<groupId>org.aspectj</groupId>
		<artifactId>aspectjrt</artifactId>
		<version>${org.aspectj-version}</version>
	</dependency>
```

</br>

## DI(Dependency Injection) 

`DI`란 의존 주입이라는 뜻으로, 직접 의존하는 객체를 생성하지 않고 다른 객체를 `setter` 또는 `constructor` 를 통해 받는 것입니다.  Spring 은 편하게 객체를 생성하고 객체에 의존을 주입해 주는 조립기라고 생각하면 편합니다. 

```java
public class Member{
  private MemberDao memberDao;
  
  // 의존 객체를 생성자를 통해 주입하기 때문에, 이는 DI입니다.
  public Member(MemberDao memberDao){
    this.memberDao = memberDao;
  }
}
```

XML 기본 설정

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd">
            
  // 스프링이 생성하는 객체 : bean 
  // id : bean 객체 구분하는 이름 // class: bean 객체 생성시 사용하는 클래스
  <bean id="Test" class="com.java.ex.Test"/>
   
</beans>
```



`Spring`에서 주입을 해줄 때에는 bean을 설정해 놓으며, `configLocation`에서 XML 경로 지정후 `GenericXmlApplicationContext`에서 XML 파일에서 빈 객체를 읽어오고, 그 이후 XML 파일은 `.getBean()` 을 통해 object 를 검색하여 사용합니다.

실제 가지고 있는 `Bean`을 사용하기 위해서는 `set(property name)`을 해주어야 불러서 사용할 수 있다.

```xml
    <bean id="Test" class="com.java.ex.Test">
    </bean>
    <bean id="myTest" class="com.java.ex.MyTest">
      <property name="Test">
          <ref bean="Test"></ref> 
          // Class Object 사용시 위의 bean을 참조하시 ref를 사용 합니다.
      </property>
      // 일반 수일때는 value를 씁니다.
      <property name="first" value="10"></property>
      <property name="second" value="2"></property>
    </bean> 
```

```java
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		String configLocation = "classpath:applicationCTX.xml";
		// XML 경로를 저장한 것
		// 객체를 생성화하고 초기화를 수행하는 클래스 ( XML 파일로 부터 읽어와 수행 ) = > 빈 객체 생성
		AbstractApplicationContext ctx = new GenericXmlApplicationContext(configLocation);
		// XML 파일을 검색해서 나온 bean object 검색 시 사용 ( getBean )
		MyTest myTest = ctx.getBean("myTest",MyTest.class);
		myTest.add();
	}
```

```java
public class MyTest { // class를 Bean으로 설정

  // field는 propery로 사용
    Test test; 
	private int first;
	private int second;
	
	public MyTest(){
		
	}
	public void add(){
		test.add(first, second);
	}
  
 	// property 사용시 setter setting을 위해 set(field Name)이 있어야 한다.
	public void setTest(Test test){
		this.test = test;
	}
	public void setFirst(int first){
		this.first = first;
	}
	public void setSecond(int second){
		this.second = second;
	}

}
```

이러한 과정을 통해 직접 객체를 불러와서 주입하는 것이 아니라, Bean을 통해 내가 쓰고자 하는 객체를 의존 객체로 하여서 불러와서 사용할 수 있다.   즉, DI를 통해 의존객체를 주입하는 것이다.

```java
<bean id="Test" class="com.java.ex.Test">
   <constructor-arg ref="memberDao"
</bean>
// 생성자를 통해 주입하기 위해서는 constructor-arg를 사용하면 된다.    
public class Test{
  private MemberDao memberDao; 
  public Test(MemberDao memberDao){
    this.memberDao = memberDao
  }
}    
```

</br>

### DI를 하는 이유

DI를 사용하는 이유는 코드의 재사용성이 높고, 유지보수를 할 시 간편하게 사용할 수 있습니다.

(xml에서의 `bean`만을 수정하느냐, 전체 코드를 수정하느냐를 생각해보자...)

</br>

## Autowired Annotation

## 

[위로](#Spring Framework)