## IPC ( = Inter Process Communication ) :
프로세스 간에 데이터를 주고받는 메커니즘을 제공하는 기술

### 1. PIPE
: 익명의 PIPE를 통해 동일한 PPID를 가진 프로세스 간에 단방향 통신 지원
구조

- FIFO 구조
- 생성된 PIPE에 대해 Write, Read만 가능
  
사용 시기
- 부모 자식 or 형제 프로세스 간 통신에 이용
- 외부 프로세스에서 사용 불가
  
유의 사항
- 쌍방 통신을 위해 Write 용 PIPE 1개와 Read PIPE 1개씩 만들어야 함.
- Read와 Write가 기본적으로 block 모드로 작동하기 때문에 프로세스가 read 대기
중이라면 read가 끝나기 전에는 write 할 수 없음.

<img width="258" alt="image" src="https://github.com/leeseoyoung16/Operating-System/assets/101916673/2e3b61af-851f-4bf9-a2d7-fea1c9d0f06b">

### 2. Named PIPE
: 이름을 가진 PIPE를 통해서 프로세스 간에 양방향 통신을 지원 ( 보통 단방향 사용 )
구조

- FIFO 구조
- 생성된 PIPE에 대해 Write 또는 Read만 가능
  
사용 시기
- 연관이 전혀 없는 프로세스 간 통신에 이용
  
유의 사항
- 쌍방 통신을 위해 Write 용 PIPE 1개와 Read PIPE 1개씩 만들어야 함.
- Read와 Write가 기본적으로 block 모드로 작동하기 때문에 프로세스가 read 대기
중이라면 read가 끝나기 전에는 write 할 수 없음.

<img width="255" alt="image" src="https://github.com/leeseoyoung16/Operating-System/assets/101916673/a4e416e4-e873-4848-b492-17ced1c26541">

### 3. Message Queue
: 메모리를 사용한 PIPE, 구조체 기반으로 통신함.
구조

- FIFO 구조
- msgtype에 따라 다른 구조체를 가져올 수 있음.
  
사용 시기
- 프로세스 간 다양한 통신을 할 때 사용할 수 있음.
  
유의 사항
- 커널에서 제공하는 Message queue이기 때문에 EnQueue하는데 제한 존재.
- Message 접근을 위해 key가 필요

<img width="245" alt="image" src="https://github.com/leeseoyoung16/Operating-System/assets/101916673/f8131a1b-44ae-412c-86d8-16c384b750ab">

### 4. Shared Memory
: 시스템 상의 공유 메모리를 통해 통신함.

구조
- 일정한 크기의 메모리를 프로세스 간에 공유하는 구조
- 공유 메모리는 커널에서 관리함.
  
사용 시기
- 프로세스 간 Read, Write를 모두 필요로 할 때 사용할 수 있음.
  
유의 사항
- 메모리 크기가 동일해야 함.

<img width="194" alt="image" src="https://github.com/leeseoyoung16/Operating-System/assets/101916673/36714109-6010-480a-9a85-ce75adaf7823">

### 5. Memory Map
: 열린 파일을 메모리에 매핑하여 파일의 내용을 메모리에 직접 로드함.
구조

- 열린 파일을 프로세스의 가상 주소 공간에 매핑함. 이렇게 매핑된 파일은 메모리에 존재하
는 것처럼 프로세스에 의해 접근 가능

사용 시기
- 대용량 데이터를 공유할 때 사용함.
- FILE I/O가 느릴 때 사용하면 좋음.
  
유의 사항
- Write 시기는 프로세스의 메모리에서 내려갈 때만 Write 됨.
  
=> 메모리와 File Sync가 안 맞을 수도 있음
- 메모리 맵 파일을 사용하기 이전, 이후에만 파일의 크기를 바꿀 수 있음

<img width="212" alt="image" src="https://github.com/leeseoyoung16/Operating-System/assets/101916673/b74f329e-ac76-4f7c-979c-64f556c9181d">

### 6. Socket
: 네트워크 소켓 통신을 사용한 데이터 공유

구조
- 네트워크 소켓을 이용하여 Client-Sever 구조로 데이터 통신
  
사용 시기
- 원격에서 프로세스 간 데이터를 공유할 때 사용
- 중대형 애플리케이션에서 주로 사용함.
  
유의 사항
- 네트워크 프로그래밍이 가능해야 함.
- 데이터 세그먼트 처리를 잘해야 함

<img width="316" alt="image" src="https://github.com/leeseoyoung16/Operating-System/assets/101916673/8680fc10-1746-4bcd-ab59-cc26a90099b2">


## 총정리

<img width="326" alt="image" src="https://github.com/leeseoyoung16/Operating-System/assets/101916673/776a477c-1a70-4d60-a77d-a774d2d480e3">
