# Service
* 동일한 서비스를 제공하는 Pod 그룹의 단일 진입점을 제공


## Service Type
* 4가지 Type 지원
  * ClusterIP(default)
    * Pod 그룹의 단일 진입점(Virtual IP) 생성
  * NodePort
    * ClusterIP가 생성된 후 모든 Worker Node에 외부에서 접속가능한 포트가 예약됨
  * LoadBalancer
    * 클라우드 인프라스트럭쳐(AWS, Azure, GCP 등)나 오픈스택 클라우드에 적용
    * LoadBalancer를 자동으로 프로 비전하는 기능 지원
  * ExternalName
    * 클러스터 안에서 외부에 접속 시 사용할 도메인을 등록해서 사용
    * 클러스터 도메인이 실제 외부 도메인으로 치환되어 동작

</br>

### 1. ClusterIP
* selector의 label이 동일한 파드들의 그룹으로 묶어서 단일 진입점(Virtual_IP) 생성
* 클러스터 내부에서만 사용 가능
* type 생략 시 default 값으로 10.96.0.0/12 범위에서 할당됨


![](https://velog.velcdn.com/images/strangehoon/post/83a7ea18-0ee5-4da7-b018-f9099ad730df/image.png)

</br>

### 2. NodePort
* 모든 노드를 대상으로 외부 접속할 수 있는 포트를 예약
* Default NodePort 범위 : 30000-32767
* ClusterIP를 생성 후 NodePort를 예약

</br>

![](https://velog.velcdn.com/images/strangehoon/post/88ea7a4d-e598-4ead-abc4-eb57c686e4a1/image.png)

</br>

### 3. LoadBalancer
* Public 클라우드(AWS, Azure, GCP 등)에서 운영 가능
* LoadBalancer를 자동으로 구성 요청
* NodePort를 예약 후 해당 nodeport로 외부 접근을 허용


![](https://velog.velcdn.com/images/strangehoon/post/995c5c2c-b3e5-4db7-885d-5155226189b3/image.png)

</br>

### 4. ExternalName
* 클러스터 내부에서 External(외부)의 도메인을 설정

![](https://velog.velcdn.com/images/strangehoon/post/24d6e6e7-536f-4373-a3dd-430c8a4bd711/image.png)

</br>

## Headless Service
* ClusterIP가 없는 서비스로 단일 진입점이 필요 없을 때 사용
* Service와 연결된 Pod의 endpoint로 DNS 레코드가 생성됨
* Pod의 DNS 주소 : pod-ip-addr.namespace.pod.cluster.local


![](https://velog.velcdn.com/images/strangehoon/post/b00275e3-0458-4f15-8344-388b388329e7/image.png)


</br>

## Kube-proxy
* Kubernetes Service의 backend 구현
* endpoint 연결을 위한 iptables 구성
* nodePort로의 접근과 Pod 연결을 구현(iptables 구성)

### kube-proxy mode
* userspace
  * 클라이언트의 서비스 요청을 iptables를 거쳐 kube-proxy가 받아서 연결
  * kubernetes 초기 버전에 잠깐 사용
* iptables
  * default kubernetes network mode
  * kube-proxy는 service API 요청 시 iptables rule이 생성
  * 클라이언트 연결은 kube-proxy가 받아서 ipatbles 룰을 통해 연결
  
* IPVS
  * 리눅스 커널이 지원하는 L4 로드밸런싱 기술을 이용
  * 별도의 ipvs 지원 모듈을 설정한 후 적용 가능
  * 지원 알고리즘 : round-robin, least connection, destination hashing, source-hashing ..
