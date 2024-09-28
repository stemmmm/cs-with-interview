# 동기화 기법

<details>  
<summary><h3>원자적 연산에 대해 설명하세요.</h3></summary>

- 더 이상 나눌 수 없는 단위의 연산
- 실행 중간에 끼어들 수 없고, 연산이 완전히 실행되거나 전혀 수행되지 않는 방식으로 동작함(all or nothing)
- 자바의 경우 `synchronized`나 `Lock`을 사용해 여러 연산을 하나의 원자적인 단위로 묶을 수 있음
- 원자적이지 않은 연산의 경우 멀티스레드 환경에서 동기화 문제가 발생할 수 있음
</details>

<details>  
<summary><h3>뮤텍스 락에 대해 설명하세요.</h3></summary>

</details>

<details>  
<summary><h3>세마포어에 대해 설명하세요.</h3></summary>

</details>

<details>  
<summary><h3>모니터에 대해 설명하세요.</h3></summary>

</details>

<details>  
<summary><h3>CAS 연산에 대해 설명하세요.</h3></summary>

- 하드웨어 차원에서 구현된 원자적 연산이며, CAS(Compare-and-Swap) 연산을 사용하면 락을 사용하지 않고도 일정 부분 원자적 연산을 수행할 수 있음
- CAS 연산의 원자성은 CPU 차원에서 보장되며, 메모리 특정 위치의 값이 예상한 값과 일치하면 새로운 값으로 변경하는 형태로 동작함
- 만약 현재 값이 예상한 값과 일치하지 않으면, 값을 변경하지 않고 busy waiting 방식으로 재시도함
- 따라서 충돌이 적은 환경에서는 락보다 성능이 좋지만, 충돌이 많이 발생하는 환경에서는 락에 비해 성능이 떨어질 수 있음
- 일반적인 경우, 동기화 락을 사용하고 간단한 연산의 경우에만 CAS 연산의 사용을 권장함
<details>  
  
<summary><h4>자바의 CAS 연산에 대해 설명하세요.</h4></summary>

- 자바에서는 `java.util.concurrent.atomic` 패키지 내의 `Atomic` 클래스들이 내부적으로 CAS 연산을 사용하여 원자성을 보장함
  
```java
import java.util.concurrent.atomic.AtomicInteger;

public class Main {
    public static void main(String[] args) {
        AtomicInteger atomicInteger = new AtomicInteger();  // 초기값: 0
        System.out.println("초기값: " + atomicInteger.get());

        // 현재 값 0이면 1로 세팅(원자적 실행)
        boolean result1 = atomicInteger.compareAndSet(0, 1);
        System.out.println("result1: " + result1);
        System.out.println("현재값: " + atomicInteger.get());

        // 현재 값 1이라 실패(원자적 실행)
        boolean result2 = atomicInteger.compareAndSet(0, 1);
        System.out.println("result2: " + result2);
        System.out.println("현재값: " + atomicInteger.get());
    }
}
```
</details>
</details>

<details>  
<summary><h3>자바의 `synchronized` 키워드에 대해 설명하세요.</h3></summary>

</details>

<details>  
<summary><h3>자바의 `Lock` 인터페이스와 `ReentrantLock`에 대해 설명하세요.</h3></summary>

</details>

<details>  
<summary><h3>자바에서 `Lock` 인터페이스와 `ReentrantLock`을 사용해 생산자-소비자 문제를 해결하는 방법에 대해 설명하세요.</h3></summary>


<details>  
<summary><h4>자바의 `BlockingQueue`에 대해 설명하세요.</h4></summary>

</details>
</details>

<details>  
<summary><h3>자바의 동시성 컬렉션에 대해 설명하세요.</h3></summary>

</details>
