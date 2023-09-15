# 쿠버네티스 컴포넌트

![](https://velog.velcdn.com/images/strangehoon/post/2ad5bb06-706a-4c1a-a5b2-43d3b2f761b1/image.png)


### 마스터 컴포넌트

* etcd
  * key-value 타입의 저장소
* kube-apiserver
  * k8s API를 사용하도록 요청을 받고 요청이 유효한지 검사
* kube-scheduler
  * 파드를 실행할 노드 선택
* kube-controller-manager
  * 파드를 관찰하며 개수를 보장

</br>

### 워커 노드 컴포넌트
* kubelet
  * 모든 노드에서 실행되는 k8s 에이전트
  * 데몬 형태로 동작
* kube-proxy
  * k8s의 network 동작을 관리
  * iptables rule을 구성
* 컨테이너 런타임
  * 컨테이너를 실행하는 엔진
  * docker, containerd, runc

</br>

### 애드온
* 네트워크 애드온
  * CNI - weave, calico, flaneld, kube-route ..
* dns 애드온
  * coreDNS
* 대시보드 애드온
* 컨테이너 자원 모니터링
  * cAdvisor
* 클러스터 로깅
  * 컨테이너 로그, k8s 운영 로그들을 수집해서 중앙화
  * ELK(ElasticSearch, Logstash, Kibana), EFK(ElasticSearch, Fluentd, Kibana), DataDog
  

