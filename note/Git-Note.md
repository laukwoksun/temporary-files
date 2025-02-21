### Git安装基本信息设置

- 下载安装
- 设置用户名
	-`git  config -- global  user.name  "你在github上注册的用户名"`
- 设置用户邮箱
	-`git  config -- global  user.email  ”注册时候的邮箱“`
- 如下命令来看看是否配置成功
	-`git config --list`

注意：git  config --global 参数，有了这个参数表示你这台机器上所有的git仓库都会使用这个配置，当然你也可以对某个仓库指定不同的用户名和邮箱

### Git远程仓库
https://www.runoob.com/w3cnote/git-guide.html

##### 设置

由于本地 Git 仓库和 GitHub 仓库之间的传输是通过SSH加密的，所以我们需要配置验证信息：

- 使用以下命令生成 SSH Key：
```
ssh-keygen -t rsa -C "xkouliu@qq.com"
```

" "内改为 Github 上注册的邮箱，之后会要求确认路径和输入密码，使用默认的一路回车就行。

成功的话会在 **~/** 下生成 **.ssh** 文件夹，进去，打开 **id_rsa.pub**，复制里面的 **key**

回到 github 上，进入 Account => Settings（账户配置）选择 **SSH and GPG keys**，然后点击 **New SSH key** 按钮,title 设置标题，可以随便填，粘贴在你电脑上生成的 key

- 为了验证是否成功，输入以下命令：

	`ssh -T git@github.com`

##### 使用

###### 创建
- 要添加一个新的远程仓库，可以指定一个简单的名字，以便将来引用,命令格式如下：
	`git remote add [shortname] [url]   
	`git remote add origin git@github.com:laukwoksun/note.git`
	
- 加完之后进入.git，打开config，这里会多出一个remote "origin"内容，这就是刚才添加的远程地址，也可以直接修改config来配置远程地址。

- 创建新文件夹，打开，然后执行 `git init` 以创建新的 git 仓库。


> [!NOTE] git remote add [shortname] [url]   
> 这个添加新的远程仓库是指本地，推送上Git/Gitee的前提是上面已经存在这个仓库

> [!NOTE] 添加新的远程仓库方法
> 方法 1: 在GitHub上手动创建仓库
> 
方法 2: 使用GitHub CLI (gh)
GitHub提供了命令行工具gh，可以让你直接从终端创建新的GitHub仓库：
1.安装GitHub CLI：
2.登录GitHub CLI
`gh auth login`
3.创建新仓库
`gh repo create  <> --source=. --remote=origin`
这条命令会在当前目录下创建一个新的GitHub仓库，并将其设置为本地仓库的远程仓库。
> 
方法 3: 使用 hub 工具
hub 是一个Git的命令行扩展，它简化了与GitHub交互的过程。你可以使用hub来创建新仓库：
安装hub：根据官方文档中的说明安装hub。
创建新仓库：
`hub create <>`
这会创建一个新的GitHub仓库，并自动配置远程仓库URL。


###### 检出仓库
- 执行如下命令以创建一个本地仓库的克隆版本：
	`git clone /path/to/repository` 
- 如果是远端服务器上的仓库，你的命令会是这个样子：
	`git clone username@host:/path/to/repository`

###### 工作流
```
本地文件夹 --->  暂存区  --->  远端仓库
```

- 提出更改（把它们添加到暂存区），使用如下命令：  
	`git add <filename>`  
	`git add *`
	`git add .`
- 使用如下命令以实际提交改动：  
	`git commit -m "代码提交信息"`
- 执行如下命令以将这些改动提交到远端仓库（可以把 _master_ 换成你想要推送的任何分支）：  
	`git push origin master`  
- 如果你还没有克隆现有仓库，并欲将你的仓库连接到某个远程服务器，你可以使用如下命令添加：  
	`git remote add origin <server>`
###### 分支
- 创建一个叫做"feature_x"的分支，并切换过去：  
	`git checkout -b feature_x`  
- 切换回主分支：  
	`git checkout master`  
- 再把新建的分支删掉：  
	`git branch -d feature_x`  
- 除非你将分支推送到远端仓库，不然该分支就是 _不为他人所见的_：  
	`git push origin <branch>`
###### 更新与合并
- 要更新你的本地仓库至最新改动，执行：  
	`git pull`  
  
- 要合并其他分支到你的当前分支（例如 master），执行：  
	`git merge <branch>`  

- 在这两种情况下，git 都会尝试去自动合并改动。遗憾的是，这可能并非每次都成功，并可能出现_冲突（conflicts）_。 这时候就需要你修改这些文件来手动合并这些_冲突（conflicts）_。改完之后，你需要执行如下命令以将它们标记为合并成功：  
	`git add <filename>`  
- 在合并改动之前，你可以使用如下命令预览差异：  
	`git diff <source_branch> <target_branch>`
###### 替换本地改动

- 假如你操作失误（当然，这最好永远不要发生），你可以使用如下命令替换掉本地改动：  
	`git checkout -- <filename>`  
- 此命令会使用 HEAD 中的最新内容替换掉你的工作目录中的文件。已添加到暂存区的改动以及新文件都不会受到影响。

- 假如你想丢弃你在本地的所有改动与提交，可以到服务器上获取最新的版本历史，并将你本地主分支指向它：  
	`git fetch origin`  
	`git reset --hard origin/master`

###### 实用小贴士

- 内建的图形化 git：  
	`gitk`  
- 彩色的 git 输出：  
	`git config color.ui true`  
- 显示历史记录时，每个提交的信息只显示一行：  
	`git config format.pretty oneline`  
- 交互式添加文件到暂存区：  
	`git add -i`




##### 命令

###### 提交更改并推送
- 当你在本地做了更改并提交后，可以通过push命令将更改推送到GitHub：
```
# 添加所有更改到暂存区
git add .

# 提交更改
git commit -m "Your commit message"

# 推送更改到GitHub的默认分支（通常是main或master）
git push origin main
```

###### 拉取最新更改
- 为了保持本地仓库与远程仓库同步，定期从远程仓库拉取最新的更改是很有必要的：
```
# 更新本地仓库以包含远程仓库的所有更改
git pull origin main

# 使用checkout
git checkout master -- <filename / .>

//实测未成功
# 确保你处于正确的分支上（例如main）
git checkout main
# 拉取最新的更改
git pull origin main

# 使用restore
git restore <file-path / directory-path>
# 将工作目录重置为最近一次提交的状态
git reset --hard HEAD

```

###### 处理合并冲突
- 在多人协作开发时，可能会遇到合并冲突。这时你需要手动解决冲突，然后再次提交更改：
```
# 解决冲突后，添加更改并提交
git add .
git commit -m "Resolved merge conflicts"
```

###### 创建和切换分支
- 在进行新功能开发或修复bug时，最好创建一个新的分支来隔离工作：
```
# 创建并切换到新分支
git checkout -b feature-branch-name

# 完成工作后，切换回主分支并合并新分支
git checkout main
git merge feature-branch-name
```

###### 删除本地和远程分支
- 完成工作后，你可以删除不再需要的分支：
```
# 删除本地分支
git branch -d feature-branch-name

# 删除远程分支
git push origin --delete feature-branch-name
```

###### 暂存区撤销
暂存区（即使用git add命令），但之后又决定不想提交这些更改时，你可以通过不同的Git命令来撤销暂存区中的更改

- 撤销单个文件的暂存
```
# 使用 git restore (推荐)
git restore --staged <file-path>

# 或者使用 git reset
git reset <file-path>
```

- 撤销所有文件的暂存
```
# 使用 git restore (推荐)
git restore --staged .

# 或者使用 git reset
git reset
```

- 恢复工作目录和暂存区到最近一次提交的状态
```
# 恢复工作目录和暂存区到最近一次提交的状态
git restore --source=HEAD --staged .

# 警告：这将丢失所有未提交的更改
git reset --hard HEAD
```

- 恢复到特定提交的状态
```
# 切换到特定分支或提交
git switch -c temp-branch <commit-hash>

# 或者只是查看而不切换分支
git checkout <commit-hash> -- <file-path>

# 然后使用 git restore 将更改应用到当前分支
git restore --source=<commit-hash> <file-path>
```



   ##### 常用命令
######  `git init  #初始化`
######  `git remote add [shortname] [url]  #添加仓库`
######  `git clone   #克隆`
######  `git status  #状态`
######  `git add .  #增加暂存区`
######  `git commit -m ''  #提交暂存区`
######  `git push origin master  #提交分支`
######  `git pull origin master  #拉取分支`
#####   `type nul > .gitignore #本地新建一个.ignore文件(windows)`
   
##### 常见报错
###### 端口被屏蔽：ssh: connect to host github.com port 22: Connection timed out
1. 终端输入ssh -T -p 443 git@ssh.github.com
`#返回结果：Hi xxx! You've successfully authenticated,but Github ode not provide shell access.`
2. C盘->用户->用户名文件夹->.ssh下，创建或编辑conifg文件，内容为：
```
Host github.com
    Hostname ssh.github.com
    Port 443
```
###### 换行符转换：LF will be replaced by CRLF the next time Git touches it
```
git config --global core.autocrlf input
```
