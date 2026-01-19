WebSocket은 브라우저가 HTTP 요청으로 시작해서, Handshake를 통해 연결을 WebSocket 프로토콜로 “업그레이드”하고, 이후에는 HTTP와 완전히 다른 양방향 통신을 하는 방식이다.

web socket과 TCP 연결은 1:1
(browser에서 websocket을 생성할 때 마다, 서버 쪽에서는 accept 가 호출된다.)