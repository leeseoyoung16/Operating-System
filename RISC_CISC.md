# CISC vs RISC 💻

CPU의 명령어 집합 아키텍처 설계, 프로세스의 ISA(Instruction Set Architecture)

초기 컴퓨터는 CISC 사용, 명령어 중 20%가 대부분의 기능 수행되어, 1980년대 복잡성을 줄이기 위해 RISC 고안하였다.

## CISC (Complex Instruction Set Computer)

1) Hardware에서 처리 (Memory to Memory)
2) 멀티 클럭 동작
3) 코드 용량 적음
4) 명령어 집합 많음 -> 명령어 해석 시간 오래 걸림 , 명령어 해석 회로 복잡
5) 명령어 길이 가변적 -> 병렬 처리 어려움 (파이프라이닝 어려움)
6) 컴파일러 구조 단순
7) 프로그램을 이루는 명령어 수가 적음
8) 처리 속도 느림
9) 전력 소모 큼
10) 가격 비쌈
11) 호환성이 절대적으로 필요한 PC용 CPU

## RISC (Reduce Instruction Set Computer)

1) Software에서 처리 (Register to Register)
2) 싱글 클럭 동작
3) 코드 용량 큼
4) 명령어 집합 적음 -> 명령어 회로 단순 
5) 명령어 길이 고정적 -> 병렬 처리 가능 (파이프라이닝 쉬움)
6) 컴파일러 구조 복잡　
7) 프로그램을 이루는 명령어 수가 많음
8) 처리 속도 빠름
9) 전력 소모 적음
10) 가격 저렴함
11) IBM System/6000, 임베디드(MIPS, ARM계열 등), 매킨토시, 서버, 워크스테이션 등을 위한 특수목적 CPU


# ARM vs x86 
## x86
- Intel 기반 CPU
 -> 완전한 제품 판매

- CISC 구조 사용
 -> 명령어 길이가 길고 디코딩하는 데 시간이 오래 걸림

- 발열이 심하지만, RAM 용량이 적게 필요
 -> 성능을 위한 설계
 -> 대용량 캐시 탑재

- 호환성이 높음

- 높은 전력을 사용하며, 명령어 처리 속도 느림

-  대부분의 데스크톱 응용 프로그램뿐 아니라 Windows, Linux를 포함한 다양한 소프트웨어와 호환, 데스크톱, 노트북, 워크스테이션을 포함한 대부분의 개인용 컴퓨터에 사용

## ARM(Advanced RISC Machine)
- arm 기반 CPU
 -> 라이센스를 판매 (목적에 맞게 최적화 가능)

- RISC 구조 사용
 -> 명령어 길이가 짧고 디코딩하는 데 빠름

- 발열이 적지만, RAM 용량이 많이 필요
 -> 낮은 전력 소비를 위한 설계 => 모바일 장치에 적합
 -> 작은 캐시 탑재

- 호환성이 낮음, x86 프로그램을 사용하려면 에뮬레이션이 필요함.
  => 프로그램 실행 속도가 느려지고, 하드웨어 리소스를 많이 사용

- 작은 전력을 사용하며, 명령어 처리 속도 빠르고 효율적

- 주로 스마트폰과 태블릿과 같은 모바일 장치에 사용

각각 x86과 ARM은 다른 용도를 위해 설계되었기 때문에, 어느 것이 더 우월한 아키텍처인지 일반적으로 판단하기는 어렵다. 또한, 최근에는 RISC와 CISC 아키텍처의 구분이 점차 희미해지고 있다. 이로 인해 ARM 아키텍처도 일부 CISC 특성을 가지고 있을 수 있으며, 반대로 x86 아키텍처도 RISC의 일부 특성을 적용하기도 한다.







### 출처 : 
https://153net.tistory.com/83

https://cs.stanford.edu/people/eroberts/courses/soco/projects/risc/risccisc/

https://onpups.pe.kr/247

https://dany-it.tistory.com/41

http://www.jidum.com/jidums/view.do?jidumId=401

https://code-piggy.tistory.com/entry/%EC%BB%B4%ED%93%A8%ED%84%B0-%EA%B5%AC%EC%A1%B0-ISA-CISC-RISC

https://cs.stanford.edu/people/eroberts/courses/soco/projects/risc/risccisc/

https://imdeveloper-92.tistory.com/42

https://www.youtube.com/watch?v=G-fJJ-OHLDw

https://yunamom.tistory.com/170
