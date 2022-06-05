# 오픈소스 SW개론 2차 과제

###### 20223132 컴퓨터공학과 김도연

## 1. 리눅스 명령어 (top, ps, jobs, kill)

### (1) top(table of processes)

top 명령어는 CPU 사용량, 메모리 사용량 등에 관한 정보를 실시간으로 출력하는 명령어이다.

<img src="https://user-images.githubusercontent.com/106876869/172039960-567cd24d-2329-4bfe-9ced-9c7371beac51.PNG" width ="70%" height="70%"/> *(top 명령어 실행 시 화면)*

+ 16:09:44 : 현재 서버의 시간

+ 5:28 : 켜져 있는 시간

+ 0 users : 사용자

+ load average : 현재 시스템이 얼마나 일을 하고 있는지 1분, 5분, 15분 단위로 실행 / 대기 중인 프로세스 수를 나타내고 있다.

+ Tasks : 프로세스 수

위쪽 화면은 현재 시스템의 상태를 보여준다. 시스템 시간 등을 전체적으로 확인할 수 있으면 아래쪽 화면은 현재 실행하고 있는 프로세스 현황을 볼 수 있다.


___프로세스 상태 정보___

|용어|설명|
|---|---|
|PID|프로세스 ID|
|USER|프로세스를 실행시킨 사용자 ID|
|PRI|프로세스의 우선순위|
|NI|NICE 값|
|RES|현재 페이지가 상주하고 있는 크기|
|SHR|분할된 페이지, 프로세스에 의해 사용된 메모리를 나눈 메모리의 총합|
|S|프로세스의 상태{S:sleeping, R:running, W:swapped out process, Z:zombies}|
|%CPU|프로세스가 사용하는 CPU의 사용율|
|%MEM|프로세스가 사용하는 메모리의 사용율|
|COMMAND|실행된 명령어|

___top 명령어 옵션___

|명령어|설명|
|---|---|
|shift+p|CPU사용률이 높은 프로세스 순서대로 표시|
|shift+m|메모리 사용률이 높은 프로세스 순서대로 표시|
|shift+t|프로세스가 돌아가고 있는 시간 순서대로 표시|
|a|메모리 사요량에 따라 정렬|
|b|Batch 모드 작동|
|c|명령행/프로그램 이름 토글|
|d|지연 시간 간격은 다음과 같음 -d ss. tt(seconds.tenths)|
|h|도움말|
|M|메모리 유닛 탐지|
|n|반복 횟수 제한|
|s|보안 모드 작동|
|S|누적 시간 모드 토글|
|u|사용자별 모니터링|
|1|CPU Core별로 사용량 보여줌|


### (2) ps(process status)

ps 명령어는 현재 실행중인 프로세스 목록과 상태를 출력하여 보여주는 기능을 한다. (≒ 윈도우의 작업관리자) ps의 옵션은 전통적인 유닉스의 System V, BSD, GNU에 따라 결과가 다르게 나타나고 표기법에도 차이를 보인다.

<img src="https://user-images.githubusercontent.com/106876869/172040383-be99c2d0-e45e-4444-9a8a-406192b816f1.PNG" width ="100%" height="100%"/> *ps 명령어 실행 결과*

***ps 옵션 사용***
+ ps -ef : 모든 프로세스를 풀 포맷으로 출력
+ ps aux : 실행 중인 모든 프로세스 확인
+ ps auxf : 실행 중인 프로세스를 트리구조로 출력
+ ps auxfww : 실행 중인 프로세스를 트리구조 + 모든 실행 중인 옵션 확인 가능
+ ps -el : 긴 포맷으로 출력하여 보고 싶은 경우

***ps 주요 옵션***

|옵션|설명|
|---|---|
|A|모든 프로세스를 출력|
|a|터미널에 종속되지 않은 모든 프로세스를 출력|
|e|커널 프로세스를 제외한 모든 프로세스를 출력|
|f|full 포맷 출력|
|l|긴 포맷으로 출력|
|M|64비트 프로세스 출력|
|m|프로세스들 뿐만 아니라 커널 스레드들 출력|
|p|특정 PID를 지정할 때 사용|
|r|현재 실행 중인 프로세서를 출력|
|u|프로세스의 소유자를 기준으로 출력|
|x|특정 사용자의 프로세스 정보를 확인|


### (3) jobs 

jobs 명령어는 작업이 중지된 상태, 백그라운드로 진행 중인 작업상태, 변경되었지만 보고되지 않은 상태 등을 표시하는 명령어이다.

***옵션***
+ -l : 프로세스 그룹 ID를 state 필드 앞에 출력
+ -n : 프로세스 그룹 중에 대표 프로세스 ID를 출력
+ -p : 각 프로세스 ID에 대해 한 행씩 출력
+ command : 지정한 명령어를 실행

___jobs로 알 수 있는 상태 값___
|상태|설명|
|---|---|
|Running|작업이 일시 중단되지 않았고 종료하지 않고 계속 진행 중|
|Done|작업이 완료되어 0을 반환하고 종료 했음|
|Done(code)|작업이 정상적으로 완료되었으며, 0이 아닌 코드를 반환 했음|
|Stopped|작업이 일시 중단|
|Stopped(SIGTSTP)|SIGTSTP 신호가 작업을 일시 중단|
|Stopped(SIGSTOP)|SIGSTOP 신호가 작업을 일시 중단|
|Stopped(SIGTTIN)|SIGTTIN 신호가 작업을 일시 중단|
|Stopped(SIGTTOU)|SIGTTOU 신호가 작업을 일시 중단|


### (4) kill

kill 명령어는 대부분 프로세스를 종료시킬때 사용하는 명령어이다.

+ 시그널은 지정하지 않을 경우 기본 값인 정상 종료(15, SIGTERM) 시그널을 보낸다.

*kill [pid]*

+시그널 지정

*kill -s [signal id][pid]*

*kill -s [signal text][pid]*

*kill -[signal id][pid]*

*kill -[signal text][pid]*


<img src="https://user-images.githubusercontent.com/106876869/172040485-07c37061-72e3-4412-9818-02f5966cd43c.PNG" width ="70%" height="70%"/> *시그널 종류*

+kill -l 명령어를 이용해 사용할 수 있는 시그널 확인할 수 있음

***KILL 옵션***

+ SIGHUP : hang up의 약자로 프로세스를 재시작시키는 시그널
+ SIGINT : 인터럽트. 실행을 중지시킨다.
+ SIGQUIT : 키보드 종료
+ SIGKILL : 무조건 종료, 강제 종료
+ SIGTERM : Terminate의 약자로 가능한 정상 종료시키는 시그널
+ CONT : Continue. STOP등에 의해 정지된 프로세스를 다시 실행
+ STOP : 무조건적, 즉각적 정지
+ TSTP : 실행 정지후 다시 실행을 계속하기 위해 대기시키는 시그널

***KILL 사용법***

```vim
// 시그널을 생략할 경우 기본 시그널 값인 SIGTERM(15)로 적용
# kill 1
# kill -s 15 1

//SIGTERN
# kill -s SIGTERM 1

//SIG를 빼고 입력 가능

//-s 옵션을 빼고 -시그널번호, -시그널 형태로 사용할 수도 있음
# kil -12 1
# kill SIGTERM 1
# kill -TERM 1
```

## 2. vim 에디터에서의 매크로 사용법

***매크로(Macro)*** 란 쉽게 말해 같은 동작을 반복하게 해주는 것이라고 할 수 있다.

이 매크로를 사용하여 각 글자의 끝에 (( )) 를 붙이는 작업을 해보았다.

<img src="https://user-images.githubusercontent.com/106876869/172041002-31b931db-d84e-45af-8b7f-f5657ebb180a.PNG" width ="60%" height="60%"/>

매크로를 실행하기 위해 **q**를 입력하고 매크로의 이름을 입력한다. 여기선 a라고 입력하였다.

<img src="https://user-images.githubusercontent.com/106876869/172041008-1260cbce-fdd7-44a8-9929-f786c6efcd36.PNG" width ="60%" height="60%"/>

그리고 문장의 마지막 글자인 d로 이동하여 (( ))를 붙여 준다. 그리고 다시 **q**를 눌러 매크로를 종료시킨다. 

<img src="https://user-images.githubusercontent.com/106876869/172043849-df9d0762-0d58-45d6-a66a-8101ca2f2ab1.PNG" width ="60%" height="60%"/>

다음 매크로를 실행시키기 위해 @a를 입력하면 각 글자가 다음 사진과 같이 변한다. 이와 같이 매크로를 사용할 수 있다. 정리해보자면 다음과 같다.

___매크로 사용법___
1) 매크로 시작 = q[name]
2) 매크로 입력
3) 매크로 종료 = q
4) 매크로 실행 = @[name]
5) 매크로 여러번 실행 = [number]@[name]

***:u = 작업 되돌리기***















