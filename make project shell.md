```bash
#!/bin/bash

if [ $# -eq 0 ]; then
        read -p "Project Name?" proj
        read -p "Description?" desc

        read -p "Project Name:$proj Description:$desc OK(yes/no)?" val
elif [ $# -eq 2 ];then
        proj=$1
        desc=$2
        val=yes
fi

if [[ $val == "yes" ]]; then
  cd /opt/git/repos
  mkdir $proj.git
  cd $proj.git
  git init --bare
  git --git-dir=/opt/git/repos/$proj.git branch -m main
  git --git-dir=/opt/git/repos/$proj.git config http.receivepack true
  [[ -n $desc ]] && echo $desc > /opt/git/repos/$proj.git/description

  chown -R www-data:www-data /opt/git/repos/$proj.git
  chmod -R 755 /opt/git/repos/$proj.git

fi

```
