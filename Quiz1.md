# OS 퀴즈 대비💎

## POSIX의 약자
- Portable operating system interface
- 이식 가능 운영체제 인터페이스

## POSIX와 JVM의 차이
- POSIX는 어떤 OS에서 컴파일해도 가능 (소스 코드 레벨에서 이식성을 가짐)
- JVM은 컴파일된 이미지에서 이식성을 가짐

## OS에 매개변수를 전달하는 3가지 방법
1. 매개변수를  레지스터 내에 전달 (call-by-value)
2. 매개변수를 메모리 내의 블록에 저장하고, 블록의 주소를 전달 (call-by-reference)
3. 매개변수를 스택에 넣고, 운영체제로 꺼냄

## Microkernel

- 대부분의 내용이 Kernel에 없고 유저레벨에 있음
- 확장성이 좋음
- 커널코드가 적어 시스템이 안정적

## Monolithickernel

- kernel 안에 모든 내용이 있음
- 모든 내용이 function call로 이루어짐
- OS에 문제가 생길 가능성 높음
- 성능은 더 좋음
