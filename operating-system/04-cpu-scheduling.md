# CPU 스케줄링

## 스케줄링 개념

<details>  
<summary><h3>CPU 스케줄링의 목적과 필요성에 대해 설명하세요.</h3></summary>

- 공정성: 모든 프로세스에게 공정하고 합리적으로 CPU 자원을 할당하기 위해
- 자원 낭비 최소화: CPU가 쉬지 않고 사용되도록 하여 자원 낭비를 방지하기 위해
- 멀티태스킹: 동시에 여러 프로세스를 실행하기 위해
- 우선순위 관리: 높은 우선순위를 가진 프로세스가 먼저 실행되기 위해

</details>

<details>  
<summary><h3>I/O bound, CPU bound 프로세스에 대해 설명하세요.</h3></summary>

#### 버스트(Burst)
- CPU 버스트: 프로세스가 CPU를 연속적으로 사용하는 시간
- I/O 버스트: 프로세스가 I/O 작업을 요청하고 완료될 때까지 기다리는 시간

#### I/O bound 프로세스
- CPU 버스트보다 I/O 버스트가 많은 프로세스(e.g. 일반적인 백엔드 API 서버 프로그램 등)
- I/O 요청 후 응답까지 기다리는 시간이 길기 때문에 CPU가 상대적으로 덜 사용됨
- 따라서 I/O bound 프로세스의 상태는 실행보다 대기 상태에 더 오래 머무름

#### CPU bound 프로세스
- I/O 버스트보다 CPU 버스트가 많은 프로세스(e.g. 동영상 편집 프로그램, 머신러닝 프로그램 등)
- 따라서 CPU bound 프로세스의 상태는 대기보다 실행 상태에 더 오래 머무름

<details>  
<summary><h4>듀얼 코어 CPU에서 동작할 I/O bound, CPU bound 프로그램은 각각 몇 개의 쓰레드를 사용하는것이 적절할까요?</h4></summary>

#### I/O bound 프로세스
- 상황에 맞게 적절한 개수의 쓰레드를 사용해야함
- 단, I/O 작업을 하는 동안 CPU가 대기하는 시간이 길어지므로 많은 수의 쓰레드를 사용하는 것이 일반적임

#### CPU bound 프로세스
- 코어 개수와 비슷한 개수의 쓰레드를 사용하는 것이 좋음, 즉 2개 ~ 3개의 쓰레드를 사용하는 것이 적절함
- 불필요하게 많은 개수의 쓰레드를 사용하면 컨텍스트 스위칭 오버헤드가 심해짐
</details>
</details>

<details>  
<summary><h3>프로세스 우선순위와 스케줄링 큐에 대해 설명하세요.</h3></summary>

#### 프로세스 우선순위
- 운영체제는 프로세스가 중요도에 따라 실행될 수 있도록 우선순위를 부여하며, 각 프로세스의 우선순위 정보는 PCB에 저장됨

#### 스케줄링 큐
- 운영체제가 모든 PCB를 확인해 실행시킬 프로세스를 결정할 순 없으므로, 스케줄링 큐를 통해 프로세스 상태를 관리함
- 준비 큐: CPU를 이용하고 싶은 프로세스들이 대기하는 큐
- 대기 큐: I/O 장치를 이용하고 싶은 프로세스들이 대기하는 큐

</details>

<details>  
<summary><h3>선점형과 비선점형 스케줄링에 대해 설명하세요.</h3></summary>

#### 선점형 스케줄링
- 운영체제가 실행중인 프로세스로부터 자원을 강제로 뺏어 다른 프로세스에 할당할 수 있는 스케줄링 방식
- 자원을 공정하게 분배할 수 있지만 컨텍스트 스위칭 오버헤드 존재
- 현재 대부분의 운영체제가 사용중인 방식

#### 비선점형 스케줄링
- 운영체제가 실행중인 프로세스로부터 자원을 강제로 뺏을 수 없는 스케줄링 방식
- 현재 실행중인 프로세스가 종료되거나 스스로 대기 상태가 되기 전까진 자원을 뺏을 수 없음
- 컨텍스트 스위칭 오버헤드는 비교적 적지만, 자원을 공정하게 분배받지 못함

</details>

<details>  
<summary><h3>단기, 중기, 장기 스케줄러에 대해 설명하세요.</h3></summary>

</details>

<br>

## 스케줄링 알고리즘

<details>  
<summary><h3>FCFS(First Come First Served) 스케줄링에 대해 설명하세요.</h3></summary>

<details>  
<summary><h4>Convoy effect에 대해 설명하세요.</h3></summary>

</details>
</details>

<details>  
<summary><h3>SJF(Shortest Job First) 스케줄링에 대해 설명하세요.</h3></summary>

</details>

<details>  
<summary><h3>RR(Round Robin) 스케줄링에 대해 설명하세요.</h3></summary>

<details>  
<summary><h4>Time slice에 따른 trade-off를 설명하세요.</h3></summary>

</details>
</details>

<details>  
<summary><h3>SRT(Shortest Remaining Time) 스케줄링에 대해 설명하세요.</h3></summary>

</details>

<details>  
<summary><h3>우선순위 스케줄링에 대해 설명하세요.</h3></summary>

<details>  
<summary><h4>Starvation 문제와 그 해결법에 대해 설명하세요.</h4></summary>

</details>
</details>

<details>  
<summary><h3>Multilevel queue에 대해 설명하세요.</h3></summary>

</details>

<details>  
<summary><h3>Multilevel feedback queue에 대해 설명하세요.</h3></summary>

</details>

<br>

## 응용 문제

<details>  
<summary><h3>쓰레드는 어떤 방식으로 스케줄링하나요?</h3></summary>

</details>
