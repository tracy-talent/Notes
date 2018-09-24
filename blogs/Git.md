

# Git

<<<<<<< HEAD
* 查看远程分支

  ```
  git branch -r
=======
* 查看分支

  ```
  1.git branch -r  查看远程分支
  2.git branch -a  查看所有分支
>>>>>>> c5a8a7ad47e8169a8f4c03856b95d7c4b05fd532
  ```

* 删除远程分支

  ```
  1.git push origin --delete <branchname>  直接删除远程分支
  2.git push origin :<branchname>   推送一个空分支到远程就相当于删除远程分支
  ```

* 删除标签(标签是静态的，用于标志一个里程碑)

  ```
  1.git push origin --delete tag <tagname>  直接删除远程标签
  2.git tag -d <tagname>  删除远程标签的先决条件是先删除本地标签
    git push origin :refs/tags/<tagname>  然后删除远程标签
  ```


<<<<<<< HEAD
=======
* 合并分支

  ```
  1.git fetch <remote-reponame>  
  2.git merge <remote-repo>/<branchname>
  ```

* 建立分支

  ```
  1.git branch <branchname> 在当前分支的基础上建立一个新分支
  2.git branch <branchname> <otherbranch>  指定分支基础上建一个分支
  3.git branch <branchname> <remote-repo>/<otherbranch> 在指定分支基础上建一个分支
  2.git checkout -b <branchname> 建立并切换分支
  ```
>>>>>>> c5a8a7ad47e8169a8f4c03856b95d7c4b05fd532
