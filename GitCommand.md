# git常用指令
## 分支操作

操作远程分支

- ```
  - git push origin master:newbranch 	//增加远程仓库的分支
  
  - git remote add newbranch  	//增加远程仓库的分支
  
  - git remote show  	// 列出现在远程有多少版本库
  
  - git remote rm newbranch 	// 删除远程仓库的新分支
  
  - git remote update  	//更新远程所有版本的分支
  
  ```

 更新本地分支

```
git fetch
```

拉取远程分支

```
git pull [RemoteHostname] [RemoteBranchname]:[LocalBranchname]  //格式
git pull origin next:master //取回“origin”主机的“next”分支，与本地的“master”分支合并
```


删除本地分支：

```
git branch –D newbranch
```

删除服务器仓库分支

```
git branch –rd origin/newbranch
```

同步远端已删除的分支

```
git remote prune origin
```

## 其他操作

 列出日志信息

```
git log –-all
```

 查找字符串

```
git grep "hello"  //查找是否有“hello”字符串,区分大小写
```

 查看状态输出

```
git status
```

修改最近一次提交

```
 git commit --amend
```

查看文件

```
git ls-files –d    //查看已经删除的文件
git ls-files –d |xargs git checkout   //将已删除的文件还原
```

显示内容或修改的内容

```
- git show v1

  显示**“tag v1”**的修改内容

- git show HEAD

  显示当前版本的修改文件

- git show HEAD^

  显示前一版本所有的修改文件

- git show HEAD~4

  显示前4版本的修改文件
```

# 更新.gitignore

个自项目下的ignore文件

```
git rm -r --cached . //清空缓存
git add . //重新提交
git commit -m "update .gitignore"
git push 对应分支
```

本地全局配置

```
git config --global core.excludesfile igniore文件绝对路径 .gitignore_global
```

```
git config -l //查看配置是否成功
```

# 查看rsa密钥

```
 cat ~/.ssh/id_rsa.pub
```

如果不存在则生成公钥

```
 ssh-keygen
```

