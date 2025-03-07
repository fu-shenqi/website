# Git

## 介绍

Git是一种分布式版本控制系统，它可以记录文件的变更历史并协调多人在同一个代码库上的开发。使用Git，开发人员可以轻松地跟踪代码的修改、回退到以前的版本、合并不同的代码分支和解决代码冲突等任务。Git最初由Linus Torvalds创建，现在是开源社区中最流行的版本控制系统之一。

### 在Git中，有四个重要的概念：工作区、缓冲区、本地仓库和远程仓库。

* 工作区：工作区（Working Directory）是指开发者正在进行开发工作的目录。它包含了项目的源码文件、资源文件等内容。在这个目录下，开发者可以自由修改、添加、删除文件等操作。

* 缓冲区：缓冲区（Staging Area）也称为索引（Index），它是一个临时存储区域，用于存放即将提交到本地仓库的文件变更。开发者对工作区所做的修改，需要先通过git add命令将修改加入到缓冲区，才能提交到本地仓库。

* 本地仓库：本地仓库（Local Repository）是指保存在本地计算机上的Git仓库。它包含了代码库的完整历史记录、分支、标签等信息。在开发过程中，每次提交到缓冲区的变更，都可以通过git commit命令保存到本地仓库中。

* 远程仓库：远程仓库（Remote Repository）是指保存在远程服务器上的Git仓库。它包含了与本地仓库相同的内容，但它是由多个开发者共享的中央代码库。开发者可以通过git push命令将本地仓库中的变更推送到远程仓库，也可以通过git pull命令将远程仓库的变更更新至本地仓库。

## 信息配置

```
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱"
```

### 代理配置

```
git config --global http.proxy http://127.0.0.1:7890
```

清除代理
```
git config --global --unset http.proxy 
git config --global --unset https.proxy
```

## 查看信息

```
git config --list
```

## 操作仓库

### 拉取远程仓库

```
git clone https://github.com/JackLau1222/OpenConverter
```

### 更新本地仓库(自动同步)

```
git pull 
```

### 更新本地仓库(手动同步)

```
git fetch 
git merge 
```

### 添加一个名为test的cpp文件（Unix/Linux）

```
touch test.cpp 
```

### 添加一个名为test的cpp文件（Windows）

```
type nul > test.cpp
```

### 将此更改提交到缓冲区

```
git add test.cpp 
```

### 将更改提交到本地仓库

```
git commit -a -m “add test.cpp” 
```
在commit中，我们可以使用-m参数，以便能够直接在命令行上提供日志消息。如果您希望通过交互式编辑器会话提供详细的日志消息，也可以这样做。你需要配置Git在Git提交期间启动你最喜欢的编辑器(去掉-m参数);如果尚未设置，则可以设置

$GIT_EDITOR环境变量如下:
```
# In bash or zsh
$ export GIT_EDITOR=vim

# In tcsh
$ setenv GIT_EDITOR emacs
```

更改commit message
```
git commit --amend
```

更改commit author email
```
git commit --amend --author="Jack Lau <xxxx@gmail.com>"
```

### 提交到目标仓库

```
git push
```

### 查看提交日志

```
git log
```

### 查看提交状态

```
git status
```

### 代码回滚

```
git reset --hard <commit_id>
```

### 使远程仓库回滚生效

```
git push orgin main --force
```

### 查看可用分支

```
git branch
```

### 切换到可用分支

```
git checkout <branch-name>
```

## 修改历史记录
### 修改最新的提交内容
```
git commit --amend --allow-empty
```
### 使用filter-branch工具删除指定文件"*.ipch"

```
git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch **/*.ipch' --prune-empty --tag-name-filter cat -- --all
```


### 使用bfg工具删除指定文件夹名

```
bfg --delete-folders ".vs"  
```

### 删除后执行以下命令实现垃圾回收，合并对象

```
git reflog expire --expire=now --all && git gc --prune=now --aggressive 
```

## git send-email
配置SMTP基本信息（以qq为例）
```Shell
git config --global sendemail.smtpServer smtp.qq.com
git config --global sendemail.smtpPort 465
git config --global sendemail.smtpUser "your_email@qq.com"
git config --global sendemail.smtpPass "your_app_password"
git config --global sendemail.smtpssl true  # Ensure SSL is enabled
git config --global sendemail.smtpAuth LOGIN  # Use LOGIN method
```
发送邮件（以ffmpeg为例）
```
git send-email --smtp-ssl --to ffmpeg-devel@ffmpeg.org --subject "[PATCH] Fix time_base handling" -1 b438672b11645e1152375beba759a0d2c704e3b1  
```

## git官网

<https://git-scm.com/downloads>