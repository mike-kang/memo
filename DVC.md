# Data Version Control

실제 data는 Data Storage에서 저장 및 다운로드 하고, git에는 meta 정보(md5)만 넣는다.

.dvc directory에 기록된다.

commit 시 git 처럼 commit과 commit들이 연결되는 것이 아닌, 파일의 hash 값을 구해서, 변경이 있는 파일만 저장한다. 각 commit들은 이 hash값을 모아둔 것이다.

이미지 폴더를 관리한다.
data----train
           test  
일 경우, data/train, data/test 각각 관리한다.

dvc add data/train 하면,
해당 폴더 안에 파일들을 이용해서 meta file 인 data/train.dvc 파일이 생성된다.
git으로는 이 meta 파일을 관리한다.

dvc도 git과 같이 분산 버젼 관리이다. 
이 이미지 폴더를 원격에 올리기 위해선, ssh를 많이 사용하는데, 원격 정보를 아래와 같이 추가한다.
dvc remote add -d ssh_remote ssh://ksflex@192.168.150.233:/storage/ai_image_data/pgs_96x96_center
(-d : default)

그리고, dvc push 하면 정보가 올라간다.
