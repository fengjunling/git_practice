# Git命令行基本操作总结
## 关联远程仓库
添加关联远程仓库

	git remote add <origin> xxx
查看关联远程仓库地址

	git remote -v
更改关联远程仓库地址

	方法一 通过命令直接修改远程地址
	git remote set-url origin xxx
	方法二 通过命令先删除旧地址再添加远程仓库
	1. git remote rm origin
	2. git remote add origin xxx
## 提交与撤销修改
文件修改加入暂存区 

	git add <file>
	添加所有文件
	git add --a
文件修改提交到分支 
		
	git commit -m '描述信息'
查看修改内容
		
	git diff <file>
版本回退
		
	git reset --hard commit_id
	查看提交记录
	git log 
	git log --pretty=oneline 可以简化输出信息
撤销修改
	
	场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令 git checkout -- file。
	场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令 git reset HEAD <file>，就回到了场景1，第二步按场景1操作。
	场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，使用命令 git reset --hard commit_id，前提是没有推送到远程库。
## 分支管理
创建与合并分支

	创建分支
	git branch <name>
	切换分支
	git checkout <name>
	创建并切换
	git checkout -b <name>
	从远程分支创建并切换
	git checkout -b <name> origin/<branch>
	查看全部分支
	git branch  （分支前有 * 代表当前所在分支）
	同步远程服务器数据到本地
	git fetch origin
	合并指定分支到当前分支
	git merge <origin>/<name>
	注: 1.合并过程中可能会遇到冲突，需要手动解决冲突，即修改文件内容然后再add->commit
	    2.git使用<<<<<<,======,>>>>>>标记不同分支的内容
	删除分支
	git branch -d <name>
拉取与推送分支

	拉取分支
	git pull <远程主机名> <远程分支>:<本地分支>
	or
	git pull <远程主机名> <远程分支名> -->远程分支默认与当前分支合并
	pull 相当于 fetch + merge 两次操作的合并
	推送分支
	git push <远程主机名> <本地分支>:<远程分支>
	or
	git push <远程主机名> <本地分支名> -->将本地分支推送与之存在"追踪关系"的远程分支（通常两者同名）若该远程分支不存在，则会被新建
	
	删除远程分支
	git push <远程主机名> :<远程分支>
	跟踪远程分支
	git branch --set-upstream-to=<远程主机名>/<远程分支> <本地分支>
	查看本地分支所跟踪的远程分支
	git branch -vv
	
## 小结
如果是在本地初始化仓库，然后与github仓库进行关联，这时本地分支不会与远程分支建立联系，拉取和推送操作若想要省略主机与分支名，需要为其建立跟踪分支,如果是从远程仓库克隆，本地分支默认与远程主机的同名分支，建立追踪关系，即本地的master分支自动"追踪"origin/master分支，可以直接使用git pull 和git push 操作。<br>
在本地初始化仓库，关联到Github上新建的仓库，第一次执行git pull origin master 拉取远程分支时，可能会出现fatal:refusing to merge unrelated histories（Git 2.9之后的版本才会出现此问题），在git pull origin master 后面跟上参数 --allow-unrelated-histories 可解决<br>原因参见[Git 2.9 Release Notes](https://github.com/git/git/blob/master/Documentation/RelNotes/2.9.0.txt#L58-L68) 