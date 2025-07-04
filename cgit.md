많은 git repository들을 웹으로 보여주기 위한 목적.
git bare repository들을 특정 폴더에 두고, nginx와 cgi를 이용한다.

## 설치
```bash
sudo apt update
sudo apt install cgit git fcgiwrap nginx
```

## 설정파일 
### /etc/cgitrc
```bash
# 기본 설정
cache-size=0
clone-url=http://192.168.150.233/git/$CGIT_REPO_URL
enable-index-links=1
enable-commit-graph=1
enable-log-filecount=1
enable-log-linecount=1
project-list=/var/www/git/projects.list
scan-path=/var/www/git/repos
```
scan-path 는 git bare repository가 있는 directory
clone-url

### /etc/nginx/sites-available/cgit
```nginx
server {
    listen 80;
    server_name 192.168.150.233;
    client_max_body_size 600M;
    root /usr/share/cgit;

    location ~ ^/cgit.cgi(/.*)?$ {
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME /usr/lib/cgit/cgit.cgi;
        fastcgi_param QUERY_STRING $query_string;
        fastcgi_param PATH_INFO $1;
        fastcgi_split_path_info ^(/cgit.cgi)(/.*)$;
        fastcgi_pass unix:/var/run/fcgiwrap.socket;
    }

    location / {
        rewrite ^/$ /cgit.cgi last;
    }

    location ~ \.css$ {
        root /usr/share/cgit;
    }
}


```

## 외부에서 git clone을 할 수 있으려면
cgit과 상관없이 nginx와 git-http-backend가 동작해야 한다.
git-http-backend은 git 설치시에 자동으로 설치되는 fastcgi script이다.

nginx가 해당 url에 대해, 동작할 수 있도록 /etc/nginx/sites-available/cgit에 아래를 추가한다.
```nginx
location ~ ^/git(/.*)?$ {
    include fastcgi_params;
    fastcgi_pass unix:/var/run/fcgiwrap.socket;
    fastcgi_param SCRIPT_FILENAME /usr/lib/git-core/git-http-backend;
    fastcgi_param GIT_PROJECT_ROOT /opt/git/repos;
    fastcgi_param GIT_HTTP_EXPORT_ALL "";
    fastcgi_param PATH_INFO $1;
}

```

그리고, repository 설정(/var/www/git/repos/QParkingSystem.git/config)에 아래 항목이 있어야 한다. 
```config
[http]
    receivepack = true
```
git --git-dir=/opt/git/repos/QParkingSystem.git config http.receivepack true


## cgi test
SCRIPT_FILENAME=/usr/lib/cgit/cgit.cgi QUERY_STRING= PATH_INFO=/ /usr/lib/cgit/cgit.cgi


## 재시작
```bash
sudo systemctl restart fcgiwrap
sudo systemctl restart nginx
```