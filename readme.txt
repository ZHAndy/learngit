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