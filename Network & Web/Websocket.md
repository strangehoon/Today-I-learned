# WebSocket이란
WebSocket은 서버와 클라이언트 간의 메시지 교환을 위한 통신 규약(프로토콜)이다. 최초 접속에서만 http 프로토콜 위에서 handshaking하기 때문에 http header를 사용한다. WebSocket을 위한 별도의 포트는 없으며 기존 포트(80, 443)를 사용한다.

**WebSocket의 특징**

1. 양방향 통신
   * 데이터 송수신을 동시에 처리할 수 있는 통신 방법
   * 클라이언트와 서버가 서로에게 원할 때 데이터를 주고 받을 수 있다.
   * 통상적인 Http 통신은 Client가 요청을 보내는 경우에만 Server가 응답하는 단방향 통신
2. 실시간 네트워킹 
   * 웹 환경에서 연속된 데이터를 빠르게 노출
   * Ex) 채팅, 주식, 비디오 데이터
   * 여러 단말기에 빠르게 데이터를 교환
   
</br>

**WebSocket 동작 과정**

![](https://velog.velcdn.com/images/strangehoon/post/40a99d58-c3c2-4b61-8bc2-8208a2fa102d/image.png)

1. HandShake : 최초 연결 요청 시 클라이언트에서 Http를 통해 웹서버에 handshake 요청을 한다. handshake를 위해 클라이언트는 서버에 아래와 같은 Http header를 보낸다.   
 
      ```yml
    GET /chat HTTP/1.1
    Host: server.example.com
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Key: x3JJHMbDL1EzLkh9GBhXDw==
    Sec-WebSocket-Protocol: chat, superchat
    Sec-WebSocket-Version: 13
    Origin: http://example.com
    ```

     그러면 서버는 아래와 같이 응답한다. 101 Status는 성공을 의미한다.

      ```yml
    HTTP/1.1 101 Switching Protocols
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Accept: HSmrc0sMlYUkAGmm5OPpG2HaGWk=
    Sec-WebSocket-Protocol: chat
    ```

2. 양방향 통신 : client와 server는 서로 메세지를 보내며 통신하는데 프레임 단위로 이루어진다. 기존 http보다 가볍다.

3. 연결종료 : client 혹은 server 양측 누구나 연결을 종료할 수 있다. 연결 종료를 원하는 측이 close frame을 상대쪽으로 전송하면 된다.


</br>


**WebSocket 한계**

1. HTML5 이후에 나온 기술 </br>
WebSocket은 HTML5이후에 나온 최신 기술이다. 따라서 Html 5이전의 브라우저에서는 동작이 안될 수 있다.
    > 대안으로 socket.io, SockJS 등

3. WebSocket은 데이터를 주고 받을 수 있게 해줄 뿐 그 이상의 일을 하지 않음 </br>
HTTP는 형식을 정해두어서 모두가 약속을 따르기만 하면 해석 할 수 있지만, WebSocket은 형식이 정해져 있지 않아 애플리케이션에서 쉽게 해석하기 힘들다.

   > 대안으로 Stomp가 있다. Stomp(Simple Text Oriented Message Protocol)는 채팅 통신을 하기 위한 형식을 정의할 수 있다.

</br>
