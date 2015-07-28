#             @Track   24245@163.com   转载请注明来源!
* 注1： 若从往下所有命令学习，最后请查阅一定的Git的理论基础，什么Git的优缺点，工作流HEAD，对象等等基础，效果更佳！
* 注2： 收集整理，一些实践，不敢保证绝对没问题，请看官自行实践出真知，thanks。



## 0. 创建篇(Create), Local Or Remote  
 > 1.整个项目克隆下来
>>		1.git clone [remoteAddress, ssh or https] 

 > 2.从远程仓库拉下来
>>      1. git init 初始化本地仓库
>>      2. git remote add [remoteBranch] [remoteAddress]
>>      3. git pull [-u(是否关联)] [remoteBranch] [localBranch]

## 1. HEAD 与ORIN_HEAD
* 注1： HEAD(大写)是"current branch"(当下的分支)。当你用git checkout切换分支的时候，HEAD 修订版本重新指向新的分支。有的时候HEAD会指向一个没有分支名字的修订版本，这种情况叫”detached HEAD“，head(小写)是commit对象的引用，每个head都有一个名字（分支名字或者标签名字等等）
* 注2: .“^”代表父提交,当一个提交有多个父提交时，可以通过在”^”后面跟上一个数字，表示第几个父提交，”^”相当于”^1”.~<n>相当于连续的<n>个”^”.
> 1.查看
>>     1. cat .git/HEAD 当前HEAD全引用全称
>>     2. cat .git/refs/heads/master 查看当前HEAD的sha1

* Git通过记录HEAD指针的上次所在的位置ORIG_HEAD提供了回退的功能。当你发现某些操作失误了，比如错误的reset到了一个很早很早的版本，可以使用 git reset --hard ORIG_HEAD 回退到上一次reset之前。

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
>>      8. git diff --name-status 版本1..版本2 显示出版本1，版本2所有变更的文件列表

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
>>      3. git reset [-- | HEAD] filename ,不改变索引，改变工作区的文件状态，并不改变内容


> 7.提交到版本库 [(git commit详解)](http://blog.csdn.net/hudashi/article/details/7664409)
>>      1. git commit -a -m "注释" (-a,除了untracked,都提交 ,-m 注释 不加每次都谈vim编辑).
>>      2. git commit -amend 修改本地最后一次提交的注释,改别的话,就得reset咯
>>      3. git blame [-L lineS(行开始),lineE(行结束)] [filename] 查看提交的信息,作者之类的 
>>      4. git commit --allow-empty-message -m "" 空白的提交注释,是不是无语了


## 3. 查看日志(log)和 查看个别的对象内容(show)
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
>>      17. git log --branches="分支" 可以查看分支的提交日志,如果没合并看不了,然并卵
>>      18. gitk  打开图形化界面查看log
>>      19. git log 分支1..分支2  查看该两个分支还没有合并的提交
>>      20. git log -p master..origin/master 比较本地的master分支和origin/master分支的差别
>>      21. git log --stat --summary 查看每次提交的变动信息
>>      22. git log –pretty=raw    查看commit之间的父子关系

> 2.reflog 可以查看所有分支的所有操作记录（包括（包括commit和reset的操作），包括已经被删除的commit记录，git log则不能察看已经删除了的commit记录  [查看csdn博客讲解](http://blog.csdn.net/ibingow/article/details/7541402)
>>      1. git reflog 查看所有分支操作记录, 常用逆转操作，取得HEAD@{index}进行追溯
>>      2. git reflog show 与git reflog 同义

> 3.show 和 cat-file, ls-files,ls-tree
>>     1. git show [-- | HEAD | $id] ,查看当前后者某次提交的详细数据
>>     2. git show --stat 若指定该参数，只显示操作详情，如删除几个文件，插入几个文件，不涉及主体内容
>>     3. git show -s --pretty=raw $id 查看某一个commit对象详细内容（包括：Tree，作者，parent，注释等）
>>     4. git cat-file type $id 查看指定type（blob，tree）和指定id（文件id），查看内容或者信息
>>     5. git cat-file -t $id 查看id的类型，例如commit对象 打印除 commit 类型
>>     6. git show-ref --heads 列出仓库中所有的头
>>     7. git ls-files --stage 列出索引的内容
>>     8. git ls-tree $id 查看某一个提交，下面的tree树

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
>>      4. git branch --set-upstream master origin/next ,将本地本地与远程分支建立联系,默认是与origin/master建立联系的

> 2.1 创建空分支((执行三步命令之前记得先提交你当前分支的修改,否则....)
>>      1.0 git symbolic-ref HEAD refs/heads/[name]
>>      1.1 rm .git/index
>>      1.1 git clean -fdx  

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
>  注: 会生成一个新的节点, 
>>      1. git merge anothername 讲another合并到当前分支,Fast-forward,也就是直接把master指向dev的当前提交，所以合并速度非常快。
>>      2. git merge --no-ff -m "comment" anothername,  禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
>>      3. git merge --squash 分支名   合并,但不记录合并记录,最好删除本地也删除远程,防止意外
>>      4. git merge 分支1 分支2 ..    多路合并分支 
>>      5. git merge $id ，再git fsck --lost-found 找的悬空commit对象，可以使用这个命令恢复,或者rebase

> 6.衍合分支(rebase)
>  注: 并不会生成新的节点,同时也能手动控制操作
>>      1. git rebase [branchname] 衍合本地分支, git rebase origin/master 衍合远程分支
>>      2. git rebase --continue 解决完冲突,注意必须标记该文件为解决,  就是继续合并
>>      3. git rebase --skip 跳过此次合并
>>      4. git rebase --abort 取消此次合并
>>      5. git rebase -i 修改提交,p,r,e,s,f,x

## 5.合并冲突解决
> 1.查看差异修改
>>      1. git diff [--ours|--theirs] [文件名]  差异比较文件, (比较自己)|(比较合并的) ,具体请看diff命令
>>      2. vim 啥的编辑工具直接修改, 冲突的文件会有标记标识的,

> 2.直接二选一
>>      1. git checkout --ours 文件名 , 直接选择自己的
>>      2. git chekcout --theirs 文件名 , 直接选择合并

## 6.Git的维护(gc 与 fsck)
> 1. 保证git良好的性能，git靠压缩历史信息来节约磁盘和内存空间.有时需要手动执行，也可以将自动关闭，配置一下即可
>>      1. git gc  执行垃圾清理，如果配置了gc.pruneexpire，那么过期时间到了就将永久删除， 

> 2. 保持git的可靠性,运行一些仓库的一致性检查, 如果有任何问题就会报告. 这项操作也有点耗时, 通常报的警告就是“悬空对象"
>>      1. git fsck 悬空对象"(dangling objects)并不是问题, 最坏的情况只是它们多占了一些磁盘空间. 有时候它们是找回丢失的工作的最后一丝希望.
>>      2. git fsck --lost-found 查看刚刚悬空对象中包括commit的，默认git fsck 是没有commit的
>>      3. git fsck --unreachable 貌似与上面差不多

## 7.Reset (回滚提交) 默认是HEAD
> 注: 重置一般用于重置暂存区,--hard特殊, checkout只会移动HEAD指针，reset会改变HEAD的引用值。
> 1.在reset可以遗弃不再使用的提交。执行遗弃时，需要根据影响的范围而指定不同的模式，可以指定是否复原索引或工作树的内容。
>>     1. git reset --hard HEAD~ (撤销最近的提交,引用回退,工作区,暂存区也回退,git log查看不到,用reflog) 
>>     2. git reset --soft HEAD~ (引用回退,但工作区内容不改变,暂存区回退,可再次checkout检出)
>>     3. git reset --mixed HEAD~ (引用回退,但工作区内容不改变,暂存区回退,可再次checkout检出)
>>     4. git reset -- filename 从暂存区中取消该文件的改动（内容不动）,相当于add的方向操作，不该变索引

## 8.Revert (撤销) 
> 常用于回滚某个commit
> 1.回滚commit
>>     1. git revert  [-- | commitid | HEAD],回滚某次提交,与本地工作区进行合并, 也许可能产生冲突,索引不改变,commit记录不改变

## 9.Checkout (检出， 强大)，默认是暂存区
> 注: checkout常用于修改工作区, 改变暂存区,与工作区,checkout只会移动HEAD指针，reset会改变HEAD的引用值。
> 1. 撤销,恢复某次提交或者某次提交中
>>     1. git checkout -- file 从当前版本库检出工作区,(--可以使某次提交,--表示当前HEAD)
>>     2. git checkout HEAD 直接检出HEAD的提交,HEAD就是当前
>>     3. git checkout 查看版本库,暂存区,工作区的差异
>>     4. git checkout branchname HEAD filename 从某个分支某次提交检出某个文件
>>     5. git checkout tagname 从当前分支上检出tag标识的版本
>>     6. git checkout "@{5}" 检出捡出第五次访问过的提交，同义与git checout HEAD@{5},是reglog 里面的提交记录

> 2. 分支的操作
>>     1. 如上分支操作

> 3. 其他
> > 

## 10.Stash (暂存区)
> 1.查看
> >   1. git stash show 指定stash@{n} 显示该暂存简略做了啥，例如增删改查等。
> >   2. git stash list 显示当前暂存区列表

> 2.存储
> >  1. git stash ,存储本地改变之后的数据，就是未提交的
> >  2. git stash save [message]， 可传message ，不传默认就是该commit提交注释


> 3.取出
> >  1. git stash pop stash@{n} 取出并删除,成功才会删除，出现冲突啥的不会
> >  2. git stash apply stash@{n} 取出但不删除，需要手动drop
> >  3. git stash branch <branchname> stash@{n} 将暂存区内容作为新的分支

> 3.清空
> >  1. git stash clear 清空暂存区
> >  3. git stash drop stash@{n} 删除暂存区

> 3.其他 (没试过)
> >  1. git stash create [<message>] 
> >  2. git stash store [-m|--message <message>] [-q|--quiet] <commit>
 

## 11.Pull (拉取) 和 Fetch(取回) 
> 注1：　fetch比 pull更安全一些因为在merge前，我们可以查看更新情况，然后再决定是否合并
> 注2:  请看config 中的url配置
> 1. pull
>>   1. git pull origin origin:next 取回origin主机的next分支，与本地的master分支合并,
>>   2. git pull origin master 直接与本地master分支合并
>>   3. git pull --rebase <远程主机名> <远程分支名>:<本地分支名> 采用rebase方式进行合并
>>   4. git pull -p 如果远程分支删除了,本地还没删除, 可以使用这个命令进行删除远程已删除分支
>>   5. git pull git://git..../proj.git master 直接传地址远程master分支与本地分支合并

> 2.fetch
>>   1.  git fetch --prune origin 同义于 git fetch -p  等同义与 git pull -p, 如果远程分支删除了,本地还没删除, 可以使用这个命令进行删除远程已删除分支
>>   2. 先 git fetch origin 取回远程分支 ,再git merge origin/next 当前分支与远程next分支进行合并
>>   3. git fetch origin 默认取回主机左右分支的内容,如果git fetch origin master 指定取回origin/master分支内容,取回之后可以checkout,merge,rebase, 爱咋干就咋整
## 12.Push (推送)
> 1.提交
>>   1. git push origin master 把本地仓库提交到远程仓库的master分支中
>>   2. git push origin test:master  提交本地test分支作为远程的master分支
>>   3. git push origin :test         刚提交到远程的test将被删除，但是本地还会保存的，不用担心
>>   4. git push -f origin master    -f就是强制提交吧, 本地有,远程删除了, 还是啥问题..
>>   5. git push origin --tags 一次性提交所有标签
>>   6. git push origin tagname 指定tagname推送
 
## 13. Cherry-pick(挑选)
> 1. cherry-pick 用于把另一个本地分支的commit修改应用到当前分支。
>>   1.git cherry-pick $id ,讲$id提交应用于当前分支,出现冲突, 解决冲突, 然后git commit -c (原提交ID),即可!

## 14 remote (远程)
> 1. 查看
>>   1. git remote 列出所有远程主机
>>   2. git remote -v 列出所有远程主机地址
>>   3. git remote show <主机名> 显示主机的详细信息
>>   4. git remote -v | --verbose 列出详细信息，在每一个名字后面列出其远程url

> 2. 添加
>>   1. git remote add origin <repository>  ..   添加远程仓库地址,然后可以pull,push拉
>>   2. git remote add -o newOrigin <repository>  所使用的远程主机自动被Git命名为origin。如果想用其他的主机名，需要用git clone命令的-o选项指定
>>   3. git remote add -t BRANCH_NAME_HERE -f origin REMOTE_REPO_URL_PATH_HERE 添加远程中某一个分支为本地分支

> 3. 修改
>>   1. git remote rename <原主机名> <新主机名> ..  修改主机名,
>>   2. git remote set-url origin <repository> ..   设置远程仓库地址(用于修改远程仓库地址)  

> 4. 删除
>>   1. git remote remove  name     # 删除远程仓库  

> 5. 设置
>>   1. git remote set-head origin master    设置远程仓库的HEAD指向master分支  

## 15 clone (克隆)
> 1. clone
>>   1. git clone <repository>  Clone远程版本库 
>>   2. git clone --bare robbin_site robbin_site.git   用带版本的项目创建纯版本仓库
>>   3. git --bare init example.git 创建远程仓库, 然后可以clone啥的..
>>   4. git clone  git://github.com/someone/some_project.git   some_project  有一个远程的Git版本库，只需要在本地克隆一份

## 16 tag (标签)
> 注：一个标签对象包括一个对象名(译者注:就是SHA1签名), 对象类型, 标签名, 标签创建人的名字("tagger"), 还有一条可能包含有签名(signature)的消息. 
> 1.查看
>>   1. git tag  查看当前分支所有标签
>>   2. git cat-file tag tagname 指定一个标签对象名称查看详细的对象信息

> 2.创建
>>   1. git tag tagname  默认标签是打在最新提交的commit上的
>>   2. git tag tagname $id 给指定id打上tag
>>   3. git -a tag -m "注释" tagname , (用-a指定标签名，-m指定说明文字),如果带了-a,-u,-s等参数,就必须要带-m之类的,不然会要手动edit..
>>   4. git -s tagname $id 创建指定签名的tag对象,签名采用PGP签名，因此，必须首先安装gpg（GnuPG）,可以全局配置
>>   5. git tag -u <gpg-key-id> tagname $id 如果没有在配置文件中配GPG key,你可以用"-u“ 参数直接指定。

> 3. 删除,更改
>>   1. git tag -d tagname 本地删除标签
>>   2. git push origin :refs/tags/tagname  远程删除标签

## 17.配置忽略文件
* 忽略文件的原则是：
   * 忽略操作系统自动生成的文件，比如缩略图等；
   * 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
   * 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。
 
>>   1. 在工作区根目录下创建.gitignore忽略文件,然后配置,可以参考下网上的[配置](https://github.com/github/gitignore),注意必须gitignore先存在, 然后配置才会生效,,


## 18.自定义Git配置
*  注1: ,当前仓库的配置文件再.git/config ，当前用户配置再.gitconfig ，--local  选项是默认选项
*  注2:  使用 git config -l 查看当前所有的配置 , git config -h 查看所有配置选项帮助
 * `1.git config  [–-add(添加配置) --get(查看某个配置)  --unset(删除某个配置)] configname 对配置进行增删改查  `
> 1.初始化配置，（配置name，email用于commit提交）
>>   1. git --global user.name "username"  注：1.7以上貌似需要git config --XXX((--global 代表全局))
>>   2. git --global user.email "email"
>>   3. git --global core.autocrlf false
>>   4. git config --global color.ui true 让Git显示颜色，会让命令输出看起来更醒目

> 2.配置别名
>>   1. git config --global alias.st(别名) status(指令, 两个包含参数用""包裹)
>>   2. git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"  好用的log 配置.. 直接git lg就行了

> 3.配置gc超时时间
>>   1. git config gc.pruneexpire "30 days" 一个月超时时间..被删除的提交会在删除30天后，且运行 *git gc* 以后，被永久丢弃

> 4.配置默认远程分支,默认合并分支
>>   1. git config branch.master.remote origin    配置默认远程分支是origin
>>   2. git config branch.master.merge refs/heads/master 配置本地默认合并分支是master
>>   3. git config branch.BRANCH_NAME_HERE.rebase true  也可以将某条branch(BRANCH_NAME_HERE)配置为总是使用rebase推送：


> 5.配置PGP签名
>>   1. git config (--global) user.signingkey <gpg-key-id> 配置签名

> 6.配置默认打开的editor
>>   1. git config --global core.editor "mate -w"    # 设置Editor使用textmate
>>   2. git config --global core.editor vim 设置默认的Editor是vim

> 7.配置缓存
>>   1. git config --global credential.helper cache  配置到缓存 默认15分钟 
>>   2. git config --global credential.helper 'cache --timeout=3600'  修改缓存时间
  
##  19.生成rsa 
>  1.生成
>>   1. github的rsa : ssh-keygen -t rsa -C "email" ( [SSH-KEYGEN参数详解](http://killer-jok.iteye.com/blog/1853451)) ,-t指定生成秘钥格式, -C指定说明文字

##  20. Tree,Commit,Blog
* 每个目录都创建了 tree对象 (包括根目录), 每个文件都创建了一个对应的 blob对象 . 最后有一个 commit对象 来指向根tree对象(root of trees), 这样就形成了一个提交对象

##  21. Git引用
* git中，分支(branch), 远程跟踪分支(remote-tracking branch)以及标签(tag)都是对提交的引用. 所有的引用是用"refs"开头, 以斜杠分割的路径. 到目前为此, 我们用到的引用名称其实是它们的简写版本:
- 分支"test"是"refs/heads/test"的简写.
- 标签"v2.6.18"是"refs/tags/v2.6.18"的简写.
- "origin/master"是"refs/remotes/origin/master"的简写.
偶尔的情况下全名会比较有用, 例如你的标签和分支重名了, 你应该用全名去区分它们.
(新创建的引用会依据它们的名字存放在.git/refs目录中. 然而, 为了提高效率, 它们也可能被打包到一个文件中, 参见git pack-refs).

##  22. git grep (检索)
> 1.搜索
>>   1. git grep -n -c hello [指定tag，$id,] 检索整个仓库带hello内容文件,-n 带行号参数,-c 包含内容行统计
>>   2. git grep --name-only hello ,检出整个仓库包含内容hello的文件列表
>>   3. git grep -e 'haha' --and -e TEST , 使用both（与）条件检索， 包含内容 haha TEST的文件
>>   4. git grep --all-match -e 'haha' -e TEST,使用either(或)进行条件检索，包含haha 或 TEST的文件
>>   5. git grep -e 'haha' --and \( -e NIMA -e NIBA \) 检索包含haha并且 NIMA或者NIBA的内容（之一）

##  23. git 导出（export）项目
> 1.archive
>>   1. git archive --format=zip --output=tagname.zip tagname 导出指定tagname格式为zip名称为tagname.zip的项目包
>>   2. git archive tagname | bzip2 > tagname.tar.bz2  导出并压缩成.tag.bz2格式
>>   3. git archive --format=tar tagname | gzip > tagname.tar.gz 导出并压缩成.tag.gz格式
>>   4. git archive -o latest.zip HEAD 导出最新zip
>>   5. git archive -o partial.tar HEAD src doc 导出最新zip，只包含src，doc文件夹
>>   6. git archive -o ../updated.zip HEAD | (git diff --name-only HEAD^) ，导出当前分支与上个分支修改的文件

## 其他
* git update-index --assume-unchanged PATH_TO_FILE_HERE 要求git忽视指定文件的变动

## Git索引，Git打包文件，Git对象 
  
## 后期扩展 PATCH 与 PGP签名
 
 [PATCH教材](http://blog.csdn.net/hudashi/article/details/7669468)
 [PATCH教程](http://blog.csdn.net/kevinx_xu/article/details/11660915)
 [GPG签名学习](http://developer.51cto.com/art/201409/452049.htm)
 
## Git服务器搭建

## 注：
>  1.工作区，暂存区，版本库的区别
> > 版本库：      当前仓库下，如果没有任何的提交，那么版本库就是对应上次提交后的内容。

> > 暂存区：      英文叫stage, 或index。在版本库.git）目录下，有一个index文件。它实际上就是一个包含文件索引的目录树，像是一个虚拟的工作区。在这个虚拟工作区的目录树中，记录了文件名、文件的状态信息（时间戳、文件长度等），文件的内容并不存储其中，而是保存在Git对象库（.git/objects）中，文件索引建立了文件和对象库中对象实体之间的对应。如果当前仓库，有文件更新，并且使用gitadd 命令，那么这些更新就会出现在暂存区中。

>> 工作区：       我们会想当然的认为，当前仓库所在目录就是我们的工作区，其实这是不完全正确的。在当前仓库中，新增，更改，删除文件这些动作，都发生在工作区里面

## 总结: 很多挺不错的Git学习blog. 感谢他们的知识分享!
*   [官方文档](https://www.kernel.org/pub/software/scm/git/docs/git-reset.html)
*  [Git community book 中文版](http://gitbook.liuhui998.com/index.html)
*  [廖雪峰大神Git讲解](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137396287703354d8c6c01c904c7d9ff056ae23da865a000) 
*   [Git 初体验](http://www.cnblogs.com/BeginMan/p/3543240.html)
*  [csdn博客   版本控制](http://blog.csdn.net/hudashi/article/category/1122124)
*   [高富帅玩 git](http://mux.alimama.com/posts/711)
*   [常用命令整理](http://justcoding.iteye.com/blog/1830388)
*  [Git高级使用](http://blog.haohtml.com/archives/11464)
*   [Git Checkout](http://wbj05791467.blog.163.com/blog/static/120329697201331735158420/)
http://wbj05791467.blog.163.com/blog/static/120329697201331735158420/
*   [Git Config](http://www.07net01.com/program/39271.html)
*   [Git 常用命令](http://www.oschina.net/question/565065_86025)
*   [Git pull fetch区别,中文翻译对照](http://www.oschina.net/translate/git-fetch-and-merge?cmp)
*  [易百Git的教程](http://www.yiibai.com/git/git_pull.html)
*   [Git魔法学习](http://www-cs-students.stanford.edu/~blynn/gitmagic/intl/zh_cn/book.html)
*   [Git使用命令](http://www.cnblogs.com/TerryBlog/archive/2013/03/19/2969283.html)
*   [Git学历笔记](http://blog.haohtml.com/archives/11464)
*   [Git reset,Checkout区别](http://wbj05791467.blog.163.com/blog/static/120329697201331735158420/)
*   [阿里MUX分享](http://mux.alimama.com/posts/799)
*   [10个很有用的高级命令](http://www.oschina.net/translate/10-useful-advanced-git-commands?print)
*   [Git架构](http://blog.csdn.net/weinianjie1/article/details/8947966)

















