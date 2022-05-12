### Git Command

#### User

- git config --global user.name "LiuYutian"
- git config --global user.email "1428456495@qq.com"

- git config user.name
- git config user.password
- git config user.email

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
- git restore files_name            没有使用 add 把文件添加到仓库，可以恢复文件
- git restore --staged files_name   使用 add 把文件添加到仓库，可以推出添加但保留文件变更

- git log                           查看提交的日志文件
- git log --pretty=oneline          显示简略信息

- git reset --hard HEAD^            恢复成上一个版本
- git reset --hard HEAD^^           恢复成上上一个版本
- git reset --hard HEAD~100         恢复成上上 100 个版本
- git reset --hard abeccf4          恢复成 “abeccf4” 的版本
- cat readme.txt                    可以在 git Bash 查看文件内同
- git reflog                        查看每一次提交的 massage 和 SHA1 内容

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