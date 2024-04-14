## OS ch3 🦕

디스크에 있는 것은 프로그램, 메모리에 로드된 것은 프로세스

프로세스는 Stack, Heap, Data, Code로 나뉨

## Process State

프로세스의 상태는 현재 활동에 따라 달라진다.

![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/ba90a3eb-aa6c-4604-8a63-58072d1bbd6a)

- New : 프로세스가 처음 생성되었을 때
- Ready : 프로세스가 프로세서에 할당되기를 기다릴 때
- Running : 프로세스가 할당되어 실행될때
- Waiting :프로세스가 이벤트를 기다릴 때
- Terminated : 프로세스가 실행을 마쳤을 때


## Process Control Block (PCB)
각각의 프로세스는 자신의 정보 묶음인 PCB를 가지고 있음.

PCB에는 프로세스 상태와 프로그램 카운터, 메모리 한계, 레지스터 정보 등이 담겨있음

- Process state : 프로세스 상태
- Program counter : 해당 프로세스가 이어서 실행해야 할 명령의 주소를 가리키는 카운터
- CPU registers : 프로세스가 인터럽트 이후 올바르게 작업을 이어가기 위해 참조하는 CPU 레지스터 값
- CPU-secheduling information : 프로세스의 중요도, 스케쥴링 큐 포인터 등 스케쥴링 파라미터 정보
- Memory-management information : base, limit 레지스터 값, 페이지 테이블 등 메모리 시스템 정보
- Accounting information : 사용된 CPU 총량, 프로세스 개수, 시간 제한 등
- I/O status information : 프로세스에 할당된 입출력 장치 목록, 열리니 파일 목록 등

## Threads
- 프로세스를 쪼개 하나의 프로세스 안에서 동시에 여러 작업 처리 가능
- 싱글 스레드 프로세스는 한번에 하나의 작업만 할 수 있음

## Process Scheduling
멀티 프로그래밍의 목적 : CPU를 최대로 사용하기 위해 항상 일부 프로세스를 실행하는 것

타임 쉐어링의 목적 : 프로세스 간의 CPU를 자주 전환함으로 사용자가 각 프로그램이 실행되는 동안 서로 상호작용할 수 있도록 하는 것

=> 프로세스 스커쥴러는 CPU에서의 프로그램을 실행을 위해 사용 가능할 프로세스 선택하며, 어떤 프로세서에 할당할 것인가 결정하는 일

## Scheduling Queues

- 프로세스가 시스템에 들어오면 잡 큐(Job queue)에 들어감
- 잡 큐는 시스템의 모든 프로세스로 구성되어 있음
- 메인 메모리에서 실행을 기다리는 레디 큐(Ready Queue)에 쌓임
- 입출력 장치를 기다리는 프로세스들은 디바이스 큐 (Device Queue) 들어감

 ## Schedulers
잡 스케쥴러 (= Long-term 스케쥴러) : 레디 큐에 프로세스를 옮기는 것

CPU 스케쥴러 (= Short-term 스케쥴러) : 프로세스를 프로세서에 할당하는 것

- Long-term 스케줄러는 CPU 밖에서 가끔 수행됨. Short-term 스케줄러는 그 반대

## Context Switch
- 프로세스가 실행되다 인터럽트가 발생해 OS가 개입하여 프로세서에 할당된 프로세스를 바꾸는 것
-  시스템 콜을 사용해야 하는 경우 프로세스가 자체적으로 처리 불가능, OS가 개입해야 함
-  프로세스가 다린 프로세스로 스위치할 때, 시스템은 작업중이던 프로세스의 상태를 저장하고 새로운 프로세스의 상태를 로드함
-  컨텍스트 : 시스템에서 활용 가능한 모니터링된 정보를 의미
-  프로세서 입장에서 컨텍스트는 PCB
-  PCB 정보가 바뀌는 것 -> 컨텍스트 스위치
-  컨텍스트 스위치는 오버헤드가 발생하는 작업이기 때문에 자주 일어나면 성능이 저하됨

## Operations on Processes
대부분의 시스템에서 프로세스는 동시에 실행될 수 있고, 동적으로 생성되거나 삭제될 수 있음

시스템은 프로세스 생성, 삭제 메커니즘을 제공해야 함

### 출처 😊
https://itwiki.kr/w/%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4_%EC%83%81%ED%83%9C

https://parksb.github.io/article/7.html
