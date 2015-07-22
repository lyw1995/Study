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
>>      4. git diff 分支1 分支2 比较两个分支的差异 等同于 git diff b1..b2，如果是other的话,git diff b1...o1 (三个点)
>>      5. git diff --staged 比较暂存区与工作区的差异,与--cached 同义
>>      6. git diff HEAD filename  比较HEAD中文件与工作区文件的差异
>>      7. git diff HEAD 比较HEAD提交的与当前工作区的差异
 
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

> 5.更名文件/文件夹
>>      1.git mv 源文件/文件夹名  新文件/文件夹名
 
> 6.撤销文件修改
>>      1. git checkout  -- filename  回滚暂存区的提交文件，
>>      2. git checkout  HEAD(master~) filename  回滚某次提交的文件，可以提交指针，也可以分支提交指针


> 7.提交到版本库 [(git commit详解)](http://blog.csdn.net/hudashi/article/details/7664409)
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
>>      17. git log --branches="分支" 可以查看分支的提交日志
>>      18. gitk  打开图形化界面查看log
>>      19. git log 分支1..分支2  查看该两个分支还没有合并的提交


> 2.reflog 可以查看所有分支的所有操作记录（包括（包括commit和reset的操作），包括已经被删除的commit记录，git log则不能察看已经删除了的commit记录  [查看csdn博客讲解](http://blog.csdn.net/ibingow/article/details/7541402)
>>      1. git reflog 查看所有分支操作记录, 常用逆转操作，取得HEAD@{index}进行追溯
>>      2. git reflog show 与git reflog 同义

## 4. 分支(branch)  [分支详解](http://blog.jobbole.com/25877/)
> 1.查看
>>      1. git branch 查看本地分支列表
>>      2. git branch -v 查看所有分支最后一次提交历史
>>      3. git branch -r 查看远程分支
>>      4. git branch -a 查看本地,远程分支

> 2.添加分支
>>      1. git branch [branchname] 创建本地分支
>>      2. git push origin [branchname] 创建远程分支
>>      3. git branch [新分支] commit_id 从已删除回复分支

> 3.更名,删除
>>      1. git branch -d [branchname] 删除本地分支
>>      2. git branch -D [branchname] 强行删除没有合并的分支
>>      3. git push origin :[branchname] 删除远程分支(注意:(冒号后面接远程分支名))
>>      4. git branch –m oldname newname 更名

> 4.切换分支
>>      1. git checkout [branchname] 切换分支
>>      2. git checkout -b [branchname] 创建并切换分支
>>      3. git checkout -b [分支名] [远程名]/[分支名] 1.6以上使用 git --track [远程]/[分支名] 本地的分支追踪远程仓库的分支,达到联系

> 5.合并分支(merge)
>>      1. git merge anothername 讲another合并到当前分支,Fast-forward,也就是直接把master指向dev的当前提交，所以合并速度非常快。
>>      2. git merge --no-ff -m "comment" anothername,  禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
>>      3. git merge --squash 分支名   合并,但不记录合并记录,最好删除本地也删除远程,防止意外
>>      3. git merge 分支1 分支2 ..    多路合并分支 

> 6.衍合分支(rebase)
>  注:
>>      1. git rebase [branchname] 衍合其他分支
>>      2. git rebase --continue 解决完冲突,注意必须标记该文件为解决,  就是继续合并
>>      3. git rebase --skip 跳过此次合并
>>      4. git rebase --abort 取消此次合并

> 7.撤销合并
>>      1. git reset --hard HEAD(HEAD~ 上上次, HEAD~n(n代表n次)) 撤销当前合并,暂存区，工作区都修改，指针指向改变

## 5.合并冲突解决
> 1.查看差异修改
>>      1. git diff [--ours|--theirs] [文件名]  差异比较文件, (比较自己)|(比较合并的) 
>>      2. vim 啥的编辑工具直接修改, 冲突的文件会有分支标识的,

> 2.直接二选一
>>      1. git checkout --ours 文件名 , 直接选择自己的
>>      2. git chekcout --theirs 文件名 , 直接选择合并

## 6.Git的维护(gc 与 fsck)

## 7.Reset (回滚提交) 默认是HEAD
> 1.充值
>>     1.

## 8.Revert (撤销) 默认是HEA
> 1.充值
>>     1.

## 9.Checkout (检出， 强大)，默认是暂存区
> 1.充值
>>     1.

## 10.Stash (暂存区)

## 11.配置忽略文件

## 12.自定义Git配置

## 注：
>  1.工作区，暂存区，版本库的区别
> > 版本库：      当前仓库下，如果没有任何的提交，那么版本库就是对应上次提交后的内容。

> > 暂存区：      英文叫stage, 或index。在版本库.git）目录下，有一个index文件。它实际上就是一个包含文件索引的目录树，像是一个虚拟的工作区。在这个虚拟工作区的目录树中，记录了文件名、文件的状态信息（时间戳、文件长度等），文件的内容并不存储其中，而是保存在Git对象库（.git/objects）中，文件索引建立了文件和对象库中对象实体之间的对应。如果当前仓库，有文件更新，并且使用gitadd 命令，那么这些更新就会出现在暂存区中。

>> 工作区：       我们会想当然的认为，当前仓库所在目录就是我们的工作区，其实这是不完全正确的。在当前仓库中，新增，更改，删除文件这些动作，都发生在工作区里面



http://wbj05791467.blog.163.com/blog/static/120329697201331735158420/

http://blog.haohtml.com/archives/11464

http://blog.csdn.net/hudashi/article/details/7664460





















