#@Track   7/20/2015 6:58:12 PM
	git --global user.name "username"  注：1.7以上貌似需要git config --XXX
	git --global user.email "email"
	git --global core.autocrlf false
	git config --global color.ui true



## 1. 创建篇(Create), Local Or Remote  
 > 1.整个项目克隆下来
>>		1.git clone [remoteAddress, ssh or https] 

 > 2.从远程仓库拉下来
>>      1. git init 初始化本地仓库
>>      2. git remote add [remoteBranch] [remoteAddress]
>>      3. git pull [-u(是否关联)] [remoteBranch] [localBranch]

## 2. 本地修改状态(Local Changes),
 > 1.查看本地改变的文件状态
>>		1.git status

 > 2.比较差异
>>      1. git diff [file|dir] 查看所有差异
>>      2. git diff --stat [file|dir] 统计该文件/文件夹的所有操作统计
>>      3. git diff $id1 $id2 比较两次提交的差异
>>      4. git diff 分支1 分支2 比较两个分支的差异
>>      5. git diff --staged 比较暂存区与工作区的差异,与--cached 同义
 
 > 3.添加文件/文件夹  [(git add详解)](http://blog.csdn.net/hudashi/article/details/7664374) ------- [(高富帅们的Git技巧)](http://mux.alimama.com/posts/711)
>>      1. git add . | git add -A  提交全部
>>      2. git add -u (untracked的文件不会提交,其他都会)
>>      3. git add -i (进入子命令系统,revert可以把存储区的撤回)
>>      4. git add -p [file(不加就当前目录)],可以修改等然提交至待提交状态,(1:例如,修改五个文件,只想提交三个文件,不错的使用

> 4.删除文件/文件夹
>>      1. git rm  删除文件(commit的)
>>      2. git rm -f 强制删除文件(没有commit的)
>>      3. git rm  -rf 强制删除文件夹(非空)
>>      4. git rm --cached 从暂存区删除,保留在工作区
>>      5. git clean -fd (会删除所有untracted文件,删除空目录,慎用)

>5.更名文件/文件夹
>>      1.git mv 源文件/文件夹名  新文件/文件夹名
 
 > 6.提交到版本库 [(git commit详解)](http://blog.csdn.net/hudashi/article/details/7664409)
>>      1. git commit -a -m "注释" (-a,除了untracked,都提交 ,-m 注释 不加每次都谈vim编辑).
>>      2. git commit -amend 修改本地最后一次提交的注释,改别的话,就得reset咯
>>      3. git blame [-L lineS(行开始),lineE(行结束)] [filename] 查看提交的信息,作者之类的 
>>      4. git commit --allow-empty-message -m "" 空白的提交注释,是不是无语了


## 3. 查看日志(log)
> 1.查看提交日志 [(git log详解)](http://blog.csdn.net/hudashi/article/details/7451555)  [(git log简解)](http://gitbook.liuhui998.com/3_4.html)
>>      1. git log  [$id] 查看所有提交的日志,指定ID,则从ID开始显示记录
>>      2. git log --stat 查看每次提交的操作,例如删除,修改啥文件
>>      3. git log -2  查看近两次提交日志
>>      4. git log --pretty=oneline,short,medium,full,fuller,email,raw以及format:<string>,等指定格式显示日志信息,例(--pretty=format:"%an %cn %p %s")
>>      5. git log --merges 查看分支合并信息, --no-merges 就是不合并信息
>>      6. git log --author=[your name], 查看作者提交日志
>>      7. git log --grep "grep content" 或者 --grep=xxx  过滤提交日志信息获取记录
>>      8. git log --abbrev-commit 精简sha-1签名..
>>      9. git log --name-status 显示新增,修改,删除的每次提交清单
>>      10. git log [branchname] 查看某分支的提交记录
>>      11. git log 查看[文件名,或者文件夹]的提交日志
>>      12. git log -p [file] 查看全部,或者指定文件提交时补丁信息,也可以看到文件修改信息
>>      13. git log --before={2015-07-21}或者--until,--after,--since ,, 现在测不出啥接过来. 就是时间之间查询日志吧,
>>      14. git log --log-size 查看日志大小
>>      15. git log --tags [tagname] 查看标签的提交日志
>>      16. git log --date-order 显示提交日志的顺序主要按提交日期来排序,--topo-order 提交(commits)按拓朴顺序来显示(就是子提交在它们的父提交前显示)

> 2.reflog 可以查看所有分支的所有操作记录（包括（包括commit和reset的操作），包括已经被删除的commit记录，git log则不能察看已经删除了的commit记录  [查看csdn博客讲解](http://blog.csdn.net/ibingow/article/details/7541402)
>>      1. git reflog 查看所有分支操作记录, 常用逆转操作，取得HEAD@{index}进行追溯

## 4. 分支(branch)
> 


























