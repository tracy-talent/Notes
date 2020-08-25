# Git

* 查看分支

  ```
  1.git branch -r  查看远程分支
  2.git branch -a  查看所有分支
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
  3.git push origin :refs/tags/<tagname>  然后删除远程标签
  ```

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

* 推送更新到远程分支

  ```
  1.git push origin <local-branch>:<remote-branch>
  2.git push -u origin master:master  如果远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
  ```

* 下载远程分支代码并与本地分支合并

  ```
  precedence:git remote add origin <url>
  
  1.git pull origin <remote-branch>:<local-branch>
  2.git fetch origin/<branch>  下载代码
    git merge origin/<branch>  合并代码
  ```

* 更新本地仓库与远程仓库同步

  ```
  prune使得远程仓库中删除的分支在本地也会被删除
  1.git remote update origin --prune
  2.git remote prune origin 
  ```

* 查看提交日志

  ```
  git log --graph --oneline --abbrev-commit
  ```
  
* 撤销提交(commit)

  ```
  1.git reset --hard HEAD^  工作区回退到最近一个commit之前的状态,撤销上一个commit
  2.git reset --hard commitid  直接移到想要的commit状态
  3.git reset --hard HEAD~n  撤销最近的n个commit
  ```

* 强制远程库回退

  ```
  git push origin HEAD --force  强制远程库回退到本地当前所指的commit
  ```

* 撤销工作区最近一次提交后的修改

  ```
  git checkout -- file
  ```

* 撤销添加到暂存区(stage)中的修改

  ```
  git reset HEAD file
  ```

* 查看远程版本库

  ```
  git remote -v
  ```

* merge之后禁止fast faward模式以保留合并分支的历史信息而不被删除

  ```
  git merge --no-ff -m "no fast forward commit" dev
  ```

* 保存暂存区工作

  ```
  当我们在开发分支下的工作还未提交只是在暂存区,但是又需要切换到别的分支修复bug,那么可以使用git stash来保存工作目录和索引状态
  1.git stash 保存当前分支下的工作目录和索引状态
  2.git stash apply 恢复最近保存的工作状态
  3.git stash list 查看保存的工作状态
  4.git stash apply stash@(id)  依据git stash list查到的id来定位恢复
  5.git stash drop 删除最近保存的一个工作状态
  6.git stash pop 恢复最近的一个工作状态并把它删除
  ```

* 建立本地分支与远程分支的关联

  ```
  如果执行git pull命令因为无法track到远程分支而失败,可以使用git pull <remote> <branch>指明,也可以使用如下命令为本地分支和远程分支建立关联
  git branch --set-upstream-to=<remote>/<branch> <localbranch>
  ```

* git rebase

  ```
  1.rebase操作可以把本地未push的分叉提交历史整理成直线；
  2.rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。
  ```

* 标签

  ```
  1.git tag 查看所用标签
  2.git show tagname 查看某个标签的详细信息,包括commitid
  3.git tag -a tagname -m "describtion" commitid 打标签,标签是基于某一次commit来建立的,不指定commitid则基于当前分支最新的commit,描述信息会出现在git show tagname中
  4.git push origin tagname  推送分支到远程
  5.git push origin --tags  推送所有未推送过的本地标签
  6.git tag -d tagname  删除本地分支
  7.git push origin :refs/tags/tagname  删除远程分支(删除不掉则先删除本地对应分支)
  ```

* git clone指定分支

  ```
  git clone -b [branchname] [URL]
  ```

* git submodule相关操作

  ```shell
  1.git submodule add https://git.oschina.net/gaofeifps/leg.git 下载子模块，除了多出一个子模块目录，还会新加一个.gitmodules文件用于存储所有子模块名字与url，主仓库中存的是指向子模块的commit指针，注意切换到子模块的master分支同步到远程最新的commit
  
  2.download带有子模块的仓库有两种方式
  git clone https://git.oschina.net/gaofeifps/body.git
  git submodule init && git submodule update
  #下面这一句的效果和上面三条命令的效果是一样的,多加了个参数  `--recursive`
  git clone https://git.oschina.net/gaofeifps/body.git --recursive
  
  3.将三方库同步到主线，在对子模块更新完毕后，先切换到子模块的mater分支，然后push到远程，然后切到主仓库的master分支push到远程，使得主仓库能即时追踪子模块的最新提交(对于别人开源的第三方库必须先fork一份，然后在fork的基础上更新，如果想合并到原作者的仓库中，则需要pull request)
  
  4.批量更新第三方库
  git submodule foreach git checkout master
  git submodule foreach git submodule update
  
  5.删除submodule，查看.gitmodules文件查看各个submodule-name
  git rm <submodule-name>
  git submodule deinit <submodule-name>
  ```
