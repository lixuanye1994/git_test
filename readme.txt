how to use git 
https://www.bilibili.com/video/BV1VK4y1e7zE

初次使用：
git config --global user.name 'xxxxx'
git config --global user.email 'xxxxx@xxx.com'

生成 ssh 公钥：
$ ssh-keygen                       // 三次回车 生成一对密钥
$ cd /c/Users/6364/.ssh/      // 到密钥目录下
$ code id_rsa.pub                // 打开公钥 粘贴到github
#----------------
添加文件到Git仓库，分两步：

$ git add <file>                //注意，可反复多次使用，添加多个文件。实际上就是把文件修改添加到暂存区
$ git add .                        // 添加当前目录全部内容 ，常用指令

$ git commit -m <message>       //添加文件后需要解释 实际上就是把暂存区的所有内容提交到当前分支。
----------------#


#----------------
版本回退：

$ git log                       //查看提交历史，以便确定要回退到哪个版本
$ git reset --hard HEAD^        //回退上一个版本
$ git reset --hard HEAD abcde   //回退到 abced（abced是每次版本的哈希值）的版本
$ git reflog                    //要重返未来，用查看命令历史，以便确定要回到未来的哪个版本
----------------#

#----------------
git 工作区详解：

第一次修改 -> git add -> 第二次修改  -> git commit   使用 git status 发现只有第一次的修改提交
	--那怎么提交第二次修改呢？
	1.继续git add再git commit
	2.也可以别着急提交第一次修改，先第二次修改再 git add，再git commit，就相当于把两次修改合并后一块提交了：
		第一次修改 -> git add -> 第二次修改 -> git add -> git commit
每次修改，如果不用git add到暂存区，那就不会加入到commit中。
$ git diff HEAD -- readme.txt   //查看工作区和版本库里最新文件有什么区别。

$ git status   //多用用，查看状态，可以看当前是什么分支，当前分支有没有提交的代码等等
----------------#

#----------------
撤销修改：

$ git checkout -- readme.txt    //把readme.txt文件在工作区的修改全部撤销.命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令
$ git reset HEAD <file>           //把暂存区的修改撤销掉，重新放回工作区unstage
----------------#

#----------------
删除文件：

$ rm test.txt                   //删除文件
现在你有两个选择
	1.是确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit提交删除理由 
	2.删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本
	 $ git checkout -- test.txt
----------------#

#----------------

从零上传github前操作：

 //  本地操作
1. git init     // 初始化，生成本地仓库
2. .gitignore  // 设置禁止追踪文件
3. git add . //把所有文件添加追踪
     // 有错误追踪的可以  git rm --cached <xxx> （所有文件就用.操作）

4. git commit -m '提交理由'   //提交代码到本地库
5.  git status   //  看一下状态
6. git log      // 查看日志
7.  git diff  // 查看修改文件的变化
8.  提交的文件修改后 又要提交 可以偷懒跳过git add  ->  git commit -am '又修改了一次'
9.  git checkout -- xxx或者.  // 恢复到上一次状态,前提要先是被追踪
    //  如果是已经git add的文件需要恢复上一次状态，使用 git reset HEAD xxxxx 回退到add之前的状态 
    //  此时就可以还原文件内容 使用git checkout -- xxx
----------------#




#----------------
上传github：    
本地commit后，使用push提交

//  push 推送 
$ git remote add origin https://github.com/lixuanye1994/git_test.git       //上传版本到github库
$ git remote add origin https://github.com/lixuanye1994/git_test.git git_test2   //另存为一个名字
$ git push -u origin master                                              //把本地master分支的最新修改推送至GitHub  -u 记录了push到远端分支的默认值
----------------#

#----------------
下载github：

$ git clone https://github.com/lixuanye1994/python.git                //下载github库
----------------#

拉取github:     // pull 拉取
$ git pull 