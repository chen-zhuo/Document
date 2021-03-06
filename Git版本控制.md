# *Git* 版本控制

简单说，[*Git*](https://git-scm.com/) 是一个开源的分布式版本控制系统。

### *Git* 介绍

在电脑上下载 [*Git*](https://git-scm.com/)，安装好以后会出现在点击鼠标右键的菜单栏里面。

![QQ截图20191124002422](image/QQ截图20191124002422.png)

##### *Git* 模式

*Git GUI Here*：图形界面模式

*Git Bash Here*：命令行模式（推荐）

##### *Git* 工作区域

工作区：添加、编辑、修改文件等动作

暂存区：暂存已经修改的文件最后统一提交带 *Git* 仓库中

历史区：最终确定的文件保存到仓库，称为一个新的版本，并且对他人可见

##### *Git* 工作流程

工作区——>暂存区——>历史区——>GitHub 仓库（网络仓库）

##### *Git* 命令

*Git* 当中许多命令和 *Linux* 一样。

```
ls：查看当前文件夹内的文件

pwd：查看当前所在路径

mkdir XXX：当前目录下创建一个XXX文件夹

touch a.XXX：当前目录下生成一个a.XXX文件

vim a.XXX：编辑文件a.XXX
	1.vim是一个编辑器
	2.按i键进入编辑模式
	3.按esc键进入阅读模式
	4.阅读模式下，输入:wq保存编辑并退出，输入:q!不保存编辑并退出

cat a.XXX：查看文件a.XXX的内容

git status：查看状态
	1.红色文件名：表示文件在工作区
	2.绿色文件名：表示文件在暂存区
	3.无文件名：表示所有提交的东西都在历史区

git add test.txt：将test.txt文件从工作区提交到暂存区

git rm 文件名： 同时从工作区和索引中删除文件。即本地的文件也被删除了。

git rm --cached 文件名： 从索引中删除文件。但是本地文件还存在， 只是不希望这个文件被版本控制。

git commit -m "提交描述"：将暂存区的文件提交到Git仓库，并添加提交描述
```

### 仓库管理

##### 配置用户

查看配置

```
# 配置信息
git config -l
# 全局配置信息
git config --global -l
```

设置用户

```
git config --global user.name'chen-zhuo'：设置用户名chen-zhuo

git config --global user.email'972305453@qq.com'：设置用户邮箱
```

##### 新建 *Git* 仓库

新建一个test文件夹

```
mkdir test
```

进入文件夹内初始化为Git仓库

```
cd test
git init

# 注释：执行后，会在该文件夹内生成一个.git文件夹，它是用来存储本地仓库数据信息的
```

##### 添加仓库文件

在仓库内部添加新文件

```
# 方法一：用vim来新建文件
cd spider 
vim 1.txt	# 1.txt不存在时，vim会自动新建；1.txt存在，就编辑文件。按i键，添加内容'first'，按esc键，输入:wq，保存退出

# 方法二：手动来新建文件并添加内容
```

![QQ截图20190420151059](image/QQ截图20190420151059.png)

查看文件状态

```
git status
```

文件名为红色，表明该文件在工作区

![QQ截图20191124171122](image/QQ截图20191124171122.png)

##### 提交仓库文件

将新建文件添加到暂存区

```
# 将当前仓库中最新修改的文件提交到暂存区
git add .
git add -A

# 只将一个文件1.txt提交到暂存区
git add 1.txt
```

提交文件后，查看文件状态，文件名为绿色，表明该文件在暂存区

![QQ截图20191124172235](image/QQ截图20191124172235.png)

将暂存区文件提交到历史区

```
# 将暂存的所有文件提交到历史区
git commit -m '提交内容的描述'

# 查看历史版本信息
git log
git reflog（包括回滚信息）
```

提交文件后，查看文件状态就没有文件显示了，输入命令可以查看提交描述

![QQ截图20191124173618](image/QQ截图20191124173618.png)

##### 连接远程仓库

```
# 查看所有当前连接的远程仓库
git remote -v

# 连接远程仓库
# 连接名称可任意命名，一般为origin，后面加上仓库的地址。
git remote add 连接名称 仓库地址

# 移除远程仓库连接
git remote remove 连接名称

# 修改远程仓库的命名 
git remote rename 连接名称 新连接名称
```

![QQ截图20191124175329](image/QQ截图20191124175329.png)

##### 同步仓库文件

```
# 同步前之前最好先拉取
git pull 连接名称 master

# 如果本地仓库有修改，上面命令可能报错，就可以用这条命令在本地合并两个仓库。
git pull --rebase 连接名称 master

# 上传文件
git push 连接名称 master
```

![QQ截图20191124183146](image/QQ截图20191124183146.png)

*push* 命令需要输入 *GitHub* 用户名和密码

![QQ截图20190420153346](image/QQ截图20190420153346.png)

##### 克隆仓库文件

复制 *GitHub* 仓库地址

![QQ截图20190420150301](image/QQ截图20190420150301.png)

克隆 *GitHub* 仓库到本地

```
git clone 仓库地址
```

![QQ截图20190420150559](image/QQ截图20190420150559.png)

### 分支管理

如果只是一个人使用git管理代码，那么记住上面的命令就够了。但如果是多人协作开发来管理代码，就必须要学习分支管理了。

**分支：从一个系统或主体中分出来的部分，这里讲的分支就是代码的不同版本。**例如，同一套代码，A拷贝后修改了文件file1，这就有了新的A_branch分支，B拷贝后修改了文件file2，这就有了新的B_branch分支。

**在多人协作开发中，一般会有多个分支。**分支的命名通常为：

```
master（主分支）
dev（开发分支）
...（其他分支）
```

!> 注意：无论有多少个分支，都必须有一个主分支，名称通常为master， 连接名称通常为origin。

##### 查看|新建

```
# 查看本地所有分支
git branch
```

前面*号和绿色字体分支代表当前所在的分支，后面的括号也表明了所在的分支。

![QQ截图20210613152026](image/QQ截图20210613152026.png)

```
# 查看全部分支
git branch -a
```

列出所有分支了，其中上方的是本地的分支，下方的有remotes/origin开头的就是远程分支。

![QQ截图20210629152538](image/QQ截图20210629152538.png)

```
# 新建分支
git branch 新建分支名称

# 新建分支并切换到新建分支
git checkout -b 新建分支名称
```

**在分支A中新建分支B，分支B就是分支A的拷贝版。**

![QQ截图20210613143616](image/QQ截图20210613143616.png)

!> 注意：新建分支不可和已有分支重名，否则会报创建分支失败的错误。

##### 切换|提交

```
# 切换分支（如果包含还未提交的工作，切换会失败，可以先提交历史区再切换）
git checkout 要切换到的分支

# 舍弃当前改动强行切换分支（慎用）
git checkout -f 要切换到的分支
```
![QQ截图20210614034659](image/QQ截图20210614034659.png)

现在我们切换到新建的new分支，做出修改后并提交。

```
# 将修改的文件从工作区提交到暂存区
git add .
```
![QQ截图20210614035726](image/QQ截图20210614035726.png)

```
# 将修改的文件从暂存区提交到历史区
git commit -m '提交描述'
```
![QQ截图20210614035849](image/QQ截图20210614035849.png)

```
# 若后面还有追加修改的文件，再次提交
git add .

# 新增修改到历史区需要确认追加的修改，输入“:wq”即可保存退出
git commit --amend
```
![QQ截图20210614041016](image/QQ截图20210614041016.png)

![QQ截图20210614040938](image/QQ截图20210614040938.png)

```
# 提交需要合并分支的请求到线上
git push -f origin 要提交的分支名称
```
![QQ截图20210614041346](image/QQ截图20210614041346.png)

##### 合并|删除

提交分支到后，可以看到线上已经多出一个分支了。

![QQ截图20210614041717](image/QQ截图20210614041717.png)

点击Pull requests，点击 Compare & Pull requests。

![QQ截图20210614041935](image/QQ截图20210614041935.png)

进入页面后，查看是否可以合并，填写合并的请求描述，点击Create pull request。

![QQ截图20210614042404](image/QQ截图20210614042404.png)

默认进入到讨论板块页面，这里可以进行讨论交流：

![QQ截图20210614043043](image/QQ截图20210614043043.png)

提交板块页面可以看到提交的信息：

![QQ截图20210614043454](image/QQ截图20210614043454.png)

检查板块可以检查提交的代码：

![QQ截图20210614044732](image/QQ截图20210614044732.png)

修改板块可以对照修改的内容：

![QQ截图20210614044930](image/QQ截图20210614044930.png)

确认无误后，回到讨论板块，点击 Merge pull request：

![QQ截图20210614045042](image/QQ截图20210614045042.png)

点击 Confirm merge 确认合并。

![QQ截图20210614045159](image/QQ截图20210614045159.png)

确认合并后，点击 Delete branch 可以安全的删除new分支了。

![QQ截图20210614045320](image/QQ截图20210614045320.png)

![QQ截图20210614045449](image/QQ截图20210614045449.png)

回到仓库页会提示合并分支的请求已完成：

![QQ截图20210614045644](image/QQ截图20210614045644.png)

再查看分支也只有master分支了，说明new分支已经成功与master主分支进行了合并。

![QQ截图20210614045540](image/QQ截图20210614045540.png)

假如合并以后，没有在网站上删除new分支，我们还可以通过命令来删除远程的new分支。

```
# 删除远程分支，但本地的同名分支还在
git push origin --delete 要删除的远程分支名称
```
确认远程的new分支删除以后，这下可以删除我们本地的new分支了。

**删除的分支不能是当前分支**：即不能在new分支里面删除new分支，只能切换到其他分支中再删除new分支。

```
# 删除分支（如果包含了还未合并的工作或没有对应的远程分支会失败）
git branch -d 要删除的分支名称

# 强行删除分支（删除分支并丢掉未提交的内容）
git branch -D 要删除的分支名称
```

![QQ截图20210614052247](image/QQ截图20210614052247.png)

##### 拉取|改名

拉取分支和前面的同步仓库文件一样，上面操作中，我们新建了一个new分支后面所有的改动都是再new分支中进行，所以本地new分支的更新程度要高于本地master，后面new分支推到线上去了和master分支进行了合并，线上master分支就有了最新的改动，本地的master分支还是以前的更新，这种情况就需要拉取分支，来同步一下线上的master分支。

```
# 拉取线上分支
$ git pull --rebase origin 要拉取的线上分支名称

# 若本地分支有改动，需要先提交到历史区，否则会拉取失败
error: cannot pull with rebase: You have unstaged changes.
```
这里成功拉取了线上的master分支，将前面在本地new分支中的修改更新到了本地的master分支中。

![QQ截图20210614053751](image/QQ截图20210614053751.png)

有时候我们需要修改分支的额名称，就可以使用下面命令进行修改：

```
# 分支改名（将master改名为new_master）
git branch -m master new_master
```
![QQ截图20210616004424](image/QQ截图20210616004424.png)

### 进阶操作

##### 选择忽略

在使用git时，默认会将下面所有文件都纳入管理，但有些文件是无需纳入的管理，也不希望它们出现在未跟踪文件列表，例如：日志文件、临时文件、编译产生的中间文件、工具自动生成的文件等等。此时我们可以创建一个名为 `.gitignore` 的文件，列出要忽略的文件模式，git会根据这些模式规则来判断是否将文件添加到版本控制中。

格式规范：

```
1.所有空行或者以注释符号#开头的行都会被 Git 忽略
2.可以使用标准的glob模式匹配
3.匹配模式最后跟斜杠/说明要忽略的是目录
4.要忽略指定模式以外的文件或目录，可以在模式前加上感叹号(!)进行取反
```

所谓的 glob 模式是指 shell 所使用的简化了的正则表达式，匹配规则如下：

```
"*"：星号匹配零个或多个任意字符
[]：匹配任何一个列在方括号中的字符，如[ab]匹配a或者匹配b
"?"：问号匹配一个任意字符
[n-m]：匹配所有在这两个字符范围内的字符，如[0-9]表示匹配所有0到9的数字

示例：
logs/：忽略当前路径下的logs目录，包含logs下的所有子目录和文件
/logs.txt：忽略根目录下的logs.txt文件
*.class：忽略所有后缀为.class的文件
!/classes/a.class：不忽略classes目录下的a.class文件
tmp/*.txt：只忽略tmp目录下的.txt文件
**/foo：可以忽略/foo, a/foo, a/b/foo等
```

除了可以在项目中定义 `.gitignore` 文件外，还可以设置全局的`.gitignore`文件来管理所有Git项目的行为。这种方式在不同的项目开发者之间是不共享的，是属于项目之上Git应用级别的行为。可以在任意目录下创建相应的`.gitignore`文件，然后再使用以下命令配置Git：

```
git config --global core.excludesfile ~/.gitignore
```

`.gitignore` 只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改`.gitignore`是无效的。所以一定要养成在项目开始就创建 `.gitignore` 文件的习惯。解决方法就是先把本地缓存删除(改变成未track状态)，然后再提交：

```
git rm -r --cached .
git add .
git commit -m "msg"
```
Python项目 `.gitignore` 文件示例：

```
venv
.idea
*.pyc
__pycache__

### VisualStudioCode ###
.vscode/*
.vscode/**
!.vscode/settings.json
!.vscode/tasks.json
!.vscode/launch.json
!.vscode/extensions.json

### VisualStudioCode Patch ###
# Ignore all local history of files
.history
```
##### 身份认证

每一次更新远程库需要进行登录，就显得很繁琐，我们就需要 *SSH Key* 来进行身份认证，不必每次登录。

创建 *SSH Key*

```
# 输入该命令，一路回车，生成公钥和密钥文件
ssh-keygen -t rsa -C "账号@qq.com"
```

![QQ截图20191124152143](image/QQ截图20191124152143.png)

找到文件生成的地方，当中有两个文件个就是 *SSH Key* 的秘钥对，*id_rsa* 是私钥，不能泄露出去，*id_rsa.pub* 是公钥，可以放心地告诉任何⼈。

![QQ截图20191124152629](image/QQ截图20191124152629.png)

用记事本格式打开 *id_rsa.pub* 并复制其中的内容

![QQ截图20191124153021](image/QQ截图20191124153021.png)

打开并登录 *GitHub* 网站在 *settings* 中新增 *New SSH key*

![QQ截图20191124153223](image/QQ截图20191124153223.png)

将复制的内容粘贴其中，并添加上标题，点击 *Add SSH key*，网站上的账户就成功添加了公钥。

![QQ截图20191124153443](image/QQ截图20191124153443.png)

![QQ截图20191124153824](image/QQ截图20191124153824.png)

输入命令尝试 *SSH* 连接，就成功连接上了。

```
ssh -T git@github.com
```

![QQ截图20191124185041](image/QQ截图20191124185041.png)

这个时候我们上传文件就不使用远程仓库的地址，我们就使用远程仓库的 *SSH*

![QQ截图20191124155441](image/QQ截图20191124155441.png)

![QQ截图20191124155513](image/QQ截图20191124155513.png)

将远程仓库的 *SSH* 添加到连接列表中

![QQ截图20191124190156](image/QQ截图20191124190156.png)

上传文件我们就通过 *SSH* 来传递文件，就不用输入密码了。

![QQ截图20191124190748](image/QQ截图20191124190748.png)

?> *GitHub* 允许你添加多个 *Key*。假定你有若干电脑，你⼀会儿在公司提交，⼀会儿在家里提交，只要把每台电脑的 *Key* 都添加到 *GitHub*，就可以在每台电脑上往 *GitHub* 推送 了。

?> *Git* 的克隆仓库可以直接使用远程仓库的 *SSH* 地址。

?> 更新新建的仓库最好先将仓库克隆到本地再更新，有 *SSH* 到时候更新完成，直接 *git push* 就好啦。

