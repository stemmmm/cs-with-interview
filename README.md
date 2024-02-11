# interview-questions
기술 면접을 대비하기 위한 질문들을 모아놓은 리포지토리입니다. 순서대로 공부하는 것을 권장드립니다.

<br>

# Java
- 자바의 컴파일 과정에 대해 설명하세요.
- 자바 가상 머신 (Java Virtual Machine, JVM)
  - 자바 가상 머신(JVM)의 역할과 기능에 대해 설명하세요.  
  - 자바 말고 다른 언어는 JVM 위에 올릴 수 없나요?
  - 반대로 JVM 계열 언어를 일반적으로 컴파일해서 사용할 순 없나요?
  - VM을 사용함으로써 얻을 수 있는 장점과 단점
  - JVM과 내부에서 실행되고 있는 프로세스는 부모 - 자식 관계를 갖고 있다고 봐도 무방한가요?
- 가비지 콜렉션 (Garbage Collection, GC)
  - GC의 원리와 장단점에 대해 설명하세요.  
  - 자바에서는 GC를 어떤 방식으로 구현했나요?
  - GC는 어떤 데이터 영역을 관리하나요?
  - `finalize()`를 수동으로 호출하는 것은 왜 문제가 될 수 있을까요?
  - 어떤 변수의 값이 `null`이 되었다면, 이 변수는 GC가 될 가능성이 있을까요?
  - Reference counting 방식과 이 알고리즘에서 발생할 수 있는 순환 참조(retain cycle)에 대해 설명하세요.
- 기본 타입(Primitive type)과 참조 타입(Reference type)에 대해 설명하세요.
- Call by value와 call by reference
  - 각각의 개념과 그 차이에 대해 설명하세요.
  - 과연 모든 언어에 이 개념이 존재할까요?
- `equals()`와 `hashcode()`
  - `equals()`와 `hashcode()`에 대해 설명하세요.
  - `hashcode()`를 직접 정의해야 한다면, 어떤 점을 염두에 두고 구현 하실건가요?
  - `equals()`를 재정의 해야 할 때, 어떤 점을 염두에 두어야 하는지 설명해 주세요.
- `String` vs `StringBuffer` vs `StringBuilder`
  - 각각의 개념과 그 차이에 대해 설명하세요.
  - Interend String에 대해 설명하세요.
- 업캐스팅과 다운캐스팅에 대해 설명하세요.
- 오토박싱과 오토언박싱에 대해 설명하세요.
- `static`
  - 컴파일 과정에서 `static` 키워드가 붙은 변수나 함수는 어떻게 처리되나요?
  - `static`을 사용하면 어떤 이점이 있고, 어떤 제약이 있나요?
  - `static`과 `static final`은 어떤 차이가 있나요?
  - `final`과 `static final`은 어떤 차이가 있나요?
  - static 클래스와 static 메서드를 비교하세요.
- `final`
  - `final` 키워드를 사용하면, 어떤 이점이 있나요?
  - 그렇다면 컴파일 과정에서, `final` 키워드는 다르게 취급되나요?
- 래퍼(Wrapper) 클래스의 역할과 사용법에 대해 설명하세요.
- 접근 제어자(Access modifier)에 대해 설명하세요.
- 예외 처리
  - `Exception`에 대해 설명해 주세요.
  - 예외를 처리하는 세 가지 방법에 대해 설명해 주세요.
  - `CheckedException`, `UncheckedException`의 차이에 대해 설명해 주세요.
  - 예외 처리가 성능에 큰 영향을 미치나요? 만약 그렇다면, 어떻게 하면 부하를 줄일 수 있을까요?
- Collection 프레임워크에 속한 자료구조들의 종류와 사용법에 대해 설명하세요.
- 쓰레드 (`Thread`)
  - `Thread`의 활용 방법과 주의점에 대해 설명하세요. 
  - `ThreadLocal`에 대해 설명해 주세요. 
- `synchronized`
  - `synchronized` 키워드의 역할과 사용법에 대해 설명하세요.
  - `synchronized` 키워드가 어디에 붙는지에 따라 의미가 약간씩 변화하는데, 각각 어떤 의미를 갖게 되는지 설명하세요.
  - 효율적인 코드 작성 측면에서, `synchronized`는 좋은 키워드일까요?
  - `synchronized`를 대체할 수 있는 자바의 다른 동기화 기법에 대해 설명하세요.
- Stream API와 람다식
  - Stream API의 개념과 활용법에 대해 설명하세요.
  - 람다식의 개념과 사용법에 대해 설명하세요.
  - Stream과 for문의 성능을 비교하세요.
  - Stream을 병렬처리 할 수 있나요?
  - Stream에서 사용할 수 있는 함수형 인터페이스에 대해 설명해 주세요.
  - 가끔 외부 변수를 사용할 때, `final` 키워드를 붙여서 사용하는데 왜 그럴까요? 꼭 그래야 할까요?
- 직렬화(Serialization)란 무엇인가요?
- 리플렉션 (`Reflection`)
    - 리플렉션의 개념과 사용법에 대해 설명하세요.
    - 의미만 들어보면 리플렉션은 보안적인 문제가 있을 가능성이 있어보이는데, 실제로 그렇게 생각하시나요? 만약 그렇다면, 어떻게 방지할 수 있을까요?
    - 리플렉션을 언제 활용할 수 있을까요?
- 어노테이션 (Annotation)
  - 자바에서 어노테이션은 어떤 기능을 하나요?
  - 별 기능이 없는 것 같은데, 어떻게 Spring에서는 어노테이션이 그렇게 많은 기능을 하는 걸까요?
  - Lombok의 @Data를 잘 사용하지 않는 이유는 무엇일까요?
- 제네릭(Generic)의 개념과 사용법에 대해 설명하세요.
- 레코드(Record)란 무엇인가요?

<br>

# 출처
- https://github.com/JaeYeopHan/Interview_Question_for_Beginner
- https://github.com/gyoogle/tech-interview-for-developer
- https://github.com/VSFe/Tech-Interview
