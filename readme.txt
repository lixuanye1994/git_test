how to use git

#----------------
添加文件到Git仓库，分两步：

$ git add <file>                //注意，可反复多次使用，添加多个文件。实际上就是把文件修改添加到暂存区
$ git commit -m <message>       //添加文件后需要解释 实际上就是把暂存区的所有内容提交到当前分支。
----------------#

#----------------
版本回退：

$ git log                       //查看提交历史，以便确定要回退到哪个版本
$ git reset --hard HEAD^        //回退上一个版本
$ git reset --hard HEAD abcde   //回退到 abced的版本
$ git reflog                    //要重返未来，用查看命令历史，以便确定要回到未来的哪个版本
----------------#

#----------------
git 工作区详解：

第一次修改 -> git add -> 第二次修改  -> git commit   使用 git status 发现只有第一次的修改提交
	--那怎么提交第二次修改呢？
	1.继续git add再git commit
	2.也可以别着急提交第一次修改，先git add第二次修改，再git commit，就相当于把两次修改合并后一块提交了：
		第一次修改 -> git add -> 第二次修改 -> git add -> git commit
每次修改，如果不用git add到暂存区，那就不会加入到commit中。
$ git diff HEAD -- readme.txt   //查看工作区和版本库里最新文件有什么区别。
----------------#

#----------------
撤销修改：

$ git checkout -- readme.txt    //把readme.txt文件在工作区的修改全部撤销.命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令
$ git reset HEAD <file>         //把暂存区的修改撤销掉（unstage），重新放回工作区
----------------#

#----------------
删除文件：

$ rm test.txt                   //删除文件
现在你有两个选择
	1.是确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit提交删除理由 
	2.删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本
	 $ git checkout -- test.txt
