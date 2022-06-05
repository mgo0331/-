# 리눅스 명령어 : top, ps, jobs, kill 명령어 조사하기
갱갱
20223181 문경원 (03분반)
***
# 1. top

+ 시스템의 상태를 전반적으로 가장 빠르게 파악 가능(CPU, Memory, Process)

+ 옵션 없이 입력하면 interval 간격(기본 3초)으로 화면을 갱신하며 정보를 보여줌 

+ top 실행 전 옵션

 ->순간의 정보를 확인하려면 -b 옵션 추가(batch 모드)
 
 ->-n : top 실행 주기 설정(반복 횟수)

+ top 실행 후 명령어

 ->shift + p : CPU 사용률 내림차순
 
 ->shit + m : 메모리 사용률 내림차순
 
 ->shift + t : 프로세스가 돌아가고 있는 시간 순
 
 ->k : kill. k 입력 후 PID 번호 작성. signal은 9
 
 ->f : sort field 선택 화면 -> q 누르면 RES순으로 정렬
 
 ->a : 메모리 사용량에 따라 정렬
 
 ->b : Batch 모드로 작동
 
 ->1 : CPU Core별로 사용량 보여줌
 
 + ps와 top의 차이점

 ->ps는 ps한 시점에 proc에서 검색한 cpu 사용량
 
 ->top은 proc에서 일정 주기로 합산해 cpu 사용율 출력
 
 + top -b -n 1
 <img width="670" alt="스크린샷 2018-07-18 20 25 32" src="https://user-images.githubusercontent.com/106901452/172040739-f266df64-4723-4ab7-9506-bce58dc59193.png">
 
 ->3:58 : 3시간 58분 전에 서버가 구동
 
 ->load average : 현재 시스템이 얼마나 일을 하는지를 나타냄. 3개의 숫자는 1분, 5분, 15분 간의 평균 실행/대기 중인 프로세스의 수. CPU 코어수 보다 적으면 문제 없음
 
 ->Tasks : 프로세스 개수
 
 ->KiB Mem, Swap : 각 메모리의 사용량
 
 ->PR : 실행 우선순위
 
 ->VIRT, RES, SHR : 메모리 사용량 => 누수 check 가능
 
 ->S : 프로세스 상태(작업중, I/O 대기, 유휴 상태 등)
 
 [1번 출처](https://zzsza.github.io/development/2018/07/18/linux-top/)
 
 ***
 
 # 2. ps
 ->현재 실행중인 프로세스의 목록을 보는 명령어이다 
 
 |명령어|설명|
 |:-----:|:----:|
 |-e|실행중인 모든 프로세스의 정보를 출력한다|
 |-f|프로세스에 대한 자세한 정보를 출력한다|
 |-u[사용자이름]|특정 사용자에 대한 모든 프로세스의 정보를 출력|
 |-p pid|pid로 지정한 프로세스의 정보를 출력|
 |u|프로세스의 소유자 이름, CPU 사용량, 메모리 사용량 등 상세 정보를 출력|
 |a|터미널에서 실행한 프로세스의 정보를 출력|
 |x|실행 중인 모든 프로세스의 정보를 출력|

[2번 출처](https://blog.naver.com/PostView.nhn?isHttpsRedirect=true&blogId=jsky10503&logNo=220728880785&parentCategoryNo=&categoryNo=109&viewDate=&isShowPopularPosts=false&from=postView)

***

# 3. jobs
->작업의 상태를 표시하는 명령어이다. 현재 쉘 세션에서 실행시킨 백그라운드 작업의 목록이 출력되며, 각 작업에는 번호가 붙어 있어 kill 뒤에'%번호' 등으로 사용할 수 있다.

|상태|설명|
|:---:|:---:|
|Running|작업이 계속 진행중임|
|Done|작업이 완료되어 0을 반환|
|Done(code)|작업이 종료되었으므로 0이 아닌 코드 반환|
|Stopped|작업이 일시 중단|
|Stopped(SIGTSTP)|SLGTSTP이 작업을 일시 중단|
|Stopped(SIGTSOP)|SLGTSOP이 작업을 일시 중단|
|Stopped(SIGTTIN)|SLGTTIN이 작업을 일시 중단|
|Stopped(SIGTTOU)|SLGTTON이 작업을 일시 중단| 

|옵션|설명|
|:---:|:---:|
|-l|프로세스 그룹 ID를 state필드 앞에 출력|
|-n|프로세스 그룹 중에 대표 프로세스 ID를 출력|
|-p|각 프로세스 ID에 대해 한 행씩 출력|
|command|지정한 명령어를 실행|

[3번 출처](https://hbase.tistory.com/265)

***

# 4. kill
-> 프로세스에 시그널을 보내는 명령어이다.

1)kill 시그널 리스트 확인

$ kill -l
 1) SIGHUP	 2) SIGINT	 3) SIGQUIT	 4) SIGILL	 5) SIGTRAP
 6) SIGABRT	 7) SIGBUS	 8) SIGFPE	 9) SIGKILL	10) SIGUSR1
11) SIGSEGV	12) SIGUSR2	13) SIGPIPE	14) SIGALRM	15) SIGTERM
16) SIGSTKFLT	17) SIGCHLD	18) SIGCONT	19) SIGSTOP	20) SIGTSTP
21) SIGTTIN	22) SIGTTOU	23) SIGURG	24) SIGXCPU	25) SIGXFSZ
26) SIGVTALRM	27) SIGPROF	28) SIGWINCH	29) SIGIO	30) SIGPWR
31) SIGSYS	34) SIGRTMIN	35) SIGRTMIN+1	36) SIGRTMIN+2	37) SIGRTMIN+3
38) SIGRTMIN+4	39) SIGRTMIN+5	40) SIGRTMIN+6	41) SIGRTMIN+7	42) SIGRTMIN+8
43) SIGRTMIN+9	44) SIGRTMIN+10	45) SIGRTMIN+11	46) SIGRTMIN+12	47) SIGRTMIN+13
48) SIGRTMIN+14	49) SIGRTMIN+15	50) SIGRTMAX-14	51) SIGRTMAX-13	52) SIGRTMAX-12
53) SIGRTMAX-11	54) SIGRTMAX-10	55) SIGRTMAX-9	56) SIGRTMAX-8	57) SIGRTMAX-7
58) SIGRTMAX-6	59) SIGRTMAX-5	60) SIGRTMAX-4	61) SIGRTMAX-3	62) SIGRTMAX-2
63) SIGRTMAX-1	64) SIGRTMAX

2)주요 시그널

|시그널|영어|설명|
|:---:|:---:|:---:|
|1)SIGHUP|Hang Up|세션이 종료될 때 시스템이 내리는 시그널|
|2)SIGINT|Interrupt|Ctrl + C, 종료 요청 시그널|
|9) SIGKILL|Kill|강제 종료 시그널|
|11) SIGSEGV|Segment Violation|메모리 침범이 일어날 때 시스템이 보내는 시그널|
|15) SIGTERM|Terminate|기본 값, 종료 요청 시그널|
|20) SIGTSTP|Temporary Stop|Ctrl + Z 일시 중지 요청 시그널|

3)프로세스에 시그널 보내기

```c
$ kill [option] PID

# 1234(PID) 프로세스 종료 
$ kill -9 1234
$ kill -SIGKILL 1234
```

[4번 출력](https://frogand.tistory.com/69)

***

# vim에디터 매크로 사용법

1)q + a       a키에 recording 시작

2)반복을 위한 내가 원하는 동작

3)q             recoding 종료

4)@a          1회 실행 

or @@         방금 실행한 매크로 실행

or 10@a       매크로 10회 실행

+ 숫자 증가 방법

1)1 숫자 입력

2)매크로 시작

3)1 숫자를 복사해서 다음줄에 붙여넣기

4)두번째줄 1에 커서를 올리고 Ctrl+a(숫자 증가)

5)매크로 종료

[vim에디터 출처](http://aboutmadlife.blogspot.com/2014/09/linux-vi-macro.html)
