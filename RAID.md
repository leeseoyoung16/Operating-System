# RAID ( Redundant Array of Independent (Inexpensive) Disk）

- 여러 개의 하드 디스크에 일부 중복된 데이터를 나눠서 저장하는 기술

 -> 작은 용량의 저장장치를 여러 대로 묶어 대용량 저장장치를 만들어 사용하는 기술

목적
- 여러 개의 디스크 모듈을 하나의 대용량 디스크처럼 사용할 수 있도록 함
- 여러 개의 디스크 모듈에 데이터를 나눠서 한 번에 쓰고 한 번에 읽는 방식으로 입출력 속도를 높임
- 여러 개의 디스크를 모아서 하나의 디스크로 만들고 하나 혹은 그 이상의 디스크에 장애가 나더라도 최소한 데이터가 사라지는 것을 방지함.

RAID를 구성하는 디스크 개수가 같아도 RAID의 구성 방식에 따라 성능, 용량이 바뀜 -> 이 구성 방식을 ‘RAID Level’

Standard RAID level -> RAID 0 ~ RAID 6

최근 출시되는 RAID 컨트롤러에서 사용 가능 한 Level은 RAID 0, RAID1, RAID5, RAID 6

## RAID 0 ( striping )

- 최소 2개의 디스크 필요
- 모든 디스크에 데이터 분할 저장
- 용량 및 성능이 단일 디스크 대비 N배
- 하나의 디스크라도 문제가 발생할 경우, 전체 RAID가 
 깨지는 일 발생 
   => 안정성 1/N

  ![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/09a5c8c3-6040-4f5a-a9f5-59f6635aff08)

## RAID 1 ( Mirroring )

- 최소 2개의 디스크 필요
- 모든 디스크에 데이터 복제하여 기록 
  => 동일한 데이터를 N개로 복제하여 각 디스크에 저장하는 방식
- 여러 개의 디스크로 구성해도 실제 사용 가능 용량은 
 단일 디스크 용량과 동일
-> 높은 신뢰도를 요구하는 결함 허용 시스템에 주로 사용
- 안정성이 높지만, 비용 문제로 인해 거의 사용하지 않음

![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/e468a97e-7572-424f-8ad6-28b63a9f6ed5)

## RAID 4 

- 최소 3개의 디스크 필요
- block 단위로 striping
- error correction을 위해 패리티 디스크를 1개 사용
- 용량 및 성능이 단일 디스크 대비 N-1배 증가
- 1개의 디스크 에러 시 복구 가능
- 2개 이상의 디스크 에러 시 복구 불가능

![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/ed7f2d4b-f263-4ca3-be5c-dadd220d05fa)

## RAID 5

- 최소 3개의 디스크 필요
- block 단위로 striping
- error correction을 위해 패리티를 1개의 디스크에 저장
단, 패리티 저장은 고정된 디스크 X, 매번 다른 디스크 저장
- 용량 및 성능이 단일 디스크 대비 N-1배 증가

![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/ced4e5c3-eb4d-4635-b4d3-eccc825640e1)

## RAID 6

- 최소 4개의 디스크 필요
- block 단위로 striping
- error correction을 위해 패리티를 2개의 디스크에 저장
단, 패리티 저장은 고정된 디스크 X, 매번 다른 디스크 저장
- 용량 및 성능이 단일 디스크 대비 N-2배 증가
- RAID 5에서 성능과 용량을 조금 줄이는 대신 안정성 높인 방식

![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/0f5dc9a8-70c7-4dbf-9ad5-fa3a7c1302b9)

## Nested RAID ( 중첩 RAID )
-> Standard RAID를 여러 개 중첩하여 사용

ex. RAID 0+1
- RAID 0을 RAID 1으로 묶는 방식

![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/54e61cda-efac-4d27-9668-b64d769d8ab2)


ex. RAID 1+0
- RAID 1을 RAID 0으로 묶는 방식

![image](https://github.com/leeseoyoung16/Operating-System/assets/101916673/aeb606e7-f72d-4a5d-be18-746d1f678184)

## 출처

https://velog.io/@zxcvbnm5288/RAID-%EB%9E%80-RAID-%EA%B5%AC%EC%84%B1%EB%B0%A9%EC%8B%9DRAID-0-1-4-5-6-10-01

https://en.wikipedia.org/wiki/Standard_RAID_levels

https://devocean.sk.com/blog/techBoardDetail.do?ID=163608

https://sunrise-min.tistory.com/entry/RAID%EB%A0%88%EC%9D%B4%EB%93%9C-%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-RAID-015610
