
# **Spring Framework** 

`Spring Framework`는 Java PlatForm 을 위한 `OpenSource Application Framework` 로서 간단하게 `Spring` 이라고 합니다. 

Spring의 용도는 동적인 웹 사이트 개발을 위한 것입니다.

* [Maven](#Maven)

* [DI](#didependency-injection)

* [Autowired](#autowired-annotation)

* AOP

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

[위로](#spring-framework)

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

[위로](#spring-framework)

</br>

## Autowired Annotation

`@Autowired` 는 get,set을 입력하지 않아도 자동으로 의존 객체가 주입되게 해주는 Annotation입니다.  즉 , 자동으로 Property를 찾아서 주입해 줍니다.

`@Override` 는 추상클래스에서 구현하지 않은 메소드를 구현할 때 쓰는 Annotation으로서, Service -> ServiceImpl 인 구현체쪽에서 많이 씁니다.

`@Resource` 는 필드나 메서드에 적용시켜 빈의 이름을 사용하여 주입하는 빈 객체를 찾아 넣습니다.

`@Autowired`는 type을 이용하며, `@Resourece`는 (name="이름")으로 주입할 객체를 넣는다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
// xmlns:context를 설정함으로서 @AutoWired 사용이 가능합니다.
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context.xsd">
            
    // Context를 통해 @Autowired가 사용가능합니다.        
    <context:annotation-config/>       

    <bean id="Test" class="com.java.ex.Test">
   		
    </bean>
  <bean id="myTest" class="com.java.ex.MyTest">
  	<property name="first" value="10"></property>
  	<property name="second" value="2"></property>
  </bean> 
  
            
</beans>
```

```java
public class MyTest {
	Test test;
	private int first;
	private int second;
	
  // @Autowired를 통해 test에 있는 property를 자동 주입해 줍니다.
	@Autowired 
	public MyTest(Test test){
		this.test = test;
	}
	public void add(){
		test.add(first, second);
	}
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

[위로](#spring-framework)

</br>



## AOP (Aspect Oriented Programming)

`AOP`란, 여러 객체에 공통으로 적용할 수 있는 기능을 구분해주고, 
객체지향적인 프로그래밍을 지향하면서 유지보수를 좀 더 편리하게 하기 위한 방법
프로그래밍을 할때 공통적인 기능이 많이 발생하여, 상속을 통해 관리하였으나 Java는 다중 상속이 불가하므로,
다양한 Module에 상속 기법을 통한 공통 기능 부여에 한계가 있어, `AOP`가 등장하였습니다.

`Spring` 에서는 주로 `Proxy` 객체를 만들어 공통 기능을 추가합니다. (`xml or @Aspect Annotation`)

`AOP`에서의 `Proxy` 객체는 말그대로 대리하여 업무를 처리. 

함수 호출자는 공통기능을  `Proxy` 에게 맡기고, `Proxy` 는 내부적으로 이러한 공통 기능을 처리합니다.

```xml
<!-- AspectJ -->
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjrt</artifactId>
    <version>${org.aspectj-version}</version>
</dependency>
 
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>${org.aspectj-version}</version>
</dependency>
 
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjtools</artifactId>
    <version>${org.aspectj-version}</version>
</dependency>

// aspect 의존성 ( pom.xml )
```
`Aspect` : 공통 기능 ( 여러객체에 공통으로 적용되는 기능 ex) 트랜잭션, 보안 , 로그 출력 , 예외처리 )
`Advice` : Aspect의 기능 자체
`JoinPoint` : Advice를 적용해야 하는 Method
`PointCut`: JoinPoint의 부분으로 Advice가 적용된 부분
`Weaving` : Advice를 핵심 기능에 적용 하는 것

### Spring AOP 구현

`Spring AOP`를 이용해서 공통 기능을 구현하고 적용하는 방법은
1. 공통 기능을 제공하는 `Aspect`를 구현한다.
2. `Aspect`를 어디(`PointCut`)에 적용할지 (`Advice`)를 설정합니다. 

### Spring AOP 구현 방법

​    1.`Aspect` 구현 클래스를 만든다.
​    2.`XML` 스키마 기반의 `POJO`를 만들거나, `@Aspect` 애노테이션을 통해 공통 기능을 사용한다.

[위로](#spring-framework)

### XML 기반의 POJO (Plain Old Java Object) 클래스로 AOP 구현방법

먼저 Aspect로 사용할 클래스를 만듭니다.

```java
import java.util.Arrays;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.Signature;

// aspect 를 import 하여야 ProceedingJoinPoint를 사용가능합니다. (JoinPoint 하위타입)
public class TimeAspect { // aspect 의존성이 있어야 합니다.
	public Object Time(ProceedingJoinPoint joinPoint) throws Throwable{
		long start = System.nanoTime();
		try{ // Object는 객체를 받기 위해서 ...
			Object result = joinPoint.proceed(); // proceed를 호출하면 대상 객체 메서드가 실행
			return joinPoint;
		}finally{
			long finish = System.nanoTime();
			Signature sig = joinPoint.getSignature();
			//메서드의 시그니처, 객체 , 대상과 함꼐 소요시간을 나타냄
			System.out.printf("%s.%s(%s) 실행시간  %d ns\n", 
					joinPoint.getTarget().getClass().getSimpleName(),sig.getName(),
					Arrays.toString(joinPoint.getArgs()),(finish-start));
		}
	}

}

```

해당 클래스를 정했다면 사용할 `AOP` 클래스를 `bean`으로 등록하여 넣어줍니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
// xmlns:aop를 추가하고, 그 이후 사용할 AOP 객체를 bean으로 등록한다.
// xmlns = xml namespace
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:aop = "http://www.springframework.org/schema/aop"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context.xsd
            http://www.springframework.org/schema/aop 
            http://www.springframework.org/schema/aop/spring-aop-3.0.xsd"
       >
            
    <context:annotation-config/>       

	<bean id="TimeAspect" class="com.java.ex.TimeAspect"></bean>
        <aop:config>
    	<aop:aspect id="meanAspect" ref="TimeAspect">
 			  <aop:pointcut id="Method" expression="execution(public * com.java.ex..*(..))">			</aop:pointcut>
    		<aop:around pointcut-ref="Method" method="Time"/>
    	</aop:aspect>
   	 </aop:config>
  
  <bean></bean>
```

이러한 작업을 하게 되면 그 이후 `bean`등록시 `AOP`가 구현되어 공통 기능을 사용할 수 있습니다.



[위로](#spring-framework)