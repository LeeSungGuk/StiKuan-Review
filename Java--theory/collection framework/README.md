# Collection Framework


다수의 데이터들을 관리하는 방법이 없으면 자료들은 단지 Data 모음일 뿐이다.  

`Collection Framework`는 JDK 1.2부터 사용할 수 있게 해주며, 사용 용도에 따라 `List`, `Set`, `Map` 인터페이스를 

상속한 구현 클래스를 통하여 다수의 데이터를 목적에 따라 사용할 수 있게 해줍니다.



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



### Iterator

컬렉션에 저장된 요소를 편하게 접근하고 보는데 사용되는 인터페이스이다. 

`Iterator`는 `List` , `Set`에 정의되어 있으므로 `Map`을 제외하고서는 바로 사용 가능하다.

```java
    public static void main(String[] args) {
        List list = new ArrayList();
        // 크기가 0인 List를 생성
        // List 생성한 이유는 LinkedList 코드로도 편하게 바꾸기 위함

        for(int i=0;i<10;i++){
            list.add(i);
        }
       
        Iterator iterator = list.iterator();
        // Iterator를 통해 Collection 요소 접근
        while(iterator.hasNext()) // iterator 접근 요소가 남았는지 확인
        {
            System.out.println(iterator.next());
            // 해당되는 다음 요소를 읽어옵니다. ( .next()를 통해 )
            iterator.remove(); // remove를 통해 next를 읽어온 요소를 삭제 가능하다.
        }
        System.out.println("List : " + list);
        // iterator를 통해 remove를 하면 원본 리스트 속의 값이 삭제됨을 알 수 있다.
        // ex) List : []
    }
```



### Arrays

`Arrays` 클래스는 배열을 다르게 유용한 함수들이 정의되어있고, 

배열의 복사(`copyOf()`, `copyOfRange()`) , 정렬 (`sort()`) , 검색 (`binarysearch()`)등의 함수가 정의되어 있다.

또한, `List` 의 값을 `Arrays`를 이용하여  생성할 수 있다.



```java
 public static void main(String[] args) {

        int[] arr = {13,21,45,23,48,67,44,89,9,100};
        // 크기가 10인 임의의 배열 생성
        int[] arr2 = Arrays.copyOf(arr,3) ;
        // Arrays.CopyOf를 통해 일부 요소를 복사하여 생성 할 수 있습니다.
        Arrays.sort(arr); // sort()를 통해 배열의 요소를 정렬할 수 있습니다.
        System.out.println(Arrays.toString(arr));
        // sort 함수 이후 정렬된 값을 볼 수 있다.
        // ex) [9, 13, 21, 23, 44, 45, 48, 67, 89, 100]
        // toString을 하지 않으면 이상한 문자와 숫자의 조합을 볼 수 있다.
        int[] arr3 = new int[4];
        Arrays.fill(arr3,4); // fill을 통해 전체 요소를 채울 수 있다.
        List list = Arrays.asList(new int[]{1,2,3,4});
        // 배열을 통해 List의 값을 받을 수 있다. 단 크기가 변경이 불가능하므로 바꾸기 위해서는
        List<Integer> list5 = new ArrayList<>(Arrays.asList(1,2,3,4));
        // 새로운 ArrayList 등을 생성하여 값을 넣어줄 수 있도록 한다.

    }
```



### List에 있는 문자열을 쉽게 정렬하는 법

`Collections`를 이용하면 쉽게 Sort 할수 있으며, 다른 기준에 따라 정렬하고자 하는 경우는 `Comparator`를 

상속받아 직접 구현해야 한다.

```java
 public static void main(String[] args) {
        ArrayList arrayList = new ArrayList(5);
        String[] Test = new String[]{"zoo", "yahoo", "xyz", "abcd", "bear"};
        for(int i=0;i<5;i++){
            arrayList.add(i,Test[i]);
        }
        Collections.sort(arrayList); 
        // ArrayList 등의 List 형태의 문자는 Collection.sort()를 사용한다.
        // 알파벳 순으로 정렬이 가능하다.
        System.out.println("List : " + arrayList);
        // List : [abcd, bear, xyz, yahoo, zoo] 
    }
```

## Set

`Set` 은 순서를 유지하지 않은 데이터의 집합이며, 데이터의 중복을 허용하지 않습니다.

### HashSet 

`HashSet`은 새로운 요소를 추가하며, 중복된 요소를 추가했을 시에는 false 를 반환하고, 저장되는 순서는 정렬 되어 있지 않습니다.

```java
    public static void main(String[] args) {
        String[] strings = new String[]{"1","2","6","2","3","4","5","4"};
        HashSet set = new HashSet();
        // 새로운 Hashset 객체를 생성한다.
        for(int i=0;i<strings.length;i++){
            set.add(strings[i]);
        } // HashSet 객체에 값을 add 한다.
        System.out.println("HashSet : " + set);
        // 중복된 값을 배제한 나머지 값이 들어가 있음을 알 수 있다.
        // ex) HashSet : [1, 2, 3, 4, 5, 6] ( 순서는 Random)
    }
```

### LinkedHashSet

`HashSet` 과의 차이는 중복을 제거하지만, 저장한 순서를 유지한 채로 값을 입력하는 것이 차이점이 있습니다.

```java
    public static void main(String[] args) {
        String[] strings = new String[]{"1","2","6","2","3","4","5","4"};
        LinkedHashSet set = new LinkedHashSet();
        // 새로운 LinkedHashset 객체를 생성한다.
        for(int i=0;i<strings.length;i++){
            set.add(strings[i]);
        } // LinkedHashSet 객체에 값을 add 한다.
        System.out.println("HashSet : " + set);
        // 중복된 값을 배제한 나머지 값이 들어가 있음을 알 수 있다.
        // ex) HashSet : [1, 2, 6, 3, 4, 5] ( LinkedHashSet은 입력 순서대로 저장한다. )
    }
```

### TreeSet

`TreeSet`은 이진 검색 트리 (binary search tree) 의 자료구조로 데이터를 저장하는 클래스입니다. 

`TreeSet`은 Red-Black Tree로 구현이 되어있다. 

```java
   public static void main(String[] args) {
       TreeSet treeset = new TreeSet();
       // 새로운 Treeset 객체를 만들고 값을 add()를 통해 삽입한다.
       for(int i=0;treeset.size()<6;i++){
           treeset.add(i);
       }
       // treeset은 값이 입력될때 자동으로 정렬되서 저장된다.
       System.out.println(treeset);
       System.out.println(treeset.headSet(3));
       System.out.println(treeset.tailSet(3));
       // headset과 tailset을 이용하여 기준 값보다 크거나, 작은 객체를 반환할 수 있습니다.
    }
```



## Map

`Map`은 키(key)와 값(value) 으로 이루어진 데이터의 집합이며, key를 입력하여 value를 찾습니다.



### HashMap

`HashMap`은 key와 value를 입력하고, key 입력시 value를 찾아내는 것이다. 

`HashMap`에서 key는 중복이 허용되지 않는다.

```java
     public static void main(String[] args) {
       HashMap map = new HashMap();
       // HashMap 객체를 생성한다.
        map.put("Test1", 123);
        map.put("Test2", 234);
        map.put("Test3", "Hi");
       //put을 통해 key와 value를 입력한다.

        System.out.println(map.get("Test3"));
        // key를 입력하여 get함수의 결과로 value가 나온다.
        // ex) "Hi"
        System.out.println(map.keySet());
        System.out.println(map.entrySet());
        System.out.println(map.values());
        // keySet ex) [Test1, Test3, Test2] - key만 반환
        // entrySet ex) [Test1=123, Test3=Hi, Test2=234] - key + value 반환
        // values ex) [123, Hi, 234] - value 반환 
        // 이렇게 분리시 Iterator 사용 가능
    }
```

### TreeMap

`TreeMap`은 이진 탐색 트리의 형태로 키와 값으로 이루어진 데이터를 저장한다.

`HashMap`보다 범위검색, 정렬에 유용하지만 대부분은 `HashMap`이 유용하다.



### Collections

`Collections`는 컬렉션 ( `List, Set` ) 과 관련된 메소드를 제공하며, `fill() , copy() , sort()` 등의 함수도 Arrays 처럼 제공이 됩니다.

