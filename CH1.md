# Operating-System 🦕
## ch1

## What Operating-Syestems Do
OS -> 컴퓨터의 하드웨어를 관리, 하드웨어와 소프트웨어, 사용자를 매개하는 프로그램

Kernel -> os의 핵심이며 실체 => 일반적으로 OS와 Kernel은 동일시 됨. 즉, Kernel이 같다면 같은 OS로 취급

OS는 Kernel과 Kernel Module들로 구성됨

Computer-System
1. 하드웨어 (CPU, Memory,I/0 Device etc..)
2. 운영체제 
3. 어플리케이션 프로그램 (Web broswer, Word processor etc...)
4. 유저

OS의 역할은 USER View와 SYstem View로 나눌 수 있음

## User View
Goal : User가 수행하는 작업 최대화

-> 사용의 용이성을 위해 설계, 성능에 신경 씀. 

-> Resource Utilization (컴퓨터 자원 사용)을 신경 쓰지 않게 도움.

## System View
-> Resource allocator (자원 할당자) : CPU 시간, 메모리 공간, 저장장치 공간, 입출력 장치 등의 자원을 관리함.

-> Control program (제어 프로그램) : 부적절한 사용을 방지하기 위해 사용자 프로그램의 수행을 제어함.

## Computer-System Organization
일반적인 컴퓨터 시스템은 하나 이상의 CPU와 Device Controller로 구성되어 있음.

-> 이들은 공통 버스로 이어져 메모리를 공유함

![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/d13ef4dc-8517-44d7-8929-1c90c3fe83c5)

## Computer Startup
Bootstrap Program : 전원을 켜거나 재부팅할 때 로드되는 초기화 프로그램

-> ROM(Read Only Memory)이나 EEPROM(Electrically Eraable Programmable Read Only Memory)에 저장.

-> 주로 Firmware(펌웨어)라고 불림.

Bootstrap program은 시스템을 초기화하고 Boot loader를 실행, Boot loader는 OS를 실행.

## Computer-System Operatrion
I/O Device와 CPU는 동시 실행 가능. 

Interrupt (인터럽트) : Device controller가 CPU에게 이벤트 발생 알리는 것

-> 보통 컴퓨터는 여러 작업을 동시에 처리하는데, 이때 당장 처리해야 하는 일이 생겨서 기존의 작업을 잠시 중단해야 하는 경우 Interrupt 신호 보냄.

-> 그러면 Kernel은 작업을 멈추고 Interrupt를 처리한 뒤 기존 작업으로 돌아옴.

![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/b06adf2a-74dd-43a9-b169-3a4b711a69a4)

Interrupt는 하드웨어나 소프트웨어에 의해 발생할 수 있음. 

소프트웨어에 의해 발생하는 Interrupt는 Trap이라고 부름.

하드웨어의 경우 : System bus를 통해 CPU에 신호를 보냄으로서 Interrupt 발생시킴

소프트웨어의 경우 : System call이라는 특별한 명령으로 Interrupt 발생시킴.


## Common Fuctions of Interrupts
보통 컴퓨터는 여러 작업을 동시에 처리하는데, 만약 CPU가 인터럽트 신호를 받으면, 하던 일 잠시 멈추고 메모리의 고정된 위치를 찾음. 

이 위치는 Interrupt vector에 저장되어 있음.

Interrupt vector : Interrupt를 처리할 수 있는 Service routine들의 주소를 가지고 있는 공간, 파일 읽기/쓰기와 같은 중요한 동작들이 하드코딩되어 있음.

Interrupt를 처리하면 CPU는 원래 작업으로 돌아옴. <- 이 과정은 사용자가 눈치채지 못할 정도로 빠를 수도, 매우 느릴수도 있음.

어떤 값을 0으로 나누는 것 (Division by zero)도 Interrupt이며, 이러한 내부 Interrupt는 Exception(예외)라고 부른다.

## Interrupt Handling
OS는 대부분 Interrupt driven(인터럽트 주도적)임. 

인터럽트가 발생하기 전까지 CPU는 대기 상태.

반면, Polling의 경우 주기적으로 이벤트를 감시해 처리 루틴을 실행.

-> 이 경우 컴퓨팅 자원 낭비가 심함. 그래서 Interrupt driven으로 보통 설계함.

## Storage Structure
Kernel은 Executor(실행기)를 통해 프로그램을 실행시킴. 

Executor는 Storage(기억장치)에서 exe파일을 가져오고, Kernel이 이것을 Memory에 할당해 실행.

=> 모든 프로그램은 메인 메모리에 로드되어 실행되며, 메인 메모리는 보통 RAM(Random-Access Memory)라고 부름.

하지만, RAM은 모든 프로그램을 담기에는 너무 작고, 비싸고, Volatile(휘발성) 장치임.

그래서, Secondary storage(보조기억장치)를 사용함.

-> Magnetic tapes(자기 테이프), Optical disk(광학 디스크), Magnetic disk(자기디스크), SSD(Solid-state Disk)

이들은 Non-volatile(비휘발성 -> NVS라고 부르기도 함)이고, 용량이 크고, 저렴함.

## I/O Structure

기억장치는 여러 I/O Device 중 하나일 뿐임. 컴퓨터는 다양한 I/O Device를 가지고 있으며, I/O controller는 각각 다른 장치를 담당함.

컴퓨터는 이 controller 덕분에 다양한 장치를 사용할 수 있음. 

OS는 각각의 Device controller는 제어하기 위한 Device driver를 가짐.

1. 입출력 명령을 수행하기 위해 Device driver는 Device controller의 Register를 로드함.
2. Device controller는 Register에서 "키보드로부터 문자 읽어오기"와 같은 동작을 읽고, 장치에서 Local Buffer로 데이터를 전송함. 
3. 전송이 끝나면 Device controller는 Device driver에게 Interrupt를 보내 동작이 끝났음을 알리고, Device driver의 통제권을 OS에게 동려줌. (이때 입력받은 데이터나 상태 정보를 넘겨주기도 함.)

사용자 프로그램은 Kernel과 사용자 프로그램을 매개하는 인터페이스인 System call을 통해 입출력 요청할 수 있음. 

## Direct Memory Access Structure

과거에는 장치 데이터를 처리하기 위해 CPU를 거쳐 메모리에 로드하는 방식(PIO: Programmed I/O)을 사용했으나, CPU 자원이 너무 많이 소모되기 때문에 이제 DMA 사용함.

DMA : 장치와 메모리를 직접 연결하는 방식, 버스가 지원하는 기능임.

메모리의 일정 부분은 DMA에 사용될 영역으로 지정되며, DMA를 제어하는 controller는 DMA controller라고 부름.

장치의 데이터는 Device controller에 의해 직접 메모리에 전달되며, CPU에서는 데이터 이동이 완료되었다는 Interrupt만 한 번 일어남. 

=> CPU가 하는 일이 줄어들어 성능이 좋아짐.

## Computer-System Architecture

현대 컴퓨터 시스템은 보통 폰 노이만 구조를 따름.
![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/385cdeee-526d-4873-b403-2fb61bbc606b)

## Single-Processor Systems

과거 대부분의 컴퓨터는 Single-processor를 사용함. 

Single-processor: 하나의 메인 CPU만 탑재, 장치에 따라 특별한 목적을 가진 프로세서가 들어감.

Disk processor는 디스크 연산만, Keyboard processor는 키보드 연산만 수행하는 식임.

## Multiprocessor Systems

이제 일반적인 컴퓨터는 Multiprocessor를 사용함.(서버 컴퓨터에만 적용되다가, 모바일 기기에도 적용됨)

멀티 프로세서 컴퓨터는 2개 이상의 processor를 가짐.

멀티 프로세서의 장점
1. Throughput(처리량)의 증가 : 프로세서가 늘어나면 더 빠른 시간 안에 연산 수행 가능. 한없이 성능이 좋아지거나, 1:1으로 좋아지는 것은 아님.
2. 규모의 경제 : 여러대의 싱글 프로세서 시스템을 구출하는 것보다 멀티 프로세서 시스템이 더 경제적임.
3. 신뢰성의 증가 : 기능이 여러 프로세서에 분산되면, 하나의 프로세서가 멈춰도 전체 시스템이 멈추지 않음.

Graceful degradation(우아한 성능저하) : 성능이 나빠지지만 작동은 가능하도록 하는 것

Fault tolerant(장애 허용 시스템) : 성능을 저하함으로서 작업을 계속 유지하는 시스템

멀티프로세서 시스템은 Asymmetric multiprocessing(비대칭 멀티프로세싱)과 Symmetric multiprocessing(대칭 멀티프로세싱)으로 나뉨


Asymmetric multiprocessing(비대칭 멀티프로세싱) : 

관료주의적 회사, 보스 프로세서가 시스템 제어하고 다른 프로세서들은 보스의 지시를 받음. <- Load balancing(부하 분산)이 효율적

대신, 보스가 멈추면 부하들도 모두 멈춤.

Symmetric multiprocessing(대칭 멀티프로세싱) : 

보스가 없는 자유로운 회사, 모든 프로세서들이 하나의 메모리를 공유하고, 동일한 작업을 병렬적으로 수행함.

만약, 프로세서에 이상이 생겨 작동을 멈춰야 한다면 자신이 수행하던 작업을 다른 프로세서들에게 나눠주고 자신만 재부팅 함.

재부팅 후 문제가 해결된다면, 다시 작업을 나눠 받음.

-> 비대칭 멀티프로세싱 시스템의 단점을 보완할 수 있는 아키텍처이기 때문에 대부분의 컴퓨터 시스템은 대칭 멀티프로세싱을 사용함.

멀티 프로세서 시스템의 CPU들은 각자의 레지스터와 캐시를 갖고 있음. 만약 CPU가 여러개라면 돌아가며 작업을 해야하는데, 다른 CPU가 작업하는 동안 나머지 CPU는 놀게 됨.

![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/58ca4369-12f3-48ba-973a-6ff21e8cf4a5)

## Dual-Core Design

CPU가 늘어나며 프로세서 간 통신에 많은 비용이 들어 효율이 계속 좋아지지는 않음.

최근 CPU 설계 트렌드는 하나의 Chip에 Cores를 늘리는 것.

-> Multicore

코어는 동일한 성능의 CPU 여러 개를 1개의 칩 속에 집접한 것.

-> On-chip communication(칩 내부 통신)이 Between-chip communication(칩 사이의 통신)보다 빠름.

-> 전력 소모량도 더 적음.

![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/3ebcbfe5-22c7-4943-9073-12fb2e4bc67e)

## Clustered Systems

Clustered Systems : 멀티프로세서 시스템의 일종, 여러개의 CPU를 모아 놓은 구조

Multiprocessor system은 여러 cpu가 하나의 시스템 이루지만, Clustered System은 여러 독립적인 시스템이 모여 하나의 시스템을 이루는 것.

-> 이런 시스템을 Loosely coupled(약결합)라고 부름, 각 노드들은 싱글 프로세서 시스템일수도, 멀티 코어 시스템일 수도 있음.

클러스터의 정의가 명확히 정해져 있지는 않음, 단지 클러스터 컴퓨터들이 하나의 저장소를 공유하고 이를 LAN(Local-Area Network)와 같은 네트워크로 연결한 시스템을 보통 클러스터 시스템이라고 부름.

클러스터링은 High-avaiability(고가용성) 서비스를 제공하기 위해 사용되며, 단일 컴퓨터보다 훨씬 저렴하게 비슷한 성능을 낼 수 있음.

 클러스터 시스템은 Asymmetric clustering(비대칭 클러스터링)과 Symmetric clustering(대칭 클러스터링)으로 나뉨.

 비대칭 클러스터링에서는 하나의 장비는 Hot-standby(상시 대기 모드)로 작동하며, 서버를 동작시키고 있는 다른 노드들을 모니터링할 뿐 다른 작업은 하지 않음.

 만약, 서버에 문제가 생기면 상시 대기 노드가 서버로서 작동하게 됨.

 대칭 클러스터링은 두개 이상의 노드가 작업을 수행하는 동시에 다른 노드들을 모니터링하는 구조

 이러한 구조는 하드웨어의 자원을 최대로 사용할 수 있어 더 효율적임.

 클러스터 시스템은 여러개의 컴퓨터 시스템이 네트워크로 연결되어 있는 구조이기 때문에 고성능 컴퓨팅 환경을 제공 함

 다만, 단일 시스템에 비해 유지보수가 힘들고, 시스템의 성능이 네트워크 환경에 많은 영향을 받음.

 ## Operating System Structure

 OS의 가장 중요한 부분 중 하나는 MultiProgram 능력

 Multiprogramming : 여러 프로그램을 메모리에 로드해 두고 한 프로세스가 대기 상태가 되면 다른 프로세스의 작업을 수행하는 시스템

 => CPU 사용 효율을 높일 수 있음

 Time sharing(시분할) 시스템 (=Multitasking) : 프로세스마다 작업 시간을 정해두고 번갈아가며 작업하는 방식, 프로세스들이 빠르게 번갈아가며 메모리를 사용.

 사용자 입장에서는 마치 동시에 작동하는 것처럼 보임. <- Response time(반응 시간)을 줄이는 것 중요

 => 여러 작업들을 동시에 메모리에 올리는 방식, OS는 메모리에 자리가 없는 경우를 고려해 어떤 작업을 먼저 처리할지 정해야 함.

 ## Operating-System Operations

 OS는 인터럽트 주도적임. 인터럽트가 없다면 시스템은 인터럽트를 기다림. 

 만약, 사용자 프로그램이 멋대로 하드웨어에 접근해 인터럽트를 보낸다면 문제가 발생함. 

 OS와 사용자는 컴퓨터의 하드웨어, 소프트웨어 자원을 공유하기 때문에 사용자 프로그램이 오류를 일으키지 않도록 방지해야함

 ## Dual-Mode and Multimode Operation

 OS는 사용자 프로그램이 함부로 시스템에 접근하지 못하도록 Mode를 나눠둔다.

 -> User mode, kernel mode

 하드웨어의 Mode bit가 0은 kernel mode 1은 User mode

![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/680eada7-502a-4b4c-9dcc-4e2a2dcaeed5)

이러한 Dual-mode 방식을 사용하면 나쁜 의도를 가진 사용자로부터 OS, 하드웨어를 비롯한 시스템과 사용자를 보호함

하드웨어는 kernel mode일 떄만 Privileged instructions(특권 명령)을 실행함.

만약 User mode에서 특권 명령을 실행하려하면 하드웨어는 이 동작을 막고 OS에 Trap을 보냄.

User mode에서 kernel mode의 기능을 호출하고 싶다면, System-call 이라는 인터페이스를 통해야 함.

## Timer

Timer : OS는 사용자 프로그램이 제어권을 OS에게 넘겨주지 않는 상황을 방지하기 위해 사용

OS 제어권을 보장하기 위해 특정 주기에 Interrupt를 발생시킴.

OS는 카운터를 설정하고, 매 Ticks마다 감소시킴. -> 카운터가 0에 도달하면 Interrupt 발생

## Process Management

디스크에 있으면 프로그램, 메모리에 로드되면 프로세스

프로그램은 하나지만 프로세스는 여러 개 일 수 있음.

프로그램은 Passive(수동적) 존재, 프로세스는 Active(능동적) 존재

프로세스는 프로그램이 어디까지 실행되었는지 북마크하는 Program counter를 가지고 있음

Single-thread 프로세스는 하나의 PC를 가지고 있으며, Multi-threads 프로세스는 여러개의 PC를 가지고 있음.

OS는 프로세스 관리를 위해 CPU에게 프로세스와 쓰레드를 스케쥴링하고, 프로세스를 생성하거나 제거하는 활동을 함.

일시정지하거나 재실행하고, 프로세스의 Synchronization(동기화)와 통신도 제공

## Memory Management

메인 메모리는 computer-system의 핵심이며, 방대한 바이트의 배열임.

각 Byte는 그들만의 주소를 가짐.

이후 프로그램이 실행될 때 프로그램은 Abolute addresses(절대 주소)로 Mapping되어 메모리에 로드됨. 

 메모리 관리는 여러 요인을 고려해야 하는 작업, 특히 시스템의 하드웨어 설계를 신경써야 함.

 OS는 메모리 관리를 위해 메모리 어떤 부분이 어디에 쓰이는지, 누가 사용하고 추적하고, 어떤 프로세스와 데이터가 메모리의 안팎으로 옯겨질지 결정함.

 또한 메모리 공간을 할당하고 해제하는 것도 OS가 함.

 ## Storage Management

 OS는 저장장치의 물리적 속성을 추상화해 File이라는 논리적 저장 단위로 정의

 파일을 Physical media(물리적 매체)에 담거나 저장장치의 파일에 접근하기도 함.

 ## File-System Management

 파일 관리는 OS가 하는 일 중 가장 눈에 잘 보이는 요소

 OS는 파일을 생성, 제거, 읽기, 쓰기를 함.

 ## Mass-Storage Management

 프로그램은 디스크에 담겨 있으며, 메인 메모리에 로드되어 실행 됨. 

 많은 사람들이 Tertiary storage devices(제 3의 저장장치)를 사용함.

 저장 장치들은 WORM (Write-Once, Read-Many-Times)와 RW(Read-Write) 형식에 차이가 있음.

 NTFS, FAT가 파일 저장 형식이며, 이를 File-system 이라고 부름

 파일 시스템이 다르면 읽기는 가능하지만 쓰기가 불가능함

 ## Caching

 캐싱은 컴퓨터 시스템에서 중요한 부분.

캐시는 굉장히 빠르고 작은 저장장치이며, 캐싱은 캐시 메모리를 사용해 컴퓨터의 속도를 높이는 기술이다.

데이터를 디스크에서 직접 가져오는 것은 너무 느려 캐시에 자주 사용될 것 같은 데이터를 미리 담아두고 CPU나 디스크가 캐시의 데이터를 참조할 수 있도록 함.

파일의 중복성이 증가하지만, 속도도 증가함.

캐싱은 Locality(지역성) 원리를 사용함.

지역성은 Temporal locality(시간 지역성)과 Spatial locality(공간 지역성)으로 나뉨.

시간 지역성 : 한 번 접근한 데이터에 다시 접근할 확률이 높다는 것.
공간 지역성 : 특정 데이터와 가까운 메모리 주소에 있는 다른 데이터들에게도 접근할 가능성이 높다는 것

```
for (inti = 0; i<10; i++) { ... }
```

위 코드에서 변수 i가 그 예시임.

공간 지역성은 특정 데이터와 가까운 메모리 주소에 있는 다른 데이터들에도 접근할 가능성이 높다는 것.

```
for (int i = 0; i<10; i++) {
 arr[i] += 1;
}
```

배열 변수 arr의 0번 요소부터 순서대로 9번 요소까지 접근함. 메모리 공간에 배열의 요소들은그 순서대로 붙어 할당되니, 실제로 가까운 메모리 공간에 연속적으로 접근하고 있음.

캐시는 한 메모리 주소에 접근했을 때 그 주변의 메모리 주소도 함께 가져옴.

## I/O System

OS는 모든 입출력 장치를 파일로 취급함.

오직 Device driver만이 장치의 자세한 정보를 알고 있음

## Protection and Security

컴퓨터 시스템은 여러 사람들이 사용하기 때문에 보안과 보호가 중요함. 

OS는 내외부로부터 컴퓨터를 위험하게 만드는 요소를 막기 위해 다양한 활동을 함. (User mode 와 Kernel mode를 나누는 것도 보호의 일종)

Privilege escalation(권한 확대) : 컴퓨터 시스템의 권한을 여러 층으로 나누고, 사용자의 권한을 구분해 어떤 행동이나 기준에 따라 사용자의 권한을 상승시키는 시스템

권한 확대는 수직 권한 확대와 수평 권한 확대로 나눌 수 있음

수직 권한 확대 : 임의의 코드를 실행시켜 더 높은 권한을 얻는 행위
수평 권한 확대 : 안드로이드 루팅, ios 탈옥

## Kernel Data Structures

Kernel 구현에는 기본적인 List, Stack, Queue, Linked list 등의 자료구조가 사용됨. 

특히 Tree는 상당히 효율적인 시간 복잡도를 가질 수 있기 때문에 자주 사용됨.

## Computing Environments

Mobile computing 환경은 컴퓨터의 접근성을 높였고, 다양한 센서를 통해 사용자와의 인터페이스를 확장 시킴

Distributed computing(분산형 컴퓨팅), Client-Server computing(클라이언트-서버 컴퓨팅), Peer-to-Peer computing(P2P 컴퓨팅) 등 다양한 컴퓨팅 환경 있음

특히 클라이언트 컴퓨팅은 AWS(Amazon Web Service)를 통해 잘 알려져 있음.

현대 컴퓨팅 환경의 가장 큰 특징은 휴대성, 가상화, 멀티코어가 있음.

## Open-Source Operating Systems

세상에는 많은 오픈소스 OS가 있음. 오픈소스 OS 개발에는 누구나 참여할 수 있고, 이를 이용해 새로운 운영체제를 만들 수도 있음.




출처 : https://parksb.github.io/article/5.html 😘









