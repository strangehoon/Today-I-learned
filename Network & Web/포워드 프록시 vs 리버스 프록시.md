# 포워드 프록시 vs 리버스 프록시
 프록시 서버란 클라이언트와 서버 사이의 중계 서버이자 통신을 대리 수행하는 서버로 프록시 서버의 위치에 따라 포워드 프록시, 리버스 프록시 서버로 나뉜다.

**포워드 프록시** : 일반적인 프록시라고 하면 포워드 프록시를 말한다. 클라이언트에서 서버로 리소스를 요청할 때 직접 요청하지 않고 프록시 서버를 거쳐서 요청한다. 

1. 캐싱 : 첫 번째 요청 이후로 동일한 요청이 들어올 경우 프록시 서버에 캐싱된 내용을 전달해줌으로써 성능을 향상시킬 수 있다. 
2. 암호화 : 클라이언트 측에서 프록시 서버를 거쳐서 웹 서비스를 이용할 경우 서버 측에서는 요청받을 때 클라이언트의 IP가 아닌 프록시 서버의 IP를 전달받게 된다. 따라서 서버 측으로부터 클라이언트의 정보를 숨길 수 있다.
3. 제한 : 보안이 중요한 사내망에서 특정 사이트에 접속하는 것을 막도록 웹 사용 환경을 제한할 수 있다. 

![](https://velog.velcdn.com/images/strangehoon/post/e18bff39-ba5c-446b-bd88-2fc80928ac4b/image.png)


</br>


**리버스 프록시** : 포워드 프록시와 반대로 애플리케이션 서버의 앞단에 위치하여 클라이언트가 서버를 요청할 때 리버스 프록시를 호출하고, 리버스 프록시가 서버로부터 응답을 전달받아 다시 클라이언트에게 전송하는 역할을 한다.

1. 로드밸런싱 : 리버스 프록시 뒤에 여러 개의 WAS를 둠으로써, 사용자 요청을 분산시킬 수 있다.
2. 보안 : 리버스 프록시를 사용하면 본래 서버의 IP 주소를 노출시키지 않을 수 있다. 클라이언트는 본 서버의 url을 모른 채 리버스 프록시 url을 통해 서비스를 이용하게 된다.
3. 캐싱 : 포워드 프록시와 유사

![image](https://github.com/strangehoon/Today-I-learned/assets/117654450/8ec1f282-f71e-4b7c-948e-608c420fc454)


> 우리가 구성하는 일반적인 web(Apache, nginx) - was(Tomcat) 분리 형태에서 web(Apache, nginx)이 리버스 프록시 서버다. 참고로 Apache에는 web, was가 둘다 존재하지만 리버스 프록시 서버라고 볼 수는 없다.

