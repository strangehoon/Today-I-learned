# Kubernetes namespace
namespace는 k8s API 종류 중 하나로 클러스터 하나를 여러 개 논리적인 단위로 나눠서 사용하는 것이다. namespace로 인해 k8s 클러스터 하나를 여러 팀이나 사용자가 함께 공유할 수 있으며 주로 용도에 따라 실행해야 하는 앱을 구분할 때 사용한다. 


### namespace 사용하기

* namespace 생성
  * CLI
    > $ kubectl create namespace [name] </br>
  $ kubectl get namespaces
  * yaml
    > $ kubectl create namespace [name] --dry-run -o yaml > [name]-ns.yaml </br>
  $ vim [name]-ns.yaml </br>
  $ kubectl create -f [name]-ns.yaml

* namespace 관리 </br>
  참고로 namespace를 지우면 그 안의 pod, deployment 등 모두 삭제 된다.
  > $ kubectl get namespace </br>
$ kubectl delete namespace


* namespace 활용
  > $ kubectl get pods -n [name] : 특정 namespace의 pods 조회 </br>
 $ kubectl get pods -all-namespaces : 전체 namespace의 모든 pods 조회


</br>

default, kube-node-lease, kube-public, kube-system은 클러스터가 생성될 때 자동으로 만들어지는 namespace이다. namespace를 따로 지정하지 않으면 default namespace이다. 

 <img src = "https://velog.velcdn.com/images/strangehoon/post/ee9faf23-ec27-487a-bc85-41f6f6f27461/image.png" height = "310px" width = "680px" allign = "left">

</br>

### 사용할 namespace switch
기본으로 사용하는 namespace를 default가 아닌 다른 이름의 namespace로 switch 할 수 있다. 

First : namespace를 포함한 context 등록
  > $ kubectl config --help </br>
$ kubectl config set-context [context NAME] --cluster=kubernetes --user=kubernetes-admin --namespace=[namespace NAME] </br>
$ kubectl config view 

Second : 등록된 namespace로 context 변경
  > $ kubectl config use-context [context NAME]
