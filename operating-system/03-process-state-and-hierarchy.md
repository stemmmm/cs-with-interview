# 프로세스 상태와 계층 구조

## 프로세스 상태

<details>
<summary><h3>프로세스 상태에 대해 설명하세요.</h3></summary>

- 운영체제는 여러 프로세스의 상태를 PCB에 기록하여 관리, 각 프로세스는 실행 중 다양한 상태로 전이됨
- 생성: 프로세스, PCB가 생성됐지만 아직 운영체제에 의해 완전히 관리되지는 않는 상태
- 준비: CPU를 할당받아 실행되기를 기다리고 있는 상태, 메모리 등의 자원은 이미 할당됨
- 실행: CPU를 할당받아 명령을 실행 중인 상태, 스케줄러에 의해 할당된 시간만큼만 실행 가능
- 대기: 입출력 작업이나 다른 이벤트가 완료되기를 기다리고 있는 상태
- 종료: 프로세스가 운영체제에 의해 종료된 상태, 프로세스의 모든 자원과 PCB가 메모리에서 제거됨

![image](https://github.com/user-attachments/assets/c3f5fe1c-8448-4853-9454-ca3b69a26673)
</details>

<details>
<summary><h3>프로세스 상태 전이에 대해 설명하세요.</h3></summary>

- 생성 -> 준비(admitted): 새로운 프로세스가 생성되면 준비 상태로 전이
- 준비 -> 실행(scheduler dispatch): 스케줄러에 의해 CPU가 할당되면 실행 상태로 전이
- 실행 -> 준비(interrupt): 할당된 시간이 종료되면 준비 상태로 전이
- 실행 -> 대기(I/O or event wait): 입출력 요청이나 특정 이벤트를 기다려야 하면 대기 상태로 전이
- 대기 -> 준비(I/O or event completion): 요청한 작업이 완료되면 준비 상태로 전이
- 실행 -> 종료(exit): 프로세스가 모든 작업을 완료하면 종료 상태로 전이
</details>

<br>

## 프로세스 계층 구조

<details>
<summary><h3>프로세스 계층 구조에 대해 설명하세요.</h3></summary>

- 운영체제는 프로세스를 계층적으로 관리
- 프로세스 계층 구조는 부모-자식 관계를 기반으로 하며, 트리 구조로 표현될 수 있음
</details>

<details>
<summary><h3>부모 프로세스와 자식 프로세스에 대해 설명하세요.</h3></summary>

- 프로세스는 실행 중 다른 프로세스를 생성할 수 있음
- 새 프로세스를 생성한 프로세르를 부모 프로세스, 부모 프로세스에 의해 생성된 프로세스를 자식 프로세스라고 부름
- 부모 프로세스와 자식 프로세스는 엄연히 다른 프로세스이므로 서로 다른 프로세스 식별자(PID)를 가짐
</details>

<details>
<summary><h3>리눅스나 유닉스의 루트 프로세스에 대해 설명하세요.</h3></summary>

- 루트 프로세스는 시스템의 부팅 과정에서 최초로 실행되는 프로세스이며 모든 프로세스의 부모임
- 루트 프로세스의 PID는 항상 1임
- 리눅스의 루트 프로세스는 `systemd`, 유닉스의 루트 프로세스는 `init`, macOS의 루트 프로세스는 `launchd`

<img width="1202" alt="스크린샷 2024-08-24 오후 7 40 15" src="https://github.com/user-attachments/assets/495a2345-a2e1-45e8-80f0-97a46a140a55">
</details>

<details>
<summary><h3>프로세스를 생성하는 시스템 콜에 대해 설명하세요.</h3></summary>

#### `fork`
- 현재 실행중인 프로세스의 복사본을 자식 프로세스로 생성
- 자식 프로세스는 부모 프로세스의 메모리, 파일 디스크립터, 환경 변수 등을 복사받음(PID는 다름)

> **파일 디스크립터**  
> 프로세스에서 파일과 같은 I/O 자원에 접근하기 위한 추상화된 참조 정수 식별자

#### `exec`
- 현재 프로세스의 메모리 공간을 새로운 프로그램으로 덮어쓰고, 새로운 프로램을 실행함
- `fork`로 만들어진 자식 프로세스는 `exec`을 통해 자신의 메모리 공간을 새로운 프로그램으로 덮어씀
- 일반적으로 `fork`와 `exec` 시스템 콜을 함께 사용해 자식 프로세스에서 새로운 프로그램을 실행함
- 만약 부모와 자식 프로세스에서 동일한 프로그램을 계속 실행하길 원하는 경우, 자식 프로세스에서 `exec`을 호출하지 않음
</details>

<details>
<summary><h3>고아 프로세스와 좀비 프로세스에 대해 설명하세요.</h3></summary>

#### 고아 프로세스
- 정의: 부모 프로세스가 종료되었지만 여전히 실행 중인 자식 프로세스
- 원인: 부모 프로세스가 자식 프로세스보다 먼저 종료되거나 비정상적으로 종료됐을때 발생
- 해결: 루트 프로세스가 고아 프로세스의 새로운 부모가 되어 관리함

#### 좀비 프로세스
- 정의: 자식 프로세스는 종료되었지만 부모 프로세스가 자식의 종료 상태를 수집 후 정리하지 않아 메모리를 계속 차지하고 있는 상태
- 원인: 부모 프로세스가 자식의 종료 상태를 수집하는 `wait` 시스템 콜을 호출하지 않은 경우 발생
- 해결: 부모 프로세스에서 `wait` 시스템 콜 호출
</details>

<br>

## 실습

<details>
<summary><h3>본인이 사용하는 언어의 쓰레드 생명 주기를 설명하세요.</h3></summary>

#### 스레드 생명 주기
- New: 스레드가 생성되었으나 시작되진 않은 상태
- Runnable: 스레드가 실행 중이거나 실행될 준비가 완료된 상태
- Blocked: 스레드가 동기화 락을 기다리는 상태
- Waiting: 스레드가 다른 스레드의 작업이 완료되길 무한정 기다리는 상태
- Timed Waiting: 스레드가 다른 스레드의 작업이 완료되길 일정 시간 동안 기다리는 상태
- Terminated: 스레드의 실행이 완료돼 종료된 상태

![image](https://github.com/user-attachments/assets/5634c746-2040-4cb8-9add-4678d8758571)

<br>

#### `join`

##### `join()`
- `join()`메서드를 호출한 부모 스레드는 자식 스레드가 `TERMINATED` 상태가 될 때까지 `WAITING` 상태임
- 자식 스레드가 `TERMINATED` 상태가 되면 부모 스레드는 다시 `RUNNABLE` 상태로 전환됨

```java
public class Join {
    public static void main(String[] args) {
        SumTask task1 = new SumTask(1, 50);
        SumTask task2 = new SumTask(51, 100);

        Thread thread1 = new Thread(task1);
        Thread thread2 = new Thread(task2);

        thread1.start();
        thread2.start();

        thread1.join();  // thread1 종료될 때까지 main 스레드 무한 대기
        thread2.join();  // thread2 종료될 때까지 main 스레드 무한 대기

        int totalSum = task1.result + task2.result;
        System.out.println("total sum: " + totalSum);
    }

    static class SumTask implements Runnable {
        int startValue;
        int endValue;
        int result = 0;

        public SumTask(int startValue, int endValue) {
            this.startValue = startValue;
            this.endValue = endValue;
        }

        @Override
        public void run() {
            int sum = 0;

            for (int i = startValue; i <= endValue; i++) {
                sum += i;
            }

            result = sum;
        }
    }
}
```

##### `join(ms)`
- `join(ms)` 메서드를 호출한 부모 스레드는 지정한 시간만큼 `TIMED_WAITING` 상태로 대기함
- 부모 스레드는 지정한 시간이 지나면 다시 `RUNNABLE` 상태로 전환됨

<br>

#### 인터럽트
- 다른 스레드의 작업을 중간에 중단하기 위해 사용하는 신호

```java
public class Interrupt {
    public static void main(String[] args) {
        MyTask task = new MyTask();
        Thread thread = new Thread(task);
        thread.start();

        Thread.sleep(100);
        thread.interrupt();
        System.out.println("스레드 인터럽트 상태1: " + Thread.currentThread().getState());  // true
    }

    static class MyTask implements Runnable {
        @Override
        public void run() {
            while (!Thread.interrupted()) {  // 스레드 인터럽트 상태 정상(false)으로 변경
                System.out.println("작업 중...");
            }

            System.out.println("스레드 인터럽트 상태2: " + Thread.currentThread().getState());  // false

            try {
                Thread.sleep(1_000);
                System.out.println("자원 정리 완료!");
            } catch (InterruptedException e) {
                System.out.println("인터럽트 발생하여 자원 정리 실패");
                System.out.println("스레드 인터럽트 상태3: " + Thread.currentThread().getState());
            }
        }
    }
}
```

<br>

#### `yield`
- 다른 스레드에게 CPU를 양보하고 싶을때 사용
- `yield` 메서드를 호출한 스레드는 `RUNNABLE` 상태를 유지하며 스케줄링 큐(대기 큐)로 들어감
- 따라서 양보할 스레드가 없거나 CPU가 남으면 `yield` 메서드를 호출해도 계속 본인이 실행될 수 있음

```java
public class Yeild {
    static final int THREAD_COUNT = 1_000;  // 양보할 수 있도록 많은 스레드 생성

    public static void main(String[] args) {
        for (int i = 0; i < THREAD_COUNT; i++) {
            Thread thread = new Thread(new MyTask());
            thread.start();
        }
    }

    static class MyTask implements Runnable {
        @Override
        public void run() {
            for (int i = 0; i < 10; i++) {
                System.out.println(Thread.currentThread().getName() + ": " + i);
                Thread.yield();
            }
        }
    }
}
```
</details>
