# 목표
현장 PC(공유기에 묶여 사설 IP를 사용하기 때문에, IP로 직접 접근이 불가능한 PC)와 소통

# 방법

사무실에 VPN 서버를 설치하고, 현장 PC를 등록.
OpenVPN에서는 `client-to-client` 옵션을 켜야 합니다
`client-to-client` 옵션은 VPN 서버에 연결된 **클라이언트들끼리 직접 통신할 수 있도록 해주는 설정**입니다. 기본적으로 OpenVPN은 클라이언트 간 통신을 차단합니다. 이 옵션을 활성화하면 같은 VPN에 붙어 있는 여러 장치가 서로를 직접 접근할 수 있게 됩니다.

**기본(OpenVPN 서버 설정 시)**:  
클라이언트 A가 클라이언트 B에게 패킷을 보내면 서버는 그것을 무시함.


### 인증
서버는 인증서가 필요하고, client도 높은 보안을 위해선 인증서가 필요하다.


### 🎯 예시: OpenVPN 구성

OpenVPN에서는 일반적으로 다음 파일이 필요합니다:

- 서버:
    
    - `server.crt(ca가 인증한 서버 인증서)`, `server.key(server 개인키)`, `ca.crt`
        
- 클라이언트:
    
    - `client.crt`, `client.key`, `ca.crt`, `client.ovpn`
    - 위 client.ovpn 파일에 위 `client.crt`, `client.key`, `ca.crt` 를 모두 포함할 수 있다.
 

### client ip 고정
https://chatgpt.com/share/695b2c56-bfa4-8004-b9cd-83fc14438bf3


### 서버 재 시작 시, client 들이 자동으로 재접속 하기
https://chatgpt.com/share/695b2c56-bfa4-8004-b9cd-83fc14438bf3
https://chatgpt.com/share/695b2e34-0fb0-8004-99c6-a69b336f2f65

