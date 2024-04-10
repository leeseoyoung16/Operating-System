## Operating System ch2 🦕

# Operating-System service

![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/7d2f6cb1-57d0-4217-a790-02bcadccef03)

## UI(User Interface)

- 사용자와 컴퓨터 시스템이 만나는 지점

  #### CLI (Command-Line Interface)
  
  - 사용자가 텍스트를 통해 명령을 내리는 인터페이스 (인터페이스를 제공하는 프로그램 -> Shell)

  #### Batch Interface

  - 명령을 파일에 넣어두고, 파일이 실행되며 명령을 실행하는 인터페이스
 
  #### GUI (Graphical User Interface)

   - 사용자는 키보드 타이핑, 마우스 클릭, 손가락 터치 등 다양한 방법으로 명령을 내리는 인터페이스

### Program execution (프로그램 실행)

 - 시스템은 프로그램을 메모리에 로드하고, 이를 실행할 수 있어야 함
 - 프로그램을 정상 혹은 비정상적으로 실행 끝낼 수 있어야 함

### I/O operation (입출력 명령)

- 프로그램이 입출력을 필요로 하면, OS는 입출력 명령을 수행해야 함
- 이때, 사용자가 직접 입출력 장치를 조작하지 않고 OS를 거쳐 수행해야 함

### File-system manipulation (파일 시스템 조작)

- 파일을 읽고, 쓰고, 만들고, 지울 수 있어야 함
- 사용자가 파일에 접근하지 못하도록 막을 수 있어야 함

### Communications (통신)

- 프로세스 간 정보를 교환해야 하는 상황에서 OS는 Shared Memory나, Message passing을 사용함.
- Shared Memory : 여러개의 프로세스가 메모리의 한 부분을 공유하는 것
- Message Passing : 프로세스 간의 정보 Packet을 주고 받는 것
-> Shared Memory보다 Message Passing 방식 속도가 더 느림

### Error detection (에러 탐지)

- CPU나 Memory와 같은 하드웨어, 입출력장치, 사용자 프로그램 등에서 일어나는 에러를 탐지하고, 바로 잡을 수 있어야 함.

## Resource allocation (자원 할당) 

- 여러 사용자나 여러 작업을 동시에 처리할 때, 컴퓨팅 자원이 잘 배분되도록 함.
- 다양한 종류의 자원을 관리할 수 있어야 함.

### Accounting (회계):

- 시스템은 어떤 유저가 어떤 종류의 자원을 얼만큼 사용하고 있는지 추적해야 함.
- 이 기록은 회계나 사용량 통계를 위해 사용될 수 있음

### Protection and Security (보호와 보안)

# system calls

- 커널과 사용자 프로그램을 이어주는 인터페이스 역할을 함.
- 사용자 프로그램이 디스크에 있는 파일 연다 = 파일 시스템에 접근한다.
- 시스템에 접근하려면 커널 모드로 전환되어야 함. -> 시스템 콜 사용해야 함

System call table (= Interrupt vector): 메모리의 특정 주소 범위에 어떤 동작들이 할당되어 있는 것

- system call에는 fork(), exit(), read(), write()와 같은 함수 존재
- But, 직접 조작하는 것 위험 => 표준 라이브러리 사용함
사용자 프로그램이 OS에게 매개변수를 넘기는 방법은 3가지 있음

1. Call-by-value : 매개변수의 값 자체를 복사하여 CPU 레지스터에 전달
2. Call-by-reference : 값의 메모리 주소를 전달 (많은 값을 전달할때 효율적)
3. 프로그램을 통해 Stack에 매개변수를 추가하고 운영체제를 통해 값을 뺌

# Types of System calls

- 프로세스 제어 : end, abort, load, execute
- 파일 관리 : create, delete open, close, read, write
- 장치 관리 : read, write, request, release
- 정보 유지 : get/set time or data
- 통신 : send/receive message, transfer status
- 보호

# Operating System Structure

현대 운영체제는 계층을 나눠서 시스템을 관리함

## simple structure
![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/d588112f-733d-43db-93a0-abfc45e2e236)

과거에는 사실상 계층이 구분되지 않았음. 

MS-DOS에서는 사용자 프로그램이 입출력 루틴에 접근해 디스플레이와 디스크 드라이브에 직접 쓰기를 할 수 있었음. 

따라서 만약 사용자 프로그램에 문제가 생기면 전체 시스템에 문제가 생김. 

-> UNIX 시스템은 이것을 개선함

전통적인 UNIX 시스템 구조는 MS-DOS에 비해 기능이 분리되었지만, 여전히 하나의 계층이 너무 많은 일을 함

하드웨어 계층 위, 사용자 계층 아래에 있는 커널이 모든 기능을 제공함

이러한 모놀리딕 (Monolithic) 구조는 구현과 유지보수가 쉽지 않음

## Layered Approach

![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/e7881142-06bf-4176-b3fa-17129714795d)

운영체제를 더 세분화해 계층을 분리한 것이 계층적 접근(Layered approach) 방식임

가장 아래에 있는 계층 (레이어 0)은 하드웨어, 가장 높은 계층 (레이어 N)은 사용자 인터페이스

이 방식은 유지보수가 아주 편함, 하나의 계층에만 신경쓰면 다른 계층에 아무런 신경을 쓰지 않아도 되기 때문

## Microkernels

마이크로커널 : 커널에서 핵심적인 요소만 남긴 가벼운 커널을 말함

커널이 커질수록 문제가 생길 가능성이 높아지고, 유지보수가 힘들어지기 때문에 커널을 가볍게 만들 필요가 있었음

- 코드 양이 훨씬 적어 컴파일, 테스트 시간이 비교적 짧고, 다른 시스템에 이식 (Porting)하기도 쉬움
- 시스템 프로그램을 추가해 기능을 늘리려하면 속도가 느려짐
- OS X의 커널(Darwin)의 일부가 마이크로커널 Match를 기반으로 만들어졌으며, IOT에도 마이크로커널이 사용됨

## Modules





## 출처 : 

https://parksb.github.io/article/6.html

https://www.scaler.com/topics/operating-system-structure/
