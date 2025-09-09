
보안을 강화한 sftp와 일반 ftp가 있다.
## ftp를 설치하려면,
```
sudo apt install vsftpd -y
```
## 서비스 상태 확인
```
systemctl status vsftpd
```

## 설정 파일 수정.
기본 설정은 `/etc/vsftpd.conf`

## 이름의 의미 요약

- **Active 모드**: 서버가 클라이언트에 “적극적으로(Active)” 연결을 시도.
    
- **Passive 모드**: 서버는 포트 열어두고 “수동적으로(Passive)” 기다리고, 클라이언트가 연결.