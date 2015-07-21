# Git 的使用  7/6/2015 5:31:00 PM 
## 学习地址
*  掌握Git的教程 , [Git community book 中文版](http://gitbook.liuhui998.com/index.html)
*  廖雪峰Git教材 , [廖雪峰大神Git讲解](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137396287703354d8c6c01c904c7d9ff056ae23da865a000) 
*  Git 初体验   [Git 初体验](http://www.cnblogs.com/BeginMan/p/3543240.html)
*  csdn博客  [版本控制](http://blog.csdn.net/hudashi/article/category/1122124)
*  高富帅玩Git [高富帅玩 git](http://mux.alimama.com/posts/711)

##1. 下载安装, 见  [Git 有mac安装方式](http://www.cocoachina.com/bbs/read.php?tid=200557)


##2. 安装的配置
	想在哪个目录初始化仓库前使用命令初始化(生成.git):
			git init
			
	git --global user.name "username"  注：1.7以上貌似需要git config --XXX
	git --global user.email "email"
	git --global core.autocrlf false


##3. 常用命令
> * 克隆:&emsp;&emsp;git clone
> * 添加:&emsp;&emsp;git add
> * 提交:&emsp;&emsp;git commit -m "change info"
> * 添加并提交:&emsp;&emsp;git commit -a -m "info"
> * 状态:&emsp;&emsp;git status
> * 不同:&emsp;&emsp;git diff [filename] ,每次先查看再add再commit
> * Log:&emsp;&emsp; git log [--pretty=oneline] [--abbrev-commit]查看分区历史 [-[index]（index表示第几个）]
> * 回退:&emsp;&emsp; git reset --hard HEAD^(^代表上一个,可以^^ ,当然也可以HEAD~100), 命令行窗口关闭无法找回,通过git reflog 命令
> * 前进:&emsp;&emsp;git reflog
> * 撤销修改:&emsp;&emsp;git checkout -- [fielname]
> * 回退工作去:&emsp;&emsp;git reset HEAD [filename]
> * 删除文件:&emsp;&emsp;git rm [filename] (需要commit)
> * 远程:&emsp;&emsp;git remote add origin git@xxx.com:xxx/xxx/.git
> * 提交至远程:&emsp;&emsp;git push -u origin master(第一次关联往后省命令,直接git push origin master,也可以git push),如svn的update， 拉下最新的代码，再更新服务器
> * 从远程拉本地:&emsp;&emsp;git pull [remote-name] [local branch] ,
> * 创建并切换分支:&emsp;&emsp;git checkout -b [branchname]
> * 创建分支:&emsp;&emsp;git branch [branchname]
> * 切换分支:&emsp;&emsp;git checkout [branchname]
> * 查看分支:&emsp;&emsp;git branch
> * 合并分支:&emsp;&emsp;git merge [branchname] [--no-ff(禁用Fast forward) -m "info"]
> * 删除分支:&emsp;&emsp;git branch -d [branchname] (-d是删除 -D是强行删除，（没有合并的）)
> * 存储区:&emsp;&emsp;git stash（存储） 和 git stash list（查看）
> * 清除存储区:&emsp;&emsp;git stash clear
> * 恢复但不删除内容:&emsp;&emsp;git stash apply 需要手动删除git stash drop 可以指定stash@{index}，指定某个储存区
> * 恢复且删除内容:&emsp;&emsp;git stash pop
> * 查看远程分支，或者详细信息:&emsp;&emsp;git remote 或者 git remote -v
> * 创建远程origin的dev分支到本地:&emsp;&emsp;git checkout -b dev origin/dev
> * 查看所有标签:&emsp;&emsp; git tag
> * 显示标签详细信息:&emsp;&emsp;git show [tagname]
> * 设置tag指定head:&emsp;&emsp;git tag [tagname]  [head指针]
> * 删除本地标签:&emsp;&emsp;git tag -d [tagname]
> * 删除远程标签:&emsp;&emsp;先删除本地，然后git push origin :refs/tags/[tagname]
> * 提交远程标签:&emsp;&emsp;git push origin [tagname],如果是所有，直接git push origin --tags


##4. Git隐藏目录详解
>  .git是Git的版本库,存在一个很重要的stage(Index)暂存区,当然,默认分支就是master,以及指向的一个HEAD指针,所以，HEAD指向的就是当前分支
> > add只是把文件修改添加到暂存区,commit才会把暂存区所有内容提交至当然分支

##5. 生成RSA  [SSH-KEYGEN参数详解](http://killer-jok.iteye.com/blog/1853451)
>  生成github的rsa : ssh-keygen -t rsa -C "email"

##6. 合并的细节 (冲突)
>  默认merge 会用Fast forward, 如果想使用普通模式
>  git merge --no-ff -m "comment" [branchname]
>  
>  冲突的话解决了的话，先add，再提交。。

##7. 提交服务器细节
*  先用git pull把最新的提交从远程origin抓下来，然后，在本地合并，如果有冲突,解决冲突，再推送至服务器：
*  git branch --set-upstream dev origin/dev 如果pull没有与远程服务器进行链接，则无法pull或者push

##8. PGP 验证
*  查看链接--[点我前进](http://developer.51cto.com/art/201409/452049.htm)
*  git tag -a <tagname> -m "blablabla..."可以指定标签信息；
*  git tag -s <tagname> -m "blablabla..."可以用PGP签名标签；

## 9. Git自定义配置
* 配置UI git config --global color.ui true  
* 配置忽略文件, 创建.gitignore 键入文件夹，文件名，可使用通配符， 然后push
* 配置别名  git config --global alias.别名 [指令]，指令语句加定界符'',如'reset HEAD'
* 很牛的显示log得别名配置： git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
* 当前仓库的配置文件再.git/config ，当前用户配置再.gitconfig

## 10. PATCH (补丁)
*  见教材  [PATCH教材](http://blog.csdn.net/hudashi/article/details/7669468)