static inline

task_t * context_switch(runqueue_t *rq, task_t *prev, task_t *next){ //runqueue_t 

    struct mm_struct *mm = next->mm; // 다음 실행 중인 ‘next’의 가상 메모리 주소 공간 ‘mm’을 가져옴
    
    struct mm_struct *oldmm = prev->active_mm; //이전 실행 중인 프로세스 ‘prev’의 가상 메모리 주소 공간 정보 ‘active_mm’을 가져옴
    
    if (unlikely(!mm)){ // mm이 NULL이라면 
    
        next->active_mm = oldmm; // 새로운 프로세스 ‘active_mm’을 현재 가상 메모리 주소 공간 정보 ‘oldmm’으로 지정
        
        atomic_inc(&oldmm->mm_count); // oldmm의 mm_count을 원자적으로 1 증가시키는 작업 (원자적 : 여러 프로세스가 동시에 이 코드를 실행하더라도 올바른 결과 보장) 
        
        enter_lazy_tib(oldmm, next); // TLB (Translation Lookaside Buffer)에 있는 페이지 테이블 엔트리를 지우고 새로운 페이지 테이블 엔트리를 적재하기 위한 함수

TLB는 가상 주소를 실제 물리 주소로 변환하는 데 사용되는 캐시.

페이지 테이블이 변경되면 TLB의 모든 엔트리 지우고 새로운 페이지 테이블 엔드리를 TLB에 적재해야 함(TLB flush).

하지만, TLB flush는 비용이 큰 작업으로 대부분의 경우 즉시 변경하지 않고 적재하지 않은 상태로 유지하는 걸 lazy TLB flush라고 함.


    }else // mm이 NULL이 아니라면
    
        switch_mm(oldmm, mm, next); // 이전 주소 공간 ‘oldmm’과 새로운 주소 공간‘mm’으로 전환하는 작업
        
    if(unlikely(!prev->mm)){ //이전 실행 중인 프로세스 ‘prev’의 가상 메모리 주소정보 ‘mm’이 NULL이라면
    
            prev->active_mm = NULL: // 이전 실행 중인 프로세스의 ‘active_mm’를 NULL로 설정
            
            WARN_ON(rq->prev_mm); //위 줄 값이 NULL이 아닌 경우 경고 생성 (주로 디버깅 및 코드 품질 검사를 위해 사용)
            
            rq->prev_mm = oldmm; // 실행 큐 ‘rq’의 ‘prev_mm’을 ‘oldmm’로 설정
    }
    
    switch_to(prev,next, prev); // 이전 실행 중인 프로세스‘prev’와 새로 실행 중인 ‘next’의 레지스터 상태와 스택을 전환
    
    return prev; //이전 실행 중인 ‘prev’ 반환
    
}

요약 : context switching 수행하는 함수, 이전 실행 중인 프로세스(prev)와 새로 실행 중인 프로세스(next) 전환하기 위한 작업 수행

runqueue_t : 커널에서 프로세스를 관리하는데 사용하는 자료구조. 리눅스 커널 프로세스 스케줄링 정보 저장하는 자료구조

struct mm_struct : 리눅스 커널에서 프로세스가 사용하는 가상 메모리 주소 공간 정보를 저장하기 위한 자료구조

task_t : 리눅스 커널에서 프로세스를 나타내는 구조체. 현재 실행 중인 프로세스나 스레드에 대한 정보 저장하고 관리.
