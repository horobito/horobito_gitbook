# 14. 프로세스 스케쥴링 관련



## 01. 우선순위 기반 스케쥴러 <a id="01.-&#xC6B0;&#xC120;&#xC21C;&#xC704;-&#xAE30;&#xBC18;-&#xC2A4;&#xCF00;&#xC974;&#xB7EC;"></a>

### 1 . priority - Based 스케쥴러 - 여러 스케쥴링 알고리즘 중 1개  <a id="1-.-priority---Based-&#xC2A4;&#xCF00;&#xC974;&#xB7EC;---&#xC5EC;&#xB7EC;-&#xC2A4;&#xCF00;&#xC974;&#xB9C1;-&#xC54C;&#xACE0;&#xB9AC;&#xC998;-&#xC911;-1&#xAC1C;"></a>

* 정적 우선순위
  * 프로세스마다 우선순위 미리 지정   
* 동적 우선순위
  * 스케쥴러가 상황에 따라 우선순위를 동적으로 변경

cf\)

* 리눅스의 시스템 콜 규격 : POSIX
  * 즉, 리눅스는 POSIX 호환 운영체제
    * POSIX에서 정한 시스템콜을 다 제공한다는 의미

## 02. 우선순위 변경 시스템 콜  <a id="02.-&#xC6B0;&#xC120;&#xC21C;&#xC704;-&#xBCC0;&#xACBD;-&#xC2DC;&#xC2A4;&#xD15C;-&#xCF5C;"></a>

### 0. 알아야 할 점

* 프로세스 중 사실상 root가 소유한 프로세스만 우선순위를 높일 수 있다.
  * 다른 프로세스는 우선순위를 낮출 수만 있다.
  * 스케쥴링 방식에 따라 우선순위가 적용될 수도 있고, 안될 수도 있다.

### 1 . nice\(\)

* ```text
  #include <unistd.h>
  int nice (int inc);
  ```
* nice\(\) 안에 우선순위를 넣어주면, 해당 값으로 우선순위가 변경됨  

### 2. getpriority\(\), setpriority\(\)

* 알아야 할 것
  * which
    * 어떤 자원의 우선순위를 가져올것인지, set 할것인지
    * 프로세스\(PRIO\_PROCESS\), 프로세스 그룹\(PRIO\_PGRP\), 사용자\(PRIO\_USER\) 별로 우선 순위를 가져올 수 있다.   
  * who
    * 보통 프로세스 id
    * 0 이면 현재 프로세스 또는 프로세스 그룹  
  * value
    * 우선순위 값
* getpriority\(\)
  * ```text
    #include <sys/resource.h>
    int getpriority(int which, id_t who);
    ```
  * 현재 이 시스템콜을 수행하는 프로세스와 관련된 우선순위 값을 얻어내는 시스템 콜  
* setpriority\(\)
  * ```text
    #include <sys/resource.h>
    int setpriority(int which, id_t who, int value);
    ```
  * 현재 프로세스와 관련된 리소스에 대해서 우선순위 값을 매겨주는 시스템 콜
  * 
* 예시

  * ```text
    int main(){
       int which = PRIO_PROCESS; 
       id_t pid;
       int ret;  // 리턴값을 받을 수 있는 변수 
   
       pid = getpid(); // 프로세스 id 를 갖고올수 있는 함수 
       ret = getpriority(which, 0); // 현재 프로세스의 우선순위를 가져오는 것 
       // 출력 : 현재 프로세스의 id, 우선순위 
   
       ret = nice(10); // 우선순위 변경 
       ret = getpriority(which, 0); // 실제 변경이 되었는지 가져온다. 
       // 변경된 프로세스의 id, 우선순위  
   
       ret = setpriority(which, 0, 5); // 현재 프로세스의 우선순위를 5로, 
       ret = getpriority(which, 0); // 위와 같다. 
   
       return 0;

    }

    // 실행 결과
    PID=XXXXX, PRIORITY=0;
    PID=XXXXX, PRIORITY=10;
    PID=XXXXX, PRIORITY=5;
    ```

