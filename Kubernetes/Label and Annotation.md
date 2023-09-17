# Label and Annotation
### Label이란?
* Node를 포함하여 pod, deployment 등 모든 리소스에 할당
* 리소스의 특성을 분류하고, Selector를 이용해서 선택
* key-value 한쌍으로 적용


![](https://velog.velcdn.com/images/strangehoon/post/797da6a3-d9d9-47ee-b97d-ed482652578a/image.png)
> 리소스가 많아지면 관리하기 힘들어진다. 

</br>

label을 이용하면 리소스 관리에 용이하다. 아래는 name과 release라는 label을 적용한 예이다.

![](https://velog.velcdn.com/images/strangehoon/post/01578017-afb9-405f-ba55-d377d17ca579/image.png)

</br>

### Label과 Selector
* Label
```yml
metadata:
  labels:
    rel : stable
    name : mainui
```

* Selector
```yml
selector:
  matchLabels:
    key: value
  matchExpressions:
    - {key: name, operator: ln, values: [mainui]}
    - {key: rel, operator: Notln, values: ["beta", "canary"]}
 ```

* 특정 리소스에 label 설정
> kubectl label <리소스> <리소스 이름> <레이블 키>=<레이블 값>

* label 명이 같은 pod를 출력(selector)
> kubectl get pods -l [레이블 키]=[레이블 값]


</br>

### Annotation
* Label과 동일하게 key-value를 통해 리소스의 특성을 기록
* Kubernetes에게 특정 정보 전달할 용도로 사용
  * 예를 들어 Deployment의 rolling update 정보 기록
  ```yml
  annotations:
    kubernetes.io/change-cause: version 1.15
  ```
* 관리를 위해 필요한 정보를 기록할 용도로 사용
  * 릴리즈, 로깅, 모니터링에 필요한 정보들을 기록
  ```yml
  annotations:
    builder: "sanghoon Lee (abc@naver.com)"
    buildDate: "20000101"
    imageRegistry: https//hub.docker.com/
   ```

</br>

### Label을 이용한 카나리 배포
* Canary 배포
  * 기존 버전을 유지한 채로 일부 버전만 신규 버전으로 올려서 신규 버전에 버그나 이상은 없는지 확인하면서 순차적으로 배포하는 방법 

![](https://velog.velcdn.com/images/strangehoon/post/1b44d7c9-f568-4cd6-b694-85ce1e3a505e/image.png)
> replicas 수를 조절하면 된다.
