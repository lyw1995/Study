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
 > 1.查看本地改变的文件或者目录
>>		1.git status

 > 2.查看存储区与工作区文件的差异,不同之处
>>      1. git diff [file|dir]

 > 3.添加到暂存区  [(git add详解)](http://blog.csdn.net/hudashi/article/details/7664374) ------- [(高富帅们的Git技巧)](http://mux.alimama.com/posts/711)
>>      1. git add . | git add -A  提交全部
>>      2. git add -u (untracked的文件不会提交,其他都会)
>>      3. git add -i (进入子命令系统,revert可以把存储区的撤回)
>>      4. git add -p [file(不加就当前目录)],可以修改等然提交至待提交状态,(1:例如,修改五个文件,只想提交三个文件,不错的使用)

 > 4.提交到版本库 [(git commit详解)](http://blog.csdn.net/hudashi/article/details/7664409)
>>      1. git commit -a -m "注释" (-a,除了untracked,都提交 ,-m 注释 不加每次都谈vim编辑).
>>      2. git commit -amend 修改本地最后一次提交的注释,改别的话,就得reset咯
>>      3. git blame [-L lineS(行开始),lineE(行结束)] [filename], 查看提交的信息,作者之类的 
