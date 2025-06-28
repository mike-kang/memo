
# branch
```bash
#브랜치명 바꾸기
git branch -m master main

#원격 브랜치 변경
git remote remove origin
git remote add origin ssh://git@192.168.150.233:/opt/git/mac_writer.git
git branch --set-upstream-to=origin/master master


```

## bare repository 사용하기
git --git-dir=/opt/git/repos/DewarpLibraryPGS.git 처럼 bare repository를 지정해서 명령한다.

