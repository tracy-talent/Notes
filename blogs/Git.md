

# Git

* 查看远程分支

  ```
  git branch -r
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


