
# ConfigMap
### ConfigMap 생성하기
ConfigMap은 컨테이너에 필요한 환경 설정을 컨테이너와 분리해서 제공하는 기능이다.

![](https://velog.velcdn.com/images/strangehoon/post/8c4ccf7a-7ed2-474e-9d8f-c9fdcbe161c1/image.png)

</br>

* ConfigMap 생성

![](https://velog.velcdn.com/images/strangehoon/post/878a5e36-cdc1-4ab7-bce7-ff4b15747ef0/image.png)

</br>

### ConfigMap의 일부분 적용하기
생성한 ConfigMap의 key를 pod의 컨테이너에 적용해보자. 
 ![](https://velog.velcdn.com/images/strangehoon/post/c85834aa-1be0-455c-9a48-10fa282dc5b3/image.png)

</br>

### ConfigMap 전체를 적용하기
생성한 ConfigMap 전체 key를 pod의 컨테이너에 적용해보자.
![](https://velog.velcdn.com/images/strangehoon/post/9051552f-dbbc-41e4-a173-085953078a36/image.png)

</br>

### ConfigMap의 볼륨으로 적용하기
생성한 ConfigMap의 key를 pod의 컨테이너에 볼륨 마운트해보자.

![](https://velog.velcdn.com/images/strangehoon/post/cd54e615-6667-492d-a2af-b3f98c6d6c68/image.png)
