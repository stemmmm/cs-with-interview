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

#### 개념
- 상호 배제를 위한 동기화 기법
- 즉, 임계 구역에 한번에 하나의 스레드만 접근할 수 있도록 함

#### 동작
1. 락 획득: 스레드는 임계 구역에 진입하기 전 뮤텍스 락 획득을 요청하는데, 만약 뮤텍스 락이 다른 스레드에 의해 사용 중이라면, 해당 스레드는 락이 해제될 때까지 대기 상태로 전환되거나 busy waiting 함
2. 임계 구역 진입: 뮤텍스 락을 획득한 스레드는 임계 구역에 진입해 공유 자원을 안전하게 접근 및 수정할 수 있음
3. 락 해제: 스레드가 임계 구역 내에서 작업을 완료하면, 뮤텍스 락을 해제하여 다른 스레드가 임계 구역에 진입할 수 있도록 함

#### 코드
```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class Counter {
    private int count = 0;
    private final Lock lock = new ReentrantLock();

    public void increment() {
        lock.lock();  // 뮤텍스 락 획득

        try {
            count++;
        } finally {
            lock.unlock();  // 뮤텍스 락 해제
        }
    }

    public int getCount() {
        lock.lock();

        try {
            return count;
        } finally {
            lock.unlock();
        }
    }
}
```
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

#### `synchronized`
- `synchronized` 키워드를 사용해 임계 영역을 보호하면 여러 스레드가 동시에 하나의 공유 자원에 접근하지 못하며, 이를 동기화라 부름
- 모든 객체는 내부에 자신만의 락(lock)을 가짐
- 특정 메소드나 블록을 `synchronized` 키워드로 감싸면, 한 스레드가 락을 획득해 해당 영역의 코드를 실행하는 동안 다른 스레드는 `BLOCKED` 상태로 락을 기다림
- 메소드 레벨에 `synchronized` 키워드를 사용해 동기화하는 것보다는 필요한 부분만 `synchronized` 블록으로 선언하는 것이 성능상 유리함

```java
// 메서드 레벨
public synchronized void method() {}

public void method() {
    // 필요한 부분만
    synchronized(this) {
        // ...   
    }
}
```

> **참고**  
> `volatile` 키워드 없이 `synchronized` 키워드만 사용해도 메모리 가시성 문제는 발생하지 않음

#### 단점
- `BLOCKED` 상태로 무한 대기: 락을 획득하기 위해 무한 대기 상태로 들어가며, 이때 CPU 스케줄링 대상에서 제외되고 인터럽트에 응답하지 않음
- 락 획득 순서 미보장: 락을 획득하기 위해 기다리는 `BLOCKED` 상태 스레드들의 락 획득 순서는 보장되지 않음(누가 먼저 락을 얻을지 예측할 수 없음)
</details>

<details>  
<summary><h3>자바의 `Lock` 인터페이스와 `ReentrantLock`에 대해 설명하세요.</h3></summary>

#### `Lock` 인터페이스

> **주의**  
> `Lock` 인터페이스에서의 락은 객체마다 갖는 모니터 락이 아닌 `ReentrantLock`이 제공하는 기능을 말하며, 모니터 락은 `synchronized`에서만 사용함

##### `void lock()`
- 락을 획득함
- 만약 다른 스레드가 이미 락을 획득했다면, 현재 스레드는 락을 획득할 때까지 `WAITING` 상태로 대기함
- `WAITING` 상태지만 인터럽트가 발생해도 무시하고 락 획득을 기다림

##### `void lockInterruptibly()`
- 락을 획득함
- 만약 다른 스레드가 이미 락을 획득했다면, 현재 스레드는 락을 획득할 때까지 `WAITING` 상태로 대기함
- 대기 중 인터럽트가 발생하면 `InterruptedExeption`이 발생하며 락 획득을 포기함

##### `boolean tryLock()`
- 락을 획득하려고 시도한 후, 즉시 성공 여부를 반환함
- 락 획득 성공: `true` 반환 
- 락 획득 실패: 다른 스레드가 이미 락을 가지고 있으면 대기하지 않고 `false` 반환

##### `boolean tryLock(long time, TimeUnit unit)`
- 주어진 시간 동안 락을 획득하려고 시도함
- 주어진 시간 내에 락 획득 성공: `true` 반환
- 주어진 시간 내에 락 획득 실패: 대기 시간이 지나면 `false` 반환

##### `void unlock()`
- 락을 해제함
- 락을 획득한 스레드만 호출할 수 있으며, 락을 해제하면 대기 중인 스레드 중 하나가 락을 획득할 수 있음

<br>

#### `ReentrantLock` 
- `Lock` 인터페이스의 구현체이며 스레드가 공정하게 락을 획득할 수 있는 모드를 제공함
- 공정 모드(fair mode)와 비공정 모드(non-fair mode)가 있음

##### 비공정 모드
- 기본 모드이며, 대기 중인 스레드 중 아무나 락을 획득할 수 있음
- 대기 중인 스레드 중 어떤 것이 락을 획득할지 예측할 수 없으며, 특정 스레드가 계속해서 락을 획득하지 못할 수 있음

##### 공정 모드
- 락을 요청한 순서대로 락을 획득할 수 있음
- 모든 스레드가 락을 요청한 순서대로 공정하게 획득할 수 있지만, 락을 획득하는 속도가 느려질 수 있음
</details>

<details>  
<summary><h3>자바에서 `Lock` 인터페이스와 `ReentrantLock`을 사용해 생산자-소비자 문제를 해결하는 방법에 대해 설명하세요.</h3></summary>

#### 개념
- 멀티스레딩 환경에서 발생할 수 있는 대표적인 동기화 문제
- 여러 생산자와 소비자 스레드가 버퍼를 사용할 때, 스레드 간 동기화 문제가 발생할 수 있음
- 한정된 버퍼 문제(Bounded-buffer problem)라고도 부름
- 생산자(Producer): 데이터를 생산하여 버퍼에 저장하는 역할
- 소비자(Consumer): 버퍼에 저장된 데이터를 사용하는 역할
- 버퍼(Buffer): 생산자가 생산한 데이터를 소비자가 소비하기 전까지 일시적으로 저장하는 공간

#### 해결법: `Object`의 `wait()`, `notify()` 메서드 사용
- 객체 내부에 존재하는 하나의 스레드 대기 집합에서 생산자, 소비자 스레드를 관리
- 즉, `notify()`를 호출할 때 대기 집합에서 어떤 스레드가 선택될지 알 수 없어 생산자가 생산자 스레드를, 소비자가 소비자 스레드를 깨우는 비효율이 발생할 수 있음
- 또한 어떤 스레드가 실행될지 알 수 없으므로 기아 문제가 발생할 수 있음
- `notifyAll()` 메서드를 사용해 기아 문제를 해결할 수 있지만, 매번 모든 스레드를 깨워야하는 비효율 발생

```java
import lombok.extern.slf4j.Slf4j;

import java.util.ArrayDeque;
import java.util.Queue;

@Slf4j
class BoundedQueue {
    private final Queue<String> queue = new ArrayDeque<>();
    private final int maxSize;

    public BoundedQueue(int maxSize) {
        this.maxSize = maxSize;
    }

    // 생산자가 큐에 데이터 저장
    public synchronized void put(String data) {
        while (queue.size() == maxSize) {
            log.info("큐가 가득차 생산자가 대기합니다.");

            try {
                wait();  // 상태 변경(RUNNABLE -> WAITING) 및 락 반납
                log.info("생산자가 깨어났습니다.");
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
        }

        queue.offer(data);
        log.info("생산자가 데이터를 저장한 다음 notify() 메서드를 호출했습니다.");
        notify();  // 대기 중인 스레드 WAITING -> BLOCKED
        // notifyAll();
    }

    // 소비자가 큐에서 데이터 소비
    public synchronized String take() {
        while (queue.isEmpty()) {
            log.info("큐가 비어있어 소비자가 대기합니다.");

            try {
                wait();  // 상태 변경(RUNNABLE -> WAITING) 및 락 반납
                log.info("소비자가 깨어났습니다.");
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
        }

        String data = queue.poll();
        log.info("소비자가 데이터를 꺼낸 다음 notify() 메서드를 호출했습니다.");
        notify();  // 대기 중인 스레드 WAITING -> BLOCKED
        // notifyAll();
        return data;
    }

    @Override
    public String toString() {
        return queue.toString();
    }
}
```

<br>

#### 개선1: `Lock`과 `Condition` 사용
- 생산자가 생산자 스레드를 깨우고, 소비자가 소비자 스레드를 깨우는 비효율을 개선해야함
- 즉, 생산자는 소비자를 깨워야하고, 소비자는 생산자를 깨워야함
- 이는 생산자 스레드 대기 집합과 소비자 스레드 대기 집합을 `Condition`으로 분리하여 해결할 수 있음

```java
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

class BoundedQueue {
    private final Lock lock = new ReentrantLock();
    private final Condition producerCondition = lock.newCondition();  // 생산자 스레드 대기 집합
    private final Condition consumerCondition = lock.newCondition();  // 소비자 스레드 대기 집합

    private final Queue<String> queue = new ArrayDeque<>();
    private final int maxSize;

    public BoundedQueue(int maxSize) {
        this.maxSize = maxSize;
    }

    public void put(String data) {
        lock.lock();
        
        try {
            while (queue.size() == maxSize) {
                log.info("큐가 가득차 생산자가 대기합니다.");

                try {
                    producerCondition.await();
                    log.info("생산자가 깨어났습니다.");
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                }
            }

            queue.offer(data);
            log.info("생산자가 데이터를 저장한 다음 consumerCondition의 signal() 메서드를 호출했습니다.");
            consumerCondition.signal();   
        } finally {
            lock.unlock();
        }
    }

    public String take() {
        lock.lock();

        try {
            while (queue.isEmpty()) {
                log.info("큐가 비어있어 소비자가 대기합니다.");
                
                try {
                    consumerCondition.await();
                    log.info("소비자가 깨어났습니다.");
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                }
            }

            String data = queue.poll();
            log.info("소비자가 데이터를 꺼낸 다음 producerCondition의 signal() 메서드를 호출했습니다.");
            producerCondition.signal();
            return data;
        } finally {
            lock.unlock();
        }
    }

    @Override
    public String toString() {
        return queue.toString();
    }
}
```

<br>

#### 개선2: `BlockingQueue` 사용
- 자바는 생산자-소비자 문제를 해결하기 위한 `BlockingQueue` 인터페이스를 제공함
- `BlockingQueue`의 구현체들은 내부적으로 위 코드와 비슷한 로직으로 동작함
- `ArrayBlockingQueue`, `LinkedBlockingQueue` 등의 구현체 존재
</details>

<details>  
<summary><h3>자바의 동시성 컬렉션에 대해 설명하세요.</h3></summary>

#### 동시성 컬렉션
- 컬렉션 프레임워크 대부분은 thread-safe 하지 않으므로 멀티스레드 환경에서 문제없이 사용할 수 있는 자료 구조가 필요함

##### synchronized 컬렉션
- 프록시 패턴을 사용해 모든 내부 메서드에 `synchronized` 키워드를 붙여 구현된 자료 구조
- 모든 메서드 사용 시 락 오버헤드가 발생하므로 성능이 크게 저하됨

##### `java.util.concurrent`의 동시성 컬렉션
- `synchronized` 컬렉션을 대체할 수 있는 높은 성능의 thread-safe 자료 구조
- 멀티스레드 환경에서 최적화된 동시 접근을 가능케 함
</details>
