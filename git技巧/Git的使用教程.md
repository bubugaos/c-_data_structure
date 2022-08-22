# Git的使用教程

![](D:%5CUsers%5C35113%5CDesktop%5C%E6%96%87%E4%BB%B6%E5%A4%B9%5C%E4%BB%A3%E7%A0%81%5Ccode_summary%5Cgit%E6%8A%80%E5%B7%A7%5Cgit%E7%9B%B8%E5%85%B3%E5%9B%BE%E7%89%87%5Cgit%E5%91%BD%E4%BB%A4%E6%9F%A5%E8%AF%A2.png)

## 安装git客户端

```markdown
1. git bash  支持linux命令的git控制台
2. git CMD   支持Windows命令的控制的台
3. git GuI   git的可视化界面
```

## git操作的具体步骤

```markdown
1. cd 路径 进入当前目录
2. 第一次运行：
   1). git config --global user.email "you@example.com"
   2). git config --global user.name "your name"
3. 配置git的基本操作
   【注意】命令：没有消息就是好消息
   1). git clone url 拿到远程仓库的项目
   2). git status 查看状态
   3). git add: 工作区（编辑区）添加到暂存区
   4). git commit -m "备注说明":暂存区提交到分支
   5). git pull origin master:远程仓库拉取到本地
   6). git push origin master: 本地仓库推送到远程
```

```ini
git init                                                  # 初始化本地git仓库（创建新仓库）
git config --global user.name "xxx"                       # 配置用户名
git config --global user.email "xxx@xxx.com"              # 配置邮件
git config --global color.ui true                         # git status等命令自动着色
git config --global color.status auto
git config --global color.diff auto
git config --global color.branch auto
git config --global color.interactive auto
git config --global --unset http.proxy                    # remove  proxy configuration on git
git clone git+ssh://git@192.168.53.168/VT.git             # clone远程仓库
git status                                                # 查看当前版本状态（是否修改）
git add xyz                                               # 添加xyz文件至index
git add .                                                 # 增加当前子目录下所有更改过的文件至index
git commit -m 'xxx'                                       # 提交
git commit --amend -m 'xxx'                               # 合并上一次提交（用于反复修改）
git commit -am 'xxx'                                      # 将add和commit合为一步
git rm xxx                                                # 删除index中的文件
git rm -r *                                               # 递归删除
git log                                                   # 显示提交日志
git log -1                                                # 显示1行日志 -n为n行
git log -5
git log --stat                                            # 显示提交日志及相关变动文件
git log -p -m
git show dfb02e6e4f2f7b573337763e5c0013802e392818         # 显示某个提交的详细内容
git show dfb02                                            # 可只用commitid的前几位
git show HEAD                                             # 显示HEAD提交日志
git show HEAD^                                            # 显示HEAD的父（上一个版本）的提交日志 ^^为上两个版本 ^5为上5个版本
git tag                                                   # 显示已存在的tag
git tag -a v2.0 -m 'xxx'                                  # 增加v2.0的tag
git show v2.0                                             # 显示v2.0的日志及详细内容
git log v2.0                                              # 显示v2.0的日志
git diff                                                  # 显示所有未添加至index的变更
git diff --cached                                         # 显示所有已添加index但还未commit的变更
git diff HEAD^                                            # 比较与上一个版本的差异
git diff HEAD -- ./lib                                    # 比较与HEAD版本lib目录的差异
git diff origin/master..master                            # 比较远程分支master上有本地分支master上没有的
git diff origin/master..master --stat                     # 只显示差异的文件，不显示具体内容
git remote add origin git+ssh://git@192.168.53.168/VT.git # 增加远程定义（用于push/pull/fetch）
git branch                                                # 显示本地分支
git branch --contains 50089                               # 显示包含提交50089的分支
git branch -a                                             # 显示所有分支
git branch -r                                             # 显示所有原创分支
git branch --merged                                       # 显示所有已合并到当前分支的分支
git branch --no-merged                                    # 显示所有未合并到当前分支的分支
git branch -m master master_copy                          # 本地分支改名
git checkout -b master_copy                               # 从当前分支创建新分支master_copy并检出
git checkout -b master master_copy                        # 上面的完整版
git checkout features/performance                         # 检出已存在的features/performance分支
git checkout --track hotfixes/BJVEP933                    # 检出远程分支hotfixes/BJVEP933并创建本地跟踪分支
git checkout v2.0                                         # 检出版本v2.0
git checkout -b devel origin/develop                      # 从远程分支develop创建新本地分支devel并检出
git checkout -- README                                    # 检出head版本的README文件（可用于修改错误回退）
git merge origin/master                                   # 合并远程master分支至当前分支
git cherry-pick ff44785404a8e                             # 合并提交ff44785404a8e的修改
git push origin master                                    # 将当前分支push到远程master分支
git push origin :hotfixes/BJVEP933                        # 删除远程仓库的hotfixes/BJVEP933分支
git push --tags                                           # 把所有tag推送到远程仓库
git fetch                                                 # 获取所有远程分支（不更新本地分支，另需merge）
git fetch --prune                                         # 获取所有原创分支并清除服务器上已删掉的分支
git pull origin master                                    # 获取远程分支master并merge到当前分支
git mv README README2                                     # 重命名文件README为README2
git reset --hard HEAD                                     # 将当前版本重置为HEAD（通常用于merge失败回退）
git rebase
git branch -d hotfixes/BJVEP933                           # 删除分支hotfixes/BJVEP933（本分支修改已合并到其他分支）
git branch -D hotfixes/BJVEP933                           # 强制删除分支hotfixes/BJVEP933
git ls-files                                              # 列出git index包含的文件
git show-branch                                           # 图示当前分支历史
git show-branch --all                                     # 图示所有分支历史
git whatchanged                                           # 显示提交历史对应的文件修改
git revert dfb02e6e4f2f7b573337763e5c0013802e392818       # 撤销提交dfb02e6e4f2f7b573337763e5c0013802e392818
git ls-tree HEAD                                          # 内部命令：显示某个git对象
git rev-parse v2.0                                        # 内部命令：显示某个ref对于的SHA1 HASH
git reflog                                                # 显示所有提交，包括孤立节点
git show HEAD@{5}
git show master@{yesterday}                               # 显示master分支昨天的状态
git log --pretty=format:'%h %s' --graph                   # 图示提交日志
git show HEAD~3
git show -s --pretty=raw 2be7fcb476
git stash                                                 # 暂存当前修改，将所有至为HEAD状态
git stash list                                            # 查看所有暂存
git stash show -p stash@{0}                               # 参考第一次暂存
git stash apply stash@{0}                                 # 应用第一次暂存
git grep "delete from"                                    # 文件中搜索文本“delete from”
git grep -e '#define' --and -e SORT_DIRENT
git gc
git fsck
```

## 详细命令

## 基本配置（配置用户名和邮箱）

```ini
git config --global user.name xxx 
git config --global user.email xxx@qq.com
```

###  创建密钥（生成的密钥默认存放在~/.ssh目录下）

```ini
ssh-keygen -t rsa -C "xxx@qq.com"
```

## 初始化仓库及操作

```ini
git init (初始化一个仓库)
git add [文件名] (添加新的文件)
git commit -m [关于本次提交的相关说明] (提交)
git status (查看文件状态)
git diff   (如果文件改变，比较两个文件内容)
git add[文件名] ||  git commit -a -m [关于本次提交的相关说明] (若文文件改变，将改变的文件放到缓冲区中 || 放到缓冲区并提价)
git log (查看提交说明)
git reset --hard head~[N]  (返回到前N个版本)
git reset --hard [commit id] (回到commit id对应的版本)
git reflog (找不到commit id 时 使用该命令，显示有可能产生commit id的命令对应的commit id)
```

###  撤销修改 

```ini
git checkout --[文件名] （--很重要，没有--，就变成了“切换到另一个分支”的命令）
```

- **说明: 把文件在 工作区 的修改全部撤销，这里有两种情况： **

  **一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态； 一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。 总之，就是让这个文件回到最近一次git commit或git add时的状态**

  ## 删除操作

  ```ini
  git rm [文件名]
  ```

   直接在windows窗口中删除 或者 使用该命令删除都可以，但是这只是工作区删除，还没有在版本库中删除。 

  ###  删除后提交 

  ```ini
  git commit -m [关于本次提交的相关说明] (提交，将版本库中的文件也删除)
  ```

   如果不小心删错了文件，不要怕 

  ```ini
  git checkout --[文件名] （因为版本库里还有，所以可以把误删的文件恢复到最新版本）
  ```

   刷新忽略文件 

  ```ini
  ## git rm -r --cached . (可以用于刷新忽略文件)
  ```

  

## 远程仓库

```ini
git remote add [远程仓库名] [远程仓库地址] 
git remote rm  [远程仓库名] (git remote rm origin   删除远程仓储)
git push -u [远程仓库名] [分支名]  （把本地库的内容推送到远程 git push -u origin master 第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，当然，在以后的推送或者拉取时就可以简化命令了。）
git push [远程仓库名] [分支名]	（从现在起，只要本地作了提交，就可以通过命令：$ git push origin master 提交）
git clone是把整个git项目拷贝下来，包括里面的日志信息，git项目里的分支，你也可以直接切换、使用里面的分支等等
git pull相当于git fetch和git merge。其意思是先从远程下载git项目里的文件，然后将文件与本地的分支进行merge。
git remote -v 查看远程仓储名称
（分支）  
git branch [分支名称]（创建新的分支）
git checkout [分支名称] （切换到不同分支）
git checkout -b [分支名称] （创建并切换到不同的分支）
git branch (查看当前所在的分支)
git merge [分支名称] （合并指定分支到当前分支）
git branch -d [分支名称]  (删除分支)
```

 **添加上游分支** 

```markdown
给fork配置远程库
	使用 git remote -v 查看远程状态
 
	确定一个将被同步给 fork 远程的上游仓库  
	git remote add upstream git [git路径]
 
	再次 git remote -v  查看状态确认是否配置成功。
	同步fork，从上游仓库 fetch 分支和提交点，提交给本地 master，并会被存储在一个本地分支 upstream/master  
	git fetch upstream
 
	切换到本地主分支(如果不在的话)  
	git checkout master
 
	把 upstream/master 分支合并到本地 master 上，这样就完成了同步，并且不会丢掉本地修改的内容。  
	git merge upstream/master
 
	如果想更新到 GitHub 的 fork 上，直接  
	git push origin master 就好了。
```

```ini
查看用户名 ：git config user.name

查看密码： git config user.password

查看邮箱：git config user.email

查看配置信息： git config --list 
```

