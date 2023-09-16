# Pod

### Pod 란?
* 컨테이너를 표현하는 k8s API의 최소 단위
* Pod에는 하나 또는 여러 개의 컨테이너가 포함될 수 있음

</br>

### Pod 생성하기
* 첫번째 방법 : kubectl run 명령(CLI)으로 생성
  > $ kubectl run [pod name] --image=[image name]

* 두번째 방법 : Pod yaml을 이용해 생성

  <img src = "https://velog.velcdn.com/images/strangehoon/post/55a778cc-eeb3-4b6e-8a34-2bf8942993d1/image.png" height = "310px" width = "380px" allign = "left">
 
   > $ kubectl create -f [file name].yaml

* 현재 동작중인 Pod 확인
 
  > $ kubectl get pods </br>
$ kubectl get pods -o wide </br>
$ kubectl get pods [pod name] -o yaml : 현재 동작중인 특정 pod를 yaml 형식으로 조회 </br>
$ kubectl get pods [pod name] -o json : 현재 동작중인 특정 pod를 yaml 형식으로 조회 </br>

</br>

### multi-container Pod 생성하기
Pod 안에 여러개의 컨테이너가 들어있을 수 있다. 하지만 하나의 Pod 안에 들어있는 컨테이너들은 IP주소가 같다.  

  <img src = "https://velog.velcdn.com/images/strangehoon/post/a89d3765-4d40-4439-8ebc-0fd399af06c7/image.png" height = "310px"> 

* multi-container Pod 생성하기

  <img src = "https://velog.velcdn.com/images/strangehoon/post/6b3e7fcc-0682-4fc5-9def-16ec7261170f/image.png" height = "310px">

  > kubectl create -f [file 이름].yaml
 
  > READY는 현재 Pod 안에 존재하는 컨테이너 개수를 의미한다. single-container Pod에 비해 multi-container Pod는 1이 아니다.
  
  ![](https://velog.velcdn.com/images/strangehoon/post/35da6d53-b788-440a-9940-1526cc0dcb48/image.png)

</br>

### Pod 관리하기
* 동작중인 pod 정보 보기
  > $ kubectl get pods </br>
$ kubectl get pods -o wide </br>
$ kubectl describe pod [pod name]

* 동작중인 pod 수정
  > $ kubectl edit pod [pod name]

* 동작중인 pod 삭제
  > $ kubectl delete pod [pod name] </br>
$ kubectl delete pod --all

</br>

### LivenessProbe을 이용한 Self-healing Pod
* livenessProbe란? 
  * Pod가 계속 실행할 수 있음을 보장
  * Pod의 spec에 정의
   
  <img src = "https://velog.velcdn.com/images/strangehoon/post/bf33158f-dcd3-4560-a3de-9f36765fa32b/image.png" height = "310px">

*  livenessProbe 매커니즘
   * httpGet probe : 지정한 IP 주소, port, path에 HTTP GET 요청을 보내, 해당 컨테이너가 응답하는지를 확인한다. 반환코드가 200이 아닌 값이 나오면 오류, 컨테이너를 다시 시작한다.
     ```yml
     livenessProbe:
       httpGet:
         path: /
         port: 80
     ```

   * tcpSocket probe : 지정된 포트에 TCP 연결을 시도, 연결되지 않으면 컨테이너를 다시 시작한다.
     ```yml
     livenessProbe:
       tcpSocket:
         port: 22
     ```

   * exec probe : exec 명령을 전달하고 명령의 종료코드가 0이 아니면 컨테이너를 다시 시작한다.
     ```yml
     livenessProbe:
       exec:
         command:
         - ls
         - /data/file
     ```
* liveness probe 매개변수
  * periodSeconds : health check 반복 실행 시간(초)
  * initialDelaySeconds : Pod 실행 후 delay할 시간(초)
  * timeoutSeconds : health check 후 응답을 기다리는 시간(초)

  <img src = "https://github.com/strangehoon/Today-I-learned/assets/117654450/3b007326-a80a-43f0-afd7-5c9d2fc02010" height = "310px" width = "480px" allign = "left">
  
  > 따로 지정안하면 default 값으로 설정된다. 


</br>

### init container
* 앱 컨테이너 실행 전에 미리 동작시킬 컨테이너
* 본 컨테이너가 실행되기 전에 사전 작업이 필요할 경우 사용
* 초기화 컨테이너가 모두 실행된 후에 앱 컨테이너를 실행

 ![](https://velog.velcdn.com/images/strangehoon/post/9435445d-ddcb-4bc4-b082-5b51d3dedd1a/image.png)

</br>

### infra container(pause)
* 파드에 대한 컨테이너 외에 존재하는 infra와 관련된 컨테이너


</br>

### static Pod 
* API server 없이 특정 노드에 있는 kublet 데몬에 의해 직접 관리
* 특정 노드의 /etc/kubernetes/manifests/ 디렉토리에 k8s yaml 파일을 저장 시 적용됨

</br>

### Pod에 리소스 할당하기

* Pod Resource 요청 및 제한
  * Resource Requests
    * pod를 실행하기 위한 최소 리소스 양을 요청
  * Resource Limits
    * pod가 사용할 수 있는 최대 리소스 양을 제한
    * memory limit을 초과해서 사용되는 pod는 종료되며 다시 스케줄링 된다

 <img src = "https://velog.velcdn.com/images/strangehoon/post/984fd54f-61e8-4b37-92ac-481c0431f7c0/image.png" height = "410px" width = "380px" allign = "left">

</br>

### Pod의 환경 변수 설정하기
**환경변수**
* Pod 내의 컨테이너가 실행될 때 필요로 하는 변수
* 컨테이너 제작 시 미리 정의
  * NGINX Dockerfile의 예
    * ENV NGINX_VERSION 1.19.2
    * ENV NJS_VERSION 0.4.3
* Pod 실행 시 미리 정의된 컨테이너 환경변수를 변경할 수 있다.

 <img src = "https://velog.velcdn.com/images/strangehoon/post/2d120be7-2521-4084-b278-bd26fb618309/image.png" height = "410px" width = "380px" allign = "left">

기존에 nginx에는 원래 MYVAR이라는 환경 변수가 없었는데 name : MYVAR, value = "testvalue"라는 환경변수를 넣어줬다. 

</br>

### Pod 구성 패턴의 종류

**Pod 실행 패턴**
* Pod를 구성하고 실행하는 패턴
* multi-container Pod

 ![](https://velog.velcdn.com/images/strangehoon/post/02a42009-fae4-4a5a-8763-2e771cf05104/image.png)
