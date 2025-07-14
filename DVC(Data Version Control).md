git 으로 관리되는 project에 대용량의 파일들이 있을 때(AI image data, Model 같은)
이를 따로 관리하기 위해 사용된다.
(git으로 관리되는 project에만 가능)

## 목표:
Data,  Model 버젼관리를 분리.
model의 
## 설치법
```bash
pip install dvc
pip install dvc[ssh]
```

## 사용법
```bash
dvc init  #  .dvc 디렉토리를 생성. 
dvc add <file or directory>  #추가.. commit은 없다.

dvc remote add -d ssh_remote ssh://user@host:/path/to/dvc-storage
dvc push   
```



