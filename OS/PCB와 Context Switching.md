# PCB와 Context Switching

**PCB는 프로세스에 대한 모든 정보가 모여있는 곳으로** Task Control Block(TCB)이라고도 한다. 각각의 프로세스마다 PCB가 따로 존재한다. PCB 들은 OS의 Process management가 관리한다. PCB에 들어있는 정보는 다음과 같다.
* process state : 현재 프로세스의 state.
* PC : 프로세스가 다음에 실행할 명령어의 주소.
* MMU info : base와 limit 값.
* CPU time : 현재 프로세스의 CPU 사용량.
* process id : 프로세스마다 번호를 붙임. 주민번호나 학번 개념과 유사.
* list of open files : 하드디스크의 어떤 파일들을 사용하는지

<img src = "https://velog.velcdn.com/images/strangehoon/post/95ef9592-585e-41f8-8de7-34c2dc7b0f86/image.png" height = "500px" width = "450px">

Context switching은 CPU가 한 프로세스에서 다른 프로세스로 옮겨가는 것을 말한다. 예를 들어 프로세스 A가 running 상태, B가 ready 상태라 가정하자.

1. 스케줄러가 A 프로세스의 실행을 중단하고 B 프로세스를 실행하도록 요청한다.
2. A 프로세스에서 SP(Stack Pointer)의 값과 PC(Program Counter)의 값을 PCB에 저장한다.
3. A 프로세스는 ready or block 상태로 바뀌고 B 프로세스의 상태가 ready에서 running 상태로 바뀐다. 이처럼 현재 CPU 데이터는 이전 프로세스의 PCB에 갱신하고, 새로 시작되는 프로세스의 PCB 데이터를 CPU로 복원해주는 작업을 dispatcher라고 한다.
4. 반대로 B 프로세스에서 A 프로세스로 컨텍스트 스위칭할 경우, B 프로세스의 SP 값과 PC 값을 PCB에 저장하고 A 프로세스의 PCB에서 SP 값과 PC 값을 찾아 덮어씌운다. 

