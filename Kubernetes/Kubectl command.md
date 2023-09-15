# Kubectl command
쿠버네티스 클러스터를 관리하는 동작은 대부분이 kubectl이라는 커맨드라인 인터페이스로 실행할 수 있다. kubectl command는 아래 기본구조를 따른다.

> kubectl [command] [TYPE] [NAME] [flags]

* command : 자원(object)에 실행할 명령
  * ex) create, get, delete, edit
* TYPE : 자원의 타입
  * ex) node, pod, service
* NAME : 자원의 이름
* flags : 부가적으로 설정할 옵션
  * ex) --help
  
### 주요 command 알아보기

`kubectl api-resources` : object들의 약어 정보 조회 </br>
`kubectl --help` : 명령어 조회

____________

`kubectl get nodes` : 노드 정보 조회 </br>
`kubectl describe node [node name]` : 특정 노드 정보 자세히 조회

____________

`kubectl run [name] --image=[image name] --port [port 번호]` : 특정 파드 실행(첫번째 방법) </br>
`kubectl get pods` : 파드 정보 조회 </br>
`kubectl describe pod [name]` : 특정 파드 정보 자세히 조회 </br>
`kubectl logs [name]` : 특정 파드 로그 정보 조회 </br>
`kubectl port-forward [name] 8080:80` : 특정 파드 port forwarding </br>
`kubectl run [name] --image=[image name] --port [port 번호] --dry-run -o yaml > [name].yaml` : 특정 파드를 yaml 파일로 생성 </br>
`kubectl create -f [name].yaml`  : yml 파일로 파드 실행(두번째 방법) </br>
`kubectl delete pod [name]` : 특정 파드 삭제

____________

`kubectl create deployment [name] --image=[image name] --replicas=3` : 디플로이먼트 생성 (복수개 파드 생성)    
`kubectl get deployments` : 디플로이먼트 정보 조회 </br>
`kubectl edit deployments.apps [name]` : 특정 디플로이먼트 편집 </br>
`kubectl delete deployments.apps [name]` : 특정 디플로이먼트 삭제

____________

`kubectl exec [name] -it -- /bin/bash` : 특정 컨테이너에 접속
