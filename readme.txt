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

7.远程仓库
	在继续阅读后续内容前，请自行注册GitHub账号。由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：

	第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

	$ ssh-keygen -t rsa -C "youremail@example.com"
	你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。

	如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

	第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

	然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：

	最后友情提示，在GitHub上免费托管的Git仓库，任何人都可以看到喔（但只有你自己才能改）。所以，不要把敏感信息放进去。
	如果你不想让别人看到Git库，有两个办法，一个是交点保护费，让GitHub把公开的仓库变成私有的，这样别人就看不见了（不可读更不可写）。另一个办法是自己动手，搭一个Git服务器，因为是你自己的Git服务器，所以别人也是看不见的。这个方法我们后面会讲到的，相当简单，公司内部开发必备。

8.添加远程仓库
	首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库
	
	现在，我们根据GitHub的提示，在本地的learngit仓库下运行命令：
	$ git remote add origin git@github.com:xxxx/yyyyy.git
	xxxx自己的github名称，yyyy为仓库名

	下一步，就可以把本地库的所有内容推送到远程库上：
	$ git push -u origin master	首次时
		由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
	从现在起，只要本地作了提交，就可以通过命令：
	$ git push origin master

	小结
	要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；
	关联后，使用命令git push -u origin master第一次推送master分支的所有内容；
	此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；
	分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，而SVN在没有联网的时候是拒绝干活的！当有网络的时候，再把本地提交推送一下就完成了同步，真是太方便了！

9.从远程库克隆
	首先，登陆GitHub，创建一个新的仓库，名字叫gitskills：
	勾选Initialize this repository with a README，这样GitHub会自动为我们创建一个README.md文件。
	现在，远程库已经准备好了，下一步是用命令git clone克隆一个本地库：
	$ git clone git@github.com:xxxxx/yyyyy.git
	$ cd yyyy
	$ ls

	小结
	要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。
	Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。

10.创建分支并合并
	首先，我们创建dev分支，然后切换到dev分支：
	$ git checkout -b dev
	git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
	$ git branch dev
	$ git checkout dev
	然后，用git branch命令查看当前分支：
	$ git branch
		git branch命令会列出所有分支，当前分支前面会标一个*号。

	然后，我们就可以在dev分支上正常提交，比如对readme.txt做个修改
	然后提交：
	$ git add readme.txt 
	$ git commit -m "branch test"

	现在，dev分支的工作完成，我们就可以切换回master分支：
	$ git checkout master
	现在，我们把dev分支的工作成果合并到master分支上：
	$ git merge dev

	合并完成后，就可以放心地删除dev分支了：
	$ git branch -d dev
	删除后，查看branch，就只剩下master分支了：
	$ git branch

	小结
		Git鼓励大量使用分支：

		查看分支：git branch

		创建分支：git branch <name>

		切换分支：git checkout <name>

		创建+切换分支：git checkout -b <name>

		合并某分支到当前分支：git merge <name>

		删除分支：git branch -d <name>