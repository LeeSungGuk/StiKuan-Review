# Generics

`Generics` 는 다양한 타입의 객체들을 다루는 메서드나 `Collection` Class에 컴파일 시에 타입을 체크해 주는 기능이다. C++에는 `template`이 비슷하게 작동해 주고 있다.



## Generics의 장점

* 타입의 안정성이 제공된다. ( 어떤 타입인지 쉽게 파악 가능하다. )
* 타입체크와 형변환을 생략할 수 있다. 

```java
import java.util.*;

public class Main {

    public static void main(String[] args) {
        // Generic 설정시 변수<타입>을 지정하여 생성할 수 있다.
        Generic<String,Integer> generic = new Generic<String, Integer>();
        generic.setValue1("Test Set");
        generic.setValue2(200);
        System.out.println(generic.getValue1());
        System.out.println(generic.getValue2());
        // 이처럼 type을 지정하여 실제로 사용할 수 있다.

        Generic generic1 = new Generic();
        generic1.setValue1("test");
        generic1.setValue2("29");
        generic1.setValue1(45);
        // Type을 지정하지 않고 넣을시 자동으로 Object Type 처리가 된다.
    }
}

// Generic 타입인 T를 선언한 것이다.
// C++에서는 템플릿이라고 생각하면 비슷합니다.
class Generic<T1,T2>{
    T1 value1;
    T2 value2;
    void setValue1(T1 item){this.value1 = item;}
    void setValue2(T2 item){this.value2 = item;}
    T1 getValue1(){ return this.value1;}
    T2 getValue2(){ return this.value2;}
}
```



이처럼 `Generics`은 원시 타입<매개변수 타입> 을 통해 객체별로 다른 타입의 활용을 할 수 있도록 도와준다.

단 `static`은 모든 객체에 동일해야 하기 때문에 `static` 변수에 `Generic`은 사용할 수 없다.

```java
class item{
  static T test1; // 이런 것이 안된다는 것이다.
}
```



`Generics` 내부 요소를 배열로 만들어 사용하고 싶다면 , new로 객체 생성시 Type을 지정해 주어야 한다는 점을 기억해야 한다.

```java
import java.lang.reflect.Array;
import java.util.*;

public class Main {

    public static void main(String[] args) {
        // Generic 설정시 변수<타입>을 지정하여 생성할 수 있다.
        // Generic 내부에서 배열을 사용하기 위해서는 type 지정이 필요하다.
        Generic<String,Integer> generic  = new Generic<String,Integer>(String.class,Integer.class,20);
        
        // Generic 자체의 배열은 이렇게 똑같이 선언해주면 된다.
        Generic<String,Integer>[] generics = new Generic[10];
    }
}

// Generic 타입인 T를 선언한 것이다.
// C++에서는 템플릿이라고 생각하면 비슷합니다.
class Generic<T1,T2>{
    T1[] value1;
    T2[] value2;

    // Generic 내부 요소의 배열을 사용하기 위해서 Type 지정이 필요하기 때문에 이렇게 해주어야 한다.
    public Generic ( Class<T1>item,Class<T2>item2,int size )
    {
        value1 = (T1[]) Array.newInstance ( item , size );
        value2 = (T2[]) Array.newInstance ( item2 ,size );
    }


```



`Generic`은 `ArrayList` 또한 자유롭게 사용가능하고,  타입을 선언하게 되면 new 생성자 부분에서는 type 생략이 가능하다. ( 주의할 점은 int 같은 자료형은 `Integer` 같은 class로 선언해 주어야 한다. )

```java
import java.lang.reflect.Array;
import java.util.*;

public class Main {

    public static void main(String[] args) {
        // 이처럼 new 부분은 type 생략이 가능하다.
        Generic<Integer> integerGeneric = new Generic<>();
        for(int i=0;i<10;i++)
        {
            integerGeneric.add(i);
        }
        System.out.println("List: "+ integerGeneric.getList());
        // List: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
        // 이처럼 ArrayList 또한 Generics 에서 사용이 가능하다.
    }
}

// Generic 타입인 T1을 선언한 것이다.
// 여기서는 ArrayList를 사용한 예제이다.
class Generic<T1>{
   ArrayList<T1>  arrayList = new ArrayList<T1>();
   void add(T1 item){arrayList.add(item);}
   T1 get(int index){return arrayList.get(index); }
   ArrayList<T1> getList(){ return arrayList;}

}
```



함수 선언부에 `Generics` 타입이 선언된 함수가 있다면, 이를 `Generics Method` 라고 한다.

```java
// Generic 타입인 T1을 선언한 것이다.
// 여기서는 ArrayList를 사용한 예제이다.
class Generic<T1>{

    // T, T1은 각자 다르다.
    // Method는 Generic class 선언 변수와 다르게 제네릭 함수로 반환할 수 있다.
   <T> void test(){

    }
}
```

