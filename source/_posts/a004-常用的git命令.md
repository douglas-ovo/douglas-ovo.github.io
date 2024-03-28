---
title: 常用的git命令
categories:
  - 前端学习
tags:
  - Git
date: 2022-07-07 15:58:23
index_img: https://img0.baidu.com/it/u=1641948811,72191990&fm=253&fmt=auto&app=138&f=JPG?w=1000&h=420
---

### github 访问慢？

1. 使用 dns 查询工具，查询 github.com，将 TTL 最小的 ip 复制
2. 找到对应路径 C:\Windows\System32\drivers\etc 下的 hosts 文件
   ![图示](https://img-blog.csdnimg.cn/2021042623563665.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzYwODc0NA==,size_16,color_FFFFFF,t_70#pic_center)

### 本地信息配置

```git
git config --global --list
git config --global user.name
git config --global user.email
```

### SSH 配置

```git
ssh-keygen -t rsa -C 'xxx@xxx.com'
```

> 公钥路径：C:/Users/Administrator/.ssh/id_rsa.pub  
> 验证 ssh 是否生效：ssh -T git@github.com

### 提交注释

feat: 增加新功能（feature）
fix:  修改bug 
perf: 改进，性能优化  
docs: 文档（documentation）  
style: 空白/格式/缺少符号等（不影响代码运行的变动）  
refactor: 重构（即不是新增功能，也不是修改 bug 的代码变动）  
chore: 构建过程或辅助工具的变动  
revert: 撤销，版本回退  
test：测试  
build: 打包  

### 基本命令

```git
git branch -avv
git branch -vv
git remote -vv
git diff
git log --oneline
git checkout xxx      或  git switch xxx
git checkout -b xxx   或  git switch -c xxx
```

### 基本使用

```git
files change...
git pull
git add .
git commit -m 'xxx'
git push
```

### 创建新工作区并推送到远程仓库

1. 由自己创建仓库

```git
git init
git add .
git commit -m 'xxx'
git branch -M main                     //重命名当前本地分支，初始分支名为master
git remote add origin git@xxxx.git     //origin为远程仓库名，可以自定义
git push origin -u main:master         //main为本地分支名，master为远程分支名，之后push需要指定远程仓库名
或
git push origin -u master              //本地分支名和远程分支名一样，之后可直接push，本地分支名和远程分支名尽量保持一样
```

2. 由别人创建仓库

```git
git clone  git@xxxx.git                //克隆默认分支，克隆后本地默认与指定远程分支建立联系
或
git clone -b xxx git@xxxx.git          //克隆其他分支，克隆后本地默认与指定远程分支建立联系
```

### 新建分支并推送远程仓库的对应分支

> **分支是用来开发不同功能的**

```git
git checkout -b 新分支名
git push origin -u dev
```

### 分支重命名

1. 本地分支

```git
git branch -m 原分支名称 新分支名称
```

2. 远程分支

```git
git push origin -d 自己的原分支名称
git push origin -u 新分支名称
```

3. 重命名分支为远程默认分支时
   > github 打开当前仓库——>settings——>branches——>手动重命名

### 删除分支

```git
git branch -d 本地分支名
git push origin -d 远程分支名
```

### 合并分支

> 切换到合并分支，合并其他工作树干净的分支

```git
git merge 被合并分支名
```

### 拉取远程新的分支并与本地建立连接

```git
git checkout -b 本地分支名 origin/远程分支名
files change...
git add .
git commit -m 'xxx'
git push

或

git fetch origin 远程分支名:本地分支名
git switch 本地分支名
files change...
git add .
git commit -m 'xxx'
git push origin -u 远程分支名
```

### 移除工作区修改

```git
git checkout .

或

git checkout 文件路径
```

### 取消 add 操作

```git
git reset
```

### 取消 commit 操作
之前提交过
```git
git reset --soft HEAD^     //仅撤销commit
git reset --mixed HEAD^    //撤销commit，add
```

第一次提交
删除.git文件夹重新提交

### 版本控制

1. 版本回退
   > 不会破坏之前的版本

```git
git reset --hard commitid
files change...
git add .
git commit -m 'xxx'
git push
git pull 解决冲突
```

> 会破坏之前的版本

```git
git reset --hard commitid
git push -f
```

2. 切换新分支指向想要回退的版本

```git
git checkout -b 分支名 commitid
```

### tag

> **tag 是用来记录版本的**
> tag 给当前仓库 commitid 记录对应的版本信息，之后可以根据 tag 找到版本对应的 commitid 进行版本控制
> 开发完新功能后将功能分支合并到主分支，之后打 tag，一般只用给主分支打 tag

```bash
git tag xxx                            //给最近的commitid打tag，当前未提交则为上次commitid打tag，当前已提交则为本次commitid打tag
git tag xxx commitid                   //给指定的commitid打tag
git tag xxx -m "注释" commitid         //给指定的commitid打tag同时添加注释
git push origin xxx                    //将本地tag推送到远程
git push origin --tag                  //本地所有tag推送到远程
git tag -d xxx                        //删除本地tag，删除本地后git pull会将远程的tag拉下来
git push origin -d xxx                 //删除远程tag
git show xxx                           //查看对应tag提交信息
git tag                                //查看本地所有tag
git ls-remote --tag                    //查看远程所有tag
```

### 常见问题

1. 改了文件名的大小写，git 会认为文件没有变化，从而导致本地和远程仓库不一致

   ```bash
   git config core.ignorecase false
   ```

   ​

---

官方文档：[Git](https://git-scm.com/book/zh/v2)
