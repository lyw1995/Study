# Git 的使用  7/6/2015 5:31:00 PM 

##1. 下载安装, 见 [廖雪峰大神Git讲解](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137396287703354d8c6c01c904c7d9ff056ae23da865a000)
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
> * Log:&emsp;&emsp; git log [--pretty=oneline] [--abbrev-commit]查看分区历史
> * 回退:&emsp;&emsp; git reset --hard HEAD^(^代表上一个,可以^^ ,当然也可以HEAD~100), 命令行窗口关闭无法找回,通过git reflog 命令
> * 前进:&emsp;&emsp;git reflog
> * 撤销修改:&emsp;&emsp;git checkout -- [fielname]
> * 回退工作去:&emsp;&emsp;git reset HEAD [filename]
> * 删除文件:&emsp;&emsp;git rm [filename]
> * 远程:&emsp;&emsp;git remote add origin git@xxx.com:xxx/xxx/.git
> * 提交至远程:&emsp;&emsp;git push -u origin master(第一次关联往后省命令,直接git push origin master,也可以git push)
> * 从远程拉本地:&emsp;&emsp;git pull [remote-name] [local branch] ,
> * 创建并切换分支:&emsp;&emsp;git checkout -b [branchname]
> * 创建分支:&emsp;&emsp;git branch [branchname]
> * 切换分支:&emsp;&emsp;git checkout [branchname]
> * 查看分支:&emsp;&emsp;git branch
> * 合并分支:&emsp;&emsp;git merge [branchname] [--no-ff(禁用Fast forward) -m "info"]
> * 删除分支:&emsp;&emsp;git branch -d [branchname]

##4. Git隐藏目录详解
>  .git是Git的版本库,存在一个很重要的stage(Index)暂存区,当然,默认分支就是master,以及指向的一个HEAD指针,所以，HEAD指向的就是当前分支
> > add只是把文件修改添加到暂存区,commit才会把暂存区所有内容提交至当然分支

##5. 生成RSA
>  生成github的rsa : ssh-keygen -t rsa -C "email"

##6. 合并的细节 (冲突)
>  默认merge 会用Fast forward, 如果想使用普通模式
>  git merge --no-ff -m "comment" [branchname]
>  
>  冲突的话解决了的话，先add，再提交。。