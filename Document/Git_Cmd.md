### Git Command

#### User

- git config --global user.name "LiuYutian"
- git config --global user.email "1428456495@qq.com"

- git config user.name
- git config user.password
- git config user.email

- git config --list                 查看配置的一些参数

#### Command

- mkdir learngit                    创建路径
- cd learngit                       切换目录
- cd ..                             回到上一层目录
- pwd                               显示当前目录
- ls -ah                            查看隐藏文件
- ls -a                             查看隐藏文件
- ls                                查看文件

- git init                          创建仓库
- rm -rf .git                       删除 Git 仓库
- git add file2.txt file3.txt       添加文件到仓库
- git commit -m "add 3 files."      提交文件保存
- git status                        获得当前 git 的状态
- git diff file_name                查看修改内容

- git log                           查看提交的日志文件
- git log --pretty=oneline          显示简略信息

- git reset --hard HEAD^            恢复成上一个版本
- git reset --hard HEAD^^           恢复成上上一个版本
- git reset --hard HEAD~100         恢复成上上 100 个版本
- git reset --hard abeccf4          恢复成 “abeccf4” 的版本
- cat readme.txt                    可以在 git Bash 查看文件内同
- git reflog                        查看每一次提交的 massage 和 SHA1 内容

- git restore file_name             没有使用 add 把文件添加到仓库，可以恢复文件
- git restore --staged file_name    使用 add 把文件添加到仓库，可以推出添加但保留文件变更

- git rm file_name                  删除文件
- git restore file_name             恢复文件
- git restore --staged file_name    恢复 add 后的文件

创建 GitHub 账户：
user: 1428456495@qq.com
pass: Yutian641010Liu

- ssh-keygen -t rsa -C "youremail@example.com"         创建SSH Key
- .SSH 在用户主目录: C:\Users\LiuYutian\.ssh
- Git支持SSH协议
- 把每台电脑的SSH Key都添加到GitHub，就可以在每台电脑上往GitHub推送 push 了,否则无法 push
- 在 GitHub 上免费托管的Git仓库，任何人都可以看到，但是不能改

GitHub 创建存储库（Repository）：learngit
- 关联本地仓库和 GitHub 仓库，
  - 使用 https 协议关联: git remote add origin http://github.com/LIUYUTIANABC/learngit.git
  - 使用SSH协议关联: git remote add origin git@github.com:LIUYUTIANABC/learngit.git
- 远程库的名字：origin（默认）

- 把本地库所有内容推送到远程库： git push -u origin master
- 注意： 第一次提交远程库，需要 git 授权给 GitHub 之后提交就没有了
- 第一次提交用 '-u' 的作用是把本地 master 和远程的 master 关联起来，以后推送或者拉取是可以简化命令
- 简化的命令： git push origin master

- git remote                查看远程库
- git remote -v             查看远程库信息
- git remote rm origin      删除远程库，实际上是解除本地和远程的绑定关系
  - GitHub 上的远程库本身并没有任何改动，要真正删除需要登录Github页面删除按钮删除
  - origin 是远程库的名字，origin是习惯命名

- 从零开发，最好的方式是先创建远程库，然后再克隆
- git clone git@github.com:LIUYUTIANABC/gitskills.git    使用SSH 协议和 GitHub 通信
  - git clone https://github.com/LIUYUTIANABC/gitskills.git    使用https 协议和 GitHub 通信

##### 分支管理————重点

git 支持多分支， 功能强大， 速度快， 实际上就是相当于多添加了一个指针

创建与合并分支

- git checkout -b dev             创建 dev 分支，然后切换到 dev 分支
  - git checkout 的 '-b' 参数表示创建并切换
  - git branch dev                单独创建分支
  - git checkout dev              单独切换到 dev 分支
  - git switch -c dev             创建分支并切换的另一种写法
  - git switch master             单独切换分支的令一种写法
- git branch                      查看当前所有的分支
- git merge drv                   把 dev 分支合并到 master
  - 提示信息 Fast-forward          表示是快速模式，直接改变 master 指针，不会检查冲突
- git branch -d dev               删除分支

解决冲突

- git switch -c feature1          创建分支
- git add -- git commit           提交修改
- git switch master               切换回主分支
- git add -- git commit           提交冲突的修改
- git merge feature1              合并出现冲突，手动解决，保存文件
- git add -- git commit           再次提交修改后的文件
- 这样就把其他分支，合并到了主分支，但其他分支的内容依旧不变
- git log --graph                 查看分支合并情况，详细信息
- git log --graph --pretty=oneline --abbrev-commit        查看分支合并，缩略版的，含主要信息
- git branch -d feature1          删除 feature1 分支
- 因为主干合并后，分支的内容依旧没有改变，如果以后再开发，需要重新生成分支
- 这个分支内容已经不和主干一致了

分支策略管理

Git 用 Fast forward 模式，删除分支后，会丢掉分支信息
禁用 Fast forward 模式，使用普通模式合并
普通模式：git 会在 merge 时生成一个新的 commit 这样就会保存分支历史，看得到分支信息

- git merge --no-ff -m "merge with no-ff" dev        禁用 Fast forward， 可以看到分支信息

> 分支管理：
> 首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
> 那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，
> 比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；

Bug 分支

在工作用正在添加一些功能，有个需要优先处理的 Bug, 可以使用 stash 来存储现在的工作区，恢复之前状态，等修改完 Bug 合并之后，再恢复现在的工作区。

- 前提：在现在的分支（dev）中有添加或修改文件，已经 add，但没有commit
- git stash             保存当前的工作区
- 回到 master 分支，创建 Bug 分支，修改 Bug， 正常提交之后，merge 到主分支，完成修改，删除 Bug 分支 issue-101
- 回到之前的 dev 分支，git switch dev
- git stash list        查看保存的工作区
- git stash apply stash@{0}       恢复之前的工作区，但是stash 内容还在
- git stash drop stash@{0}        删除 stash 工作区
- git stash pop         恢复的同时删除

怎么把 master 分支中，修改的 Bug 也添加到现在的 dev分支中

- 手动修改，再一次提交，可以完成
- 使用 cherry-pick 命令复制一个特定的提交
  - 在 dev 分支中使用
  - git cherry-pick 2e846d5          复制在 master 修改 bug 后的代码
  - 注意： 这里的 commit 是 master 提交的那个 SHA 值， 不是 merge 的那个 SHA 值

Feature 分支

- 真正的开发项目中，每添加一个新功能，最好重新建一个 feature 分支，完成后，合并，再删除 feature 分支
- git switch -c feature-vulcan            创建一个分支
- 修改，添加，提交，回到 dev 分支合并
- git branch -d feature-vulcan            删除分支失败，因为还没有合并
- git branch -D feature-vulcan            强制删除

多人协作

在自己的电脑创建 master 和 dev 分支，通过 push 推送到 GitHub 然后，另外一台电脑（需要添加SSH Key）或者另一个目录通过 clone 命令，克隆远程库

- 另一台电脑：
  - 此时，他的目录下只能看到 master 分支，看不到 dev 分支
  - git checkout -b dev origin/dev            创建远程 origin 的 dev 分支到本地
  - 此时，git branch 查看分支，就有 dev 分支了，就可以在 dev 分支上进行修改，提交
  - 通过 git push origin dev                  推送 dev 分支的修改
- 我的电脑，做了修改后：
  - git push origin dev    试图推送，但是失败，因为，远程的版本库有更新版本
  - 此时用 git pull                            把远程库的最新内容拉区下来
    - 如果可以拉取，说明本地 dev 和远程 origin/dev 是有连接的
    - 如果拉取失败，使用    git branch --set-upstream-to=origin/dev dev     链接本地 dev 分支和远程 origin/dev 分支
  - 合并冲突，git push origin dev           推送我的修改

#### Note

- git add 后面增加的文件用空格分开
- git commit 如果有文件被修改了，也需要使用 add 命令之后才能提交到仓库
- git reset 恢复上一个版本后，使用 git log 已经无法查看之前更新的版本了
  - 要使用 git reflog 查看所有提交的版本 SHA1 的值
- 要使用 git reset 必须提交版本库中所有修改的文件，否则恢复之后，修改内容丢失

- 工作区和暂存区： git add 把文件存储到暂存区;  git commit 把暂存区文件提交到 master 分支中
- git 管理的是修改：
  - 如果执行，第一次修改 -> git add -> 第二次修改 -> git commit
  - 使用 git status 查看发现，第二次修改不会提交
  - 正确方法： 第一次修改 -> git add -> 第二次修改 -> git add -> git commit

- 删除文件：
  - 使用 git rm 删除文件；恢复使用 git restore；确实删除使用 git commit
  - 先手动删除文件，然后使用git rm <file>和git add<file>效果是一样的。

### Linux Command

- git  用的是 Linux 的命令， 所以  git bash 可以使用  Linux  命令

- mkdir learngit            创建路径
- touch file_name           创建一个新的文件
- code file_name            使用 code 打开
- rm -f file_name           删除文件
- rm -rf files_name         删除文件夹
- clear                     清空窗口

### Windows Command

- mkdir wikihow             创建路径
- cd wikihow                切换目录
- dir                       查看路径内容
- cls                       清空窗口
- NUL> aa                   创建新文件
- del aa                    删除文件
- cd..                      回到上一层目录
- rmdir name                删除空白目录
- rmdir /s wikihow          删除目录和文件

### Github 加速

#### 参考网址

- 知乎： https://zhuanlan.zhihu.com/p/75994966
        https://zhuanlan.zhihu.com/p/403089781

- GitHub520： https://gitee.com/inChoong/GitHub520

- 1、获取GitHub官方CDN地址

> - 查看 IP 地址：https://ipaddress.com/
>
> - GitHub.com    IP地址：140.82.113.4
> - assets-cdn.github.com    IP地址：185.199.111.153
> - github.global.ssl.fastly.net    IP地址：199.232.69.194
>
> 140.82.113.3    github.com
> 185.199.108.153 assets-cdn.github.com
> 199.232.69.194  github.global.ssl.fastly.net

- 2、修改系统Hosts文件

> - 接着,打开系统hosts文件(需管理员权限)。
> - 路径：C:\Windows\System32\drivers\etc
> - 使用 code 打开编辑会提示使用管理员权限
> - 并在末尾添加三行记录并保存。(需管理员权限，注意IP地址与域名间需留有空格)

- 3、刷新系统DNS缓存

> - 最后,Windows+X 打开系统命令行（管理员身份）或powershell
> - 运行 ipconfig /flushdns 手动刷新系统DNS缓存。
