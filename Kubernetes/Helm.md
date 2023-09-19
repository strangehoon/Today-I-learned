# Helm

### Helm이란? 
* 쿠버네티스 패키지 매니저(https://helm.sh/docs/)
* Helm의 기능
  * 새로운 차트 생성
  * chart로 chart archive(tgz) files로 패키지화하기
  * chart가 저장되는 chart 저장소와 상호작용
  * kubernetes cluster에 chart의 설치 및 제거, 릴리즈 주기 관리
   
</br>

### Install Helm
* Helm 설치하기
>$ curl -fsSL -o get_helm.sh `https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3` </br>
$ chmod 700 get_helm.sh </br>
$ ./get_helm.sh

* Helm 자동 완성 기능 설치하기
> $ source <(helm completion bash) </br>
$ echo "source <(helm completion bash)" >> ~/.bashrc

</br>

### Chart vs Chart Archive
**Chart** : Helm에서 chart는 Kubernetes 애플리케이션을 정의하고 패키징하는 데 사용되는 디렉토리 구조와 파일 집합을 의미한다. 이 디렉토리에는 Kubernetes 리소스 및 설정 파일, 템플릿 및 값 설정 파일(values.yaml) 등이 포함된다. Helm chart는 애플리케이션의 설치, 업그레이드 및 롤백과 관련된 정보를 포함하고 있으며, 이를 사용하여 Kubernetes 클러스터에 애플리케이션을 배포할 수 있다.

**Chart Archive** : Chart archive는 Helm chart를 패키징하고 저장하는 방법 중 하나이다. chart archive는 .tgz 확장자를 가진 압축 파일로서, Helm chart의 모든 구성 요소와 메타데이터를 포함하고 있다. chart archive를 만들면 다른 환경이나 클러스터에서 Helm chart를 쉽게 공유하고 배포할 수 있다.

</br>

### Helm Command
* Repository 추가/삭제
> $ helm repo [add|remove|list] [NAME] [URL]

* Repository 조회 
> $ helm repo list

* Repository에서 제공하는 chart 검색
> $ helm search repo </br>
> $ helm search repo [KEYWORD]

* chart 정보와 세부 정보 조회 
> $ helm show chart [CHART] </br>
> $ helm inspect values [CHART]

* chart 조회
> $ helm list

* 특정 value 수정해서 chart 설치
> $ helm install webserver --set service.type=NodePort  bitnami/nginx

* value.yaml 파일을 수정하여 chart 설치
> $ helm inspect values bitnami/nginx > nginx_value.yaml </br>
-> nginx_value.yml을 수정해서 적용시킨다. 

* chart archive 설치
> $ helm install [chart_name] [CHART]

* chart archive 삭제
> $ helm uninstall [chart_name]
