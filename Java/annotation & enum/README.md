# Enum

C언어의 `Enum` 과 비슷한 Java의 `Enum`은 JDK 1.5 Version 부터 추가되었으며, C는 단순한 값이었지만, Java는 Type까지 관리합니다.

```java
enum Direct { North, South, East , West}
// 열거형은 enum 을 통해 선언할 수 있습니다.

public class Main {

    public static void main(String[] args) {
        Direct direct;
        Direct direct1;
        // 열거형을 만든 후 , 열거형 내의 값을 자유롭게 넣을 수 있습니다.
        direct = Direct.East;
        direct1 = Direct.East;
        System.out.println("Enum value : " + direct); // ex) Enum value : East
        if(direct == direct1) // Enum 끼리는 == 로 비교가 가능하다
        {
            System.out.println("두 열거형 변수는 같습니다 . ");
        }else{
            System.out.println("두 열거형 변수는 다릅니다 . ");
        }
    }
}

```



`Enum`에 있는 값 하나하나가 그 `Enum` Name의 객체라고 볼 수 있다.



# Annotation

`Annotation`은 소스 코드에 메타데이터를 표현하는 것입니다.   

프로그래밍 언어 자체에는 영향을 주지는 않지만, `@Override` 와 같이 이러한 `Annotation`을 Method나 다른 

Annotation을 너어주면, 컴파일러가 Annotation을 확인하고 옳지 않으면 결과를 출력시켜 주기 때문에,

상당히 유용하게 소스코드의 구조나 타겟의 연결을 편하게 관리해 줄 수 있는 도구입니다.

`Metadata` : Data를 설명해 주는 Data라고 간단히 생각하시면 됩니다.