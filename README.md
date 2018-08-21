# Git命令行基本操作总结
## 关联远程仓库
添加关联远程仓库

	git remote add origin xxx
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
