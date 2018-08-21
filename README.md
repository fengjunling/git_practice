# <center>git_practice
##Git命令行操作总结
 文件修改加入暂存区 

	git add <file>
 文件修改提交到分支 
		
	git commit -m '描述信息'
 版本回退
		
	git reset --hard commit_id
	查看提交记录
	git log 
	git log --pretty=oneline 可以简化输出信息
 撤销修改
	
	场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令 git checkout -- file。
	场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令 git reset HEAD <file>，就回到了场景1，第二步按场景1操作。
	场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，使用命令 git reset --hard commit_id，前提是没有推送到远程库。