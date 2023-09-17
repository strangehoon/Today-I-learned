# Controller
**Controller의 종류**

 ![](https://velog.velcdn.com/images/strangehoon/post/1d865d8c-e09f-47cb-9000-4c524790ffa6/image.png)

</br>

### Replication Controller
* 요구하는 Pod의 개수를 보장하며 Pod 집합의 실행을 항상 안정적으로 유지하는 것을 목표
  * 요구하는 Pod의 개수가 부족하면 template를 이용해 Pod를 추가
  * 요구하는 Pod의 수보다 많으면 최근에 생성된 Pod를 삭제
* 기본 구성
  * selector
  * replicas
  * template
  
 <img src = "https://velog.velcdn.com/images/strangehoon/post/8b6d07be-af48-42f7-ad1a-0079d11453ce/image.png" height = "410px" width = "480px" allign = "left">

* replicas 수정
  * First method : yaml 파일에서 수정
  * Second method : command 명령어로 수정
    > kubectl scale rc [rc name] --replicas=[number]

</br>

### ReplicaSet
* ReplicationController와 같은 역할을 하는 컨트롤러
* ReplicationController 보다 풍부한 selector 제공
 ```yml
selector:
  matchLabels:
    component: redis
  matchExpressions:
    - {key: tier, operator: ln, values: [cache]}
    - {key: environment, operator: Notln, values: [dev]
 ```

* matchExpressions 연산자
  * ln : key와 values를 지정하여 key, value가 일치하는 Pod만 연결
  * Notln : key는 일치하고 value는 일치하지 않는 Pod에 연결
  * Exists : key에 맞는 label의 pod를 연결
  * DoesNotExist : key와 다른 label의 pod를 연결
  
 </br>
 
### Deployment
* ReplicaSet을 컨트롤해서 Pod수를 조절
* For Rolling Update & Rolling Back

 <img src = "https://velog.velcdn.com/images/strangehoon/post/b0b44d69-201b-48f2-86e5-0bed4c09315f/image.png" height = "310px" width = "380px" allign = "left">


* Rolling Update
  > kubectl set image deployment <deploy name> <container_name>=<new_version_image> --record
  
* RollBack
  > kubectl rollout history deployment <deploy_name>
kubectl rollout undo deploy <deploy_name> 

</br>

### DemonSet
* 전체 노드에서 Pod가 한개씩 실행되도록 보장
* 로그 수입기, 모니터링 에이전트와 같은 프로그램 실행 시 적용
* demonset은 rolling update/rollback 지원  
 ![](https://velog.velcdn.com/images/strangehoon/post/7b7b1cff-4c53-4a07-af79-83a92c6a8fee/image.png)
> 각각의 node에 nginx 컨테이너 실행되도록 보장

</br>

### StatefulSet
* Pod의 상태를 유지해주는 컨트롤러
    * Pod 이름
    * Pod의 볼륨(스토리지)
* rolling update/rollback 지원
  
![](https://velog.velcdn.com/images/strangehoon/post/5df6267e-87a1-4162-b511-b1558c65b245/image.png)
> 3개의 pod가 각각 이름 sf-nginx-0, sf-nginx-1, sf-nginx-2로 생성된다. demonset과 달리 노드에 Pod 1개씩을 보장하진 않는다.   

</br>

### Job Controller
* kubernetes는 Pod를 계속 running 중인 상태로 유지하도록 보장됨
* Batch 처리하는 Pod는 작업이 완료되면 종료됨
* Batch 처리에 적합한 컨트롤러로 Pod의 성공적인 완료를 보장
  * 비정상 종료 시 다시 실행
  * 정상 종료 시 완료

  ![](https://velog.velcdn.com/images/strangehoon/post/3cb7254c-1c0c-46cf-8a3b-51e5f47f7cf8/image.png)


</br>

### CronJob
* Job 컨트롤러로 실행할 Application Pod를 주기적으로 반복해서 실행
* Linux의 cronjob의 스케줄링 기능을 Jon Controller에 추가한 API
* 다음과 같은 반복 해서 실행하는 Job을 운영해야 할 때 사용
  * Data Backup
  * Send email
  * Cleaning tasks

* Cronjob Schedule: "0 3 1 * *"
   * Minutes (from 0 to 59)
   * Hours (from 0 to 23)
   * Day of the month(from 1 to 31)
   * Month (from 1 to 12)
   * Day of the week (from 0 to 6)
  
  ![](https://velog.velcdn.com/images/strangehoon/post/9746f0be-4ed4-4fc1-bcfb-1a5ea7f9bdaa/image.png)
