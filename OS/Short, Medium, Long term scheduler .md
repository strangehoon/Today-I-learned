### Short term scheduler (CPU scheduler)
Ready queue 안의 프로세스들의 순서를 정해주는 것을 CPU Scheduler라고 한다. CPU의 스위칭은 굉장히 빠르므로 CPU Scheduler는 short term Scheduler라고도 부른다.

</br>

### Medium term scheduler (Swap out)
OS의 역할 중 하나는 성능 향상이다. 만약 메인 메모리에 A라는 프로세스가 활동하지 않는다면 이 프로세스에 CPU time을 할애하는 건 비효율적이다. Medium term Scheduler는 주기적으로 메인 메모리에 있는 프로세스들을 검사하여 하드디스크로 옮길 프로세스를 찾아서 옮겨준다.

* swap out : 프로세스 관리부서에서는 PCB의 CPU time을 토대로 일정 시간 동안 활동하지 않는 프로세스를 찾아서 하드디스크로 내쫓는다.
* swap disk : 내쫓아진 프로세스가 위치하는 곳으로 하드디스크에 별도로 공간이 할당된다. backing store라고도 불린다.
* swap in : 내쫓아진 프로세스가 swap disk에 있다가 다시 작업을 해서 메인 메모리에 올라온다.
이러한 과정을 통칭해서 swapping이라고 한다. Process management는 비어있는 메모리에 다른 프로세스를 올리거나 A와 C에 더 할당하는 식으로 효율적으로 관리할 수 있다.

</br>

### Long term scheduler (Job scheduler)
Job queue 안의 프로세스들의 순서를 정해주는 것을 job Scheduler라고 한다. Job Scheduler는 long term Scheduler라고도 부른다. 메모리가 꽉 차있는 경우를 생각해 보자. Job Scheduler는 프로세스가 완전히 끝나고 메모리가 비워져야 일어나는데 이러한 일은 자주 일어나지 않고 대략 몇 분 간격으로 일어나기 때문이다. 또한 job Scheduler는 CPU/IO bound process 들을 적절히 섞어서 올리는 것이 중요하다.

* CPU bound process : 프로세스가 하는 일들이 주로 CPU를 사용하는 것, 대표적으로 일기예보.
* I/O bound process : 프로세스가 하는 일들이 주로 I/O 관련 작업, 대표적으로 word 같은 문서 편집.

</br>

<img src = "https://velog.velcdn.com/images/strangehoon/post/e07bcada-33a8-45ee-b21e-a8bd253ecbbb/image.png" height = "370px" width = "520px" allign = "left">

> job queue, ready queue, device queue 모두 OS의 Process management에 들어있다. 또한 queue 안에는 PCB 들이 줄을 서서 대기한다.
