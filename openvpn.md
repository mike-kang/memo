```bash
sudo systemctl restart openvpn@server
```

## 서버에 telnet 붙이기
```
/etc/openvpn/server.conf

management 127.0.0.1 7505
```

```bash
telnet 127.0.0.1 7505
> status

```

## window client 추가하기
```
client 인증서를 생성하고, 이를 이용해, <client name>.ovpn 파일을 생성. 이를 client pc의 
C:\Users\<사용자>\OpenVPN\config 에 둔다.
```



##  client 제거하기위해 인증서 제거

각 client 인증서는 serial key로 관리된다.

