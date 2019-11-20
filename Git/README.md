# Git

### 概念

##### 版本库、工作区与暂缓区

* 版本库（Repository）：隐藏的文件 `.git`
* 工作区（Working Directory）：项目目录

* 暂缓区（Stage/Index ）：在`.git` 文件夹里面的index文件（索引文件）



##### 远程仓库

充当服务器的角色，每个人都从这个“服务器”仓库克隆一份到自己的电脑上，并且各自把各自的提交推送到服务器仓库里，也从服务器仓库中拉取别人的提交

Github提供Git仓库托管服务



##### SSH协议

本地Git仓库和GitHub仓库之间的传输是通过SSH加密

因为GitHub需要通过公钥识别出你推送的提交确实是你推送的，而不是别人冒充的

只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了

* 创建SSH Key / 寻找SSH Key

  创建

  ```bash
  ssh-keygen -t rsa -C "youremail@example.com"
  ```

  寻找

  在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

* 登陆GitHub，打开“Account settings”，“SSH Keys”页面上点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容





### 常用命令

##### 初始化版本库 

```bash
git init
```

> 初始化后，自动生成了一个分支master以及指向该分支的指针head

 

##### 将文件添加到暂缓区

```bash
git add <filename1> <filename2> 
```

>git add -A  提交所有变化
>
>git add -u  提交被修改(modified)和被删除(deleted)文件，不包括新文件(new)
>
>git add .  提交新文件(new)和被修改(modified)文件，不包括被删除(deleted)文件



##### 暂存区的所有内容提交到当前分支

```bash
git commit -m <message>
```



##### 查看仓库当前状态

```bash
git status
```



##### 查看修改内容

```bash
git diff <filename>
```

> git diff  <filename> 工作区与暂存区比较
>
> git diff HEAD <filename> 工作区与HEAD ( 当前工作分支) 比较
>
> git diff --staged 或 --cached  <filename> 暂存区与HEAD比较
>
> git diff branchName <filename>  当前分支的文件与branchName 分支的文件进行比较
>
> git diff commitId <filename> 与某一次提交进行比较



##### 查看提交日志

```bash
git log
```

> git log --pretty=oneline 简化日志的输出



##### 查看所有分支的所有操作记录

```bash
git reflog
```

> 可以找回被删除的commit-id



##### 撤销修改（文件还未`git add`）

```bash
git checkout -- <filename>bash
```

> git checkout <filename> : 切换分支filename



##### 撤销暂缓区的修改/删除（文件已经`git add`）

```bash
git reset HEAD <filename>
```



##### 版本回退（文件已经`git commit`）

```bash
git log --pretty=oneline

git reset --hard HEAD^

// 回退后，本地版本落后远程仓库，需要强推到远程仓库
git push -f
```

> git reset --hard HEAD^ 回退上一个版本
>
> git reset --hard HEAD^^ 回退上上一个版本
>
> git reset --hard HEAD~100 回退上100个版本



##### 删除文件（文件已经commit）

```bash
git rm <filename>
git commit -m <message>
```



##### 恢复误删文件（文件已经commit）

```bash
git checkout -- <filename>
```

> git reset HEAD <filename>：恢复只是git add的误删文件，删除也是被看修改的一种



##### 先有本地仓库，后有远程仓库，再本地库关联远程库

1. 本地仓库关联远程仓库

   ```bash
   git remote add origin git@github.com:yourname/project.git
   ```

   > git@github.com:yourname/project.git 是仓库地址
   >
   > 远程库的名字就是`origin`，这是Git默认的叫法

   

2. 关联后，本地仓库内容全部推送给远程仓库

   ```bash
   git push -u origin master
   ```

   > 第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令`git push origin master`



##### 先创建远程库，再克隆到本地仓库

1. 登陆GitHub，创建一个新的远程仓库，勾选`Initialize this repository with a README`

2. 克隆远程仓库

   ```bash
   git clone git@github.com:yourname/project.git
   ```

### 初始化本地已有项目,并推送到远端Git仓库操作

1. 创建本地项目，在项目根目录执行git init命令
    ```bash
    git init
    ```

2. 在git服务器上创建一个仓库，拷贝仓库地址

3. 执行`git remote add origin`，黏贴仓库地址
    ```bash
    git remote add origin https://github.com/KayanChan/uniapp-superhero.git
    ```

4. 从远程分支拉取master分支并与本地master分支合并
    ```bash
    git pull origin master:master
    ```

5. 提交本地分支到远程分支
    ```bash
    git push -u origin master
    ```

6. 将现有项目添加并提交上传
    ```bash
    git add -A
    git config --global core.autocrlf true
    git commit -m '初始化git项目'
    git push --set-upstream origin master
    ```
    
### 切换账号
    ```
    git config --global user.name "Your_username"
    git config --global user.email "Your_email"
    ```
