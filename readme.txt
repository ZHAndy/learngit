1.	安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！
  	安装完成后，还需要最后一步设置，在命令行输入：

	$ git config --global user.name "Your Name"
	$ git config --global user.email "email@example.com"

2. 	创建版本库
	选择一个合适的地方，创建一个空目录：

	$ mkdir learngit
	$ cd learngit
	$ pwd
	/Users/michael/learngit

	初始化一个Git仓库，使用git init命令。

	添加文件到Git仓库，分两步：

	第一步，使用命令git add <file> <file> <file>，注意，可反复多次使用，添加多个文件；

	第二步，使用命令git commit，完成。

3.	时光机穿梭
	运行git status命令看看结果：
	$ git diff <file>,查看修改内容
	提交修改和提交新文件是一样的两步：
	git add <file>
	git commit -m "注释"
	
	要随时掌握工作区的状态，使用git status命令。
	如果git status告诉你有文件被修改过，用git diff可以查看修改内容。

4.版本回退
	$ git log	查看修改日志
	$ git log --pretty=oneline 查看日志版本
	$ git reset --hard HEAD^ 回退到某一版本
		首先，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交3628164...882e1e0（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。	
	$ cat readme.txt	读取版本内容
	$ git reflog	记录每次命令
		可用版本号读取任何版本

	小结：
	HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。

	穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。

	要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

5.撤销修改
	git checkout -- file可以丢弃工作区的修改：
		$ git checkout -- readme.txt
			--很重要，没有--，就变成了“创建一个新分支”的命令
	用命令git reset HEAD file可以把暂存区的修改撤销掉（unstage），重新放回工作区：
		$ git reset HEAD readme.txt

	小结
	场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
	场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。
	场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

6.删除文件
	一般情况下，你通常直接在文件管理器中把没用的文件删了，或者用rm命令删了：
	$ rm test.txt
	从版本库中删除该文件，那就用命令git rm删掉，并且git commit：
	git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。
	小结
	命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。