# CPU 스케줄링

## 스케줄링 개념

<details>  
<summary><h3>CPU 스케줄링의 목적과 필요성에 대해 설명하세요.</h3></summary>

#### 목적
- 공정성: 모든 프로세스가 CPU를 공정하게 사용할 수 있도록 보장하기 위함
- CPU 이용률 극대화: CPU가 쉬지 않고 사용되도록 하여 자원 낭비를 방지하기 위함 

#### 필요성
- 멀티태스킹: 동시에 여러 프로세스를 실행하기 위함
- 우선순위 관리: 높은 우선순위를 가진 프로세스가 먼저 실행될 수 있도록하기 위함 

</details>

<details>  
<summary><h3>I/O bound, CPU bound 프로세스에 대해 설명하세요.</h3></summary>

#### 버스트(Burst)
- CPU 버스트: 프로세스가 CPU를 연속적으로 실행하는 시간
- I/O 버스트: 프로세스가 I/O 작업을 요청하고 기다리는 시간

#### I/O bound 프로세스
- I/O 버스트가 많은 프로세스(e.g. 일반적인 백엔드 API 서버)

#### CPU bound 프로세스
- CPU 버스트가 많은 프로세스(e.g. 동영상 편집 프로그램 등)

<details>  
<summary><h4>듀얼 코어 CPU에서 동작할 CPU bound 프로그램은 몇 개의 쓰레드를 사용하는게 좋을까요?</h4></summary>

코어 개수와 비슷한 개수의 쓰레드를 사용하는 것이 좋음, 즉 2개 ~ 3개의 쓰레드를 사용하는 것이 적절함
</details>

<details>  
<summary><h4>듀얼 코어 CPU에서 동작할 I/O bound 프로그램은 몇 개의 쓰레드를 사용하는게 좋을까요?</h4></summary>

정해진 바는 없으며 상황에 맞게 적절한 개수의 쓰레드를 사용해야함
</details>

</details>

<details>  
<summary><h3>프로세스 우선순위와 스케줄링 큐에 대해 설명하세요.</h3></summary>

</details>

<details>  
<summary><h3>선점형과 비선점형 스케줄링에 대해 설명하세요.</h3></summary>

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
