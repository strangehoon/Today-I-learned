# Blocking vs Non-Blocking & Synchronous vs Asynchronous

**Blocking** : 자신의 작업을 진행하다가 다른 주체의 작업이 시작되면 다른 작업이 끝날 때까지 기다렸다가 자신의 작업을 시작하는 것 </br>

**Non-Blocking** : 다른 주체의 작업에 관련없이 자신의 작업을 하는 것

> Blocking/Non-Blocking은 현재 작업이 block 되느냐 아니냐에 따른 **제어의 관점**

</br>

**Synchronous** : 작업을 동시에 수행하거나, 동시에 끝나거나, 끝나는 동시에 시작함을 의미 </br>

**Asynchronous** : 시작, 종료가 일치하지 않으며, 끝나는 동시에 시작 하지 않음을 의미

> Synchronous/Asynchronous는 요청한 작업에 대해 완료 여부를 신경 써서 작업을 순차적으로 수행할지 아닌지에 따른 **순서와 결과(처리) 관점**

</br>

1. Blocking + Synchronous : 다른 작업이 진행되는 동안 자신의 작업을 처리하지 않고 다른 작업의 완료 여부를 바로 받아 순차적으로 처리하는 방식
ex) 자바의 코드 실행 후 커멘드에서 입력을 받는 경우
2. Nonblocking + ASynchronous : 다른 작업이 진행되는 동안에도 자신의 작업을 처리하고 다른 작업의 결과를 바로 처리하지 않아 작업 순서가 지켜지지 않는 방식
ex) 웹 브라우저의 파일 다운로드
3. Blocking + Asynchronous : 다른 작업이 진행되는 동안 자신의 작업을 멈추고 기다리는, 다른 작업의 결과를 바로 처리하지 않아 순서대로 작업을 수행하지 않는 방식이다. 
ex) 보통 개발자 실수..
4. Nonblocking + Synchronous : 다른 작업이 진행되는 동안에도 자신의 작업을 처리하고 다른 작업의 결과를 바로 처리하여 작업을 순차대로 수행하는 방식
ex) 특정 어플리케이션을 설치하는 동안 화면에 나타나있는 로딩율
