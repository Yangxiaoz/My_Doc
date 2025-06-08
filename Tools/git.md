# git基础命令与工作流使用指南

> Written  In 2025_03.21 __by yxl   
> Last Edited In 2025_03.21__by yxl

本文记录关于git的一些基本指令使用以及日常工作流中使用git的流程

## 一、git核心概念图示

TBD...

## 二、常用指令


1. branch

```bash
git branch                         #查看当前分支名称列表
git branch  <new_name>             #创建一个名为new_name的新分支
```


2. checkout

```bash
git checkout  <name>              #切换到 name分支
git checkout -b <new_name>        #创建并切换到 new_name分支
```

3. 改动提交

```bash
#查看当前本地未提交的改动
git diff 
```

```bash
#暂存当前所有本地改动
git add .                          #缓存所有改动
git add <file1> <file2> <src/>     #缓存指定文件/文件夹改动
git add -p                         #交互式缓存文件改动
#查看已缓存的信息
git status 

```

```bash
#提交缓存
git commit -m "describe this commit"
```


4. 版本控制

```bash
#云端更新
git fetch --prune                   #从远程仓库获取最新数据，并清理（prune）已删除的远程跟踪分支
git pull    origin                  #拉取远端最新代码
```

```bash
#分支变更
git merge   <branch_1>                #将branch_1分支与当前所在的分支进行合并
git rebase  <branch_base>             #将当前分支变基到branch_base分支
``` 

```bash
#范围变基
git rebase --onto <newbase> <upstream> <branch = local_brach>
                                    # newbase  ：变基目的分支-- hash 
                                    # upstream ：变基源上游--  hash or name
                                    # branch   :变基源分支--   hash or name (defualt to current branch)
```

```bash
#版本追踪
git branch -vv                      #查看本地分支上下游跟踪情况
git branch --set-upstream-to=local_base <target_branch>  
                                    # 为分支设置上游为 local_base
git rebase                          # 无需指定分支名,快速变基
```



```bash

```
