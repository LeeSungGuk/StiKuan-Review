# Collection Framework


다수의 데이터들을 관리하는 방법이 없으면 자료들은 단지 Data 모음일 뿐이다.  

`Collection Framework`는 JDK 1.2부터 사용할 수 있게 해주며, 사용 용도에 따라 `List`, `Set`, `Map` 인터페이스를 

상속한 구현 클래스를 통하여 다수의 데이터를 목적에 따라 사용할 수 있게 해줍니다.

- [List](#List)
- [Stack & Queue](#Stack)




## List

`List` 는 순서가 있는 데이터의 집합이며, 데이터의 중복을 허용합니다. 

### ArrayList

`ArrayList`는 편하게 배열로 이루어진 리스트라고 이해하면 쉽고, 기존의 `Vector` Class를 개선한것이다.



```java
import java.util.ArrayList;
import java.util.Collections;

public class Main {

    public static void main(String[] args) {
        ArrayList list = new ArrayList();
        // 크기가 0인 ArrayList를 생성

        list.ensureCapacity(10);
        // ensureCapacity를 통해 Size를 늘릴 수 있습니다.

        for(int i=0;i<10;i++){
            list.add(i);
            // .add를 통하여 원소에 값을 집어 넣을 수 있습니다.
        }

       System.out.println("List :" + list);
       // list는 한번에 출력 시킬 수 있습니다.
       // ex) List :[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

       System.out.println("List :" + list.subList(1,4));
       // list는 부분으로도 출력할 수 있습니다. ex) List :[1, 2, 3] (시작원소, 마지막원소 + 1);

       ArrayList list2 = new ArrayList(list.subList(1,4));
       // 기존의 ArrayList의 일부를 통해 새로운 list도 생성 가능합니다.

        Collections.sort(list2); // Collection.sort()를 이용해 정렬도 가능합니다.
        int arrayValue = (int) list2.get(2); // get을 통해 특정 index의 원소를 꺼낼 수 있습니다.
    }
}
```



### LinkedList

`LinkedList`는 배열은 크기를 변경할 수 없고 변경하기 위해서는 데이터 복사 작업이 필요하고, 비순차적인 데이터의 추가 , 삭제에 시간이 걸리기 때문에 삭제, 삽입 및 크기 변경이 편하도록 만든 Class입니다.

```java
    public static void main(String[] args) {
          LinkedList linkedlist = new LinkedList();
          // 새로운 linkedList를 생성합니다.
          for(int i=0;i<10;i++){
              linkedlist.add(i,i+40);
          } // linkedlist는 add(index번호, 내용)을 통해 값을 넣습니다.
          System.out.println("Linkedlist :" + linkedlist);
            // Linkedlist 또한 list 전체를 출력할 수 있습니다.
            // Linkedlist :[40, 41, 42, 43, 44, 45, 46, 47, 48, 49]
    
          int index =  linkedlist.lastIndexOf(linkedlist.getLast());
          System.out.println(index);
            // lastindexOf라는 Method를 통해 객체의 위치 또한 찾을 수 있다.
    
            // JDK 1.5부터는 Queue, JDK 1.6부터는 Deque를
            // Linkedlist에서 사용할 수 있게 하고 있다.
    
            // peek, pop등을 사용할 수 있게 한다.
          int object1 = (int)linkedlist.peekFirst(); // 첫 요소 반환
          System.out.println(object1); // Example : 40
    }
```



### ArrayList vs LinkedList

그러면 결국 둘은 어느 때 쓰는 것이 좋을까? 답은 순차적인 삭제, 삽입을 하거나 검색시에는 `ArrayList` 가 

시간상 효율이 더 좋으며, `LinkedList`는 비 순차적인 Data들을 삭제, 삽입할 시 유용하다. 또한 `LinkedList`는

Data가 많을수록 접근시간이 길어지기 때문에, 공간적 효율성과 시간적 효율성등을 자세히 파악하여 둘 중 유용한 

것을 쓰는 것이 좋다. 



### Stack

 Java에서 제공하는 `Stack` Class 또한, 자료구조의 `Stack`과 유사한 LIFO 

(Last - In - First - Out)으로 되어있는 클래스이며, 사용방법도 자료구조의 `Stack`과 유사하다고 생각하면 된다.

```java
  public static void main(String[] args) {
        Stack stack = new Stack();
        // 새로운 Stack 구현체를 생성합니다.
        for(int i=0;i<10;i++)
            stack.push(i);
        // push를 통해 값을 넣을 수 있습니다.
        while(!stack.empty()){
                System.out.println(stack.pop());
        } // pop을 통해 값을 꺼낼수 있으며, LIFO방식으로 마지막 입력값이 먼저 출력된다.
        // ex) 9,8,7,6,5,4,3,2,1,0
    }
```



### Queue

Java에서 제공하는 `Queue` Class 또한, 자료구조의 `Queue`과 유사한 

FIFO (First - In - First - Out)으로 되어있는 클래스이며, 사용방법도 자료구조의 `Stack`과 유사하다고 생각하면 된다.

JDK 1.5 버전 이후로는 `LinkedList`를 통해 `Queue` 함수의 구현체로 사용합니다.

```java
  public static void main(String[] args) {
        Queue queue = new LinkedList();
        // 새로운 Queue 구현체를 생성합니다.
        // Q : Queue는 LinkedList로 구현을 하느냐
        // A : Queue는 Java에서 Interface만 정의되어 있음
        // A : 구현체는 LinkedList로 하고 있다.
        for(int i=0;i<10;i++)
            queue.offer(i);
        // offer를 통해 값을 넣을 수 있습니다.
        while(!queue.isEmpty()){
            System.out.println(queue.poll());
        } // poll을 통해 값을 꺼낼수 있으며, FIFO방식으로 처음 입력값이 먼저 출력된다.
        // ex) 0,1,2,3,4,5,6,7,8,9
    }
```



