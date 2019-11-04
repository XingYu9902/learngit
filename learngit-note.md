## Git的三种状态
Git有三种状态、你的文件可能处于其中之一：**已提交（committed）、已修改（modified）和已暂存（staged）**。**已提交**表示数据已经安全的保存在本地数据库中。**已修改**表示修改了文件，但还没有保存到数据库中。**已暂存**表示对一个已修改文件的当前版本做了标记，使之包含在下一次提交的快照中。由此引入Git项目的三个工作区域的概念：Git仓库、工作目录以及暂存区域。

![工作区域](https://github.com/XingYu9902/learngit/blob/master/images/Snipaste_2019-10-31_18-03-08.png)

>Git仓库目录时Git用来保存项目的源数据和对象数据库的地方。这是Git中最重要的部分，从其它计算机克隆仓库时，拷贝的就是这里的数据。

>工作目录是对项目的某个版本独立提取出来的内容。这些从Git仓库的压缩数据库中提取出来的文件，放在磁盘上供你使用或修改

>暂存区域是一个文件，保存了下次将提交的文件列表信息，一般在Git仓库目录中。有时候也被称作“索引”，不过一般说法还是叫暂存区域

![状态1](https://github.com/XingYu9902/learngit/blob/master/images/Snipaste_2019-10-31_17-56-26.png)

![状态2](https://github.com/XingYu9902/learngit/blob/master/images/Snipaste_2019-10-31_17-56-51.png)

![状态3](https://github.com/XingYu9902/learngit/blob/master/images/Snipaste_2019-10-31_18-57-03.png)

## 在Windows上安装Git
在Windows上使用Git，可以从Git官网直接下载安装程序，在国内可以使用镜像。


## 创建版本库
  >在Windows系统下，尽量确保目录名没有中文，防止发生奇怪的错误。

  >1.cd d:  进入d盘

  >2.mkdir \<repository-name\>  创建库
  
  >3.cd \<repository-name\> 进入库内
  
 >补充， pwd命令显示当前目录路径, ls显示当前目录，ls -ah显示隐藏目录
 
 >4.通过git init命令把这个目录变成Git可以管理的仓库
 
 ## Git配置
 在下载安装好git后，需要对Git进行配置
 >$ git config --global user.name "Your Name"          Your Name为GitHub用户名
 
 >$ git config --global uesr.email "email@example.com"      email为Github的注册邮箱
# 时光穿梭机
## 将文件添加到版本库
### 使用vi编辑器
>1.vi \<file-name\> 创建、修改文件

>2.按i进入编辑模式

>3.编辑完成按ESC，选择一下命令操作：

![1](https://github.com/XingYu9902/learngit/blob/master/images/dasda.png)

>查看文件内容 cat \<file-name\>

>4.git add \<file-name\>  把文件添加到暂存区

>5.git commit -m "描述" 把文件提交到git仓库

>简单解释一下git commit命令，-m后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。嫌麻烦不想输入-m "xxx"行不行？确实有办法可以这么干，但是强烈不建议你这么干，因为输入说明对自己对别人阅读都很重要。

>注意，可以先多次`git add`,最后一次`git commit`

## 查看仓库状态
>$ git status 可以查看上述所说的三种状态。

## 版本回退

git log命令显示从最近到最远的提交日志,如果觉得显示的信息看起来太复杂，我们可以用 **--pretty=oneline**参数，使信息看着更加清晰。

接下来启动时光穿梭机，把我们修改的文件回退到上一个版本，怎么做呢？

首先，GIt必须知道当前版本是哪个版本，在Git中，**用HEAD表示当前版本**，也就是那一串16进制数列，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^容易数不过来，所以写成HEAD~100。

然后使用命令：

>$ git reset --hard HEAD^ 

就可以使文件回退到上一个版本。

但是，假如我们已经修改了很多版本，要回退到某一个版本，光靠记忆肯定是记不住的，所以Git为我们提供一个可以查看历史提交信息的命令：

>$ git log

在历史提交信息中，我们可以看见每一次提交的描述信息和commit_id，使用commit_id就可以回退到我们指定版本，使用命令：

>$ git reset --hard commit_id 

现在我们知道了如何回到过去，那么如何重返现在呢，Git提供了git reflog命令，可以查看命令历史。

>$ git reflog

### 小结
- HEAD指向的版本就是当前版本，因此Git允许我们在版本的历史之间穿梭，使用命令**git reset --hard commit_id**
- 穿梭前，用**git log**可以查看提交历史，以便确定要回退到哪个版本。
- 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本

## 管理修改
为什么Git比其他版本控制系统设计的优秀，因为Git跟踪并管理的是修改，而非文件。

举个例子：

比方说我们修改一个文件：readme.md，并git add，然后我们再修改readme.md，接下来我们git commit，然后我们使用git status查看状态，你会发现，在状态中显示我们并没有做出改变，这是为什么？

让我们回顾一下操作过程：第一次修改->gitadd->第二次修改->git commit

找到原因了，因为Git管理的是修改，当你用git add命令后，在工作区的第一次修改被放入暂存区，准备提交，但是在工作区的第二次修改并没有放入暂存区，所以git commit只负责把暂存区的的修改提交，也就是第一次的修改被提交了，第二次的修改不会被提交。

使用命令:

>$ git diff HEAD --\<file-name\> 可以查看工作区和版本库里面最新版本的区别

### 小结
每次修改，如果不用git add到暂存区，那就不会加入到commit中。

## 撤销修改

假如你正在修改一个文件，但是你发现你添加的内容不太对劲，这时你需要纠正它，你可以选择手动删除，或者手动把文件恢复到上一个版本，正如我们在版本回退中的演示那样。

不过Git可以帮助你丢弃你最近一次的全部修改，使用命令：

>$ git checkout --\<file-name\> 就可以把file-name的修改全部撤销，此时有两种情况：

1. 一种是\<file-name\>自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库(上一次commit)一模一样的状态；

2.一种是\<file-name\>已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区(上一次add）后的状态。

但是还有一种情况是，你不但做了修改，还add到了暂存区，庆幸的是你在commit之前发现了这个错误，这是Git可以用命令：

>git restore --staged \<file-name\> 就可以把暂存区修改的文件，放回工作区，此时就回到上述**1**中的场景了。

### 小结
- 当你改乱了某个文件内容的时候，你可以手动删除。当你想丢弃工作区的修改时，使用命令git checkout -- file

- 当你改乱了某个文件，并且提交到暂存区（stage）的时候，想丢弃修改，分两步，第一步使用git restore --staged file或者 git reset HEAD file，退回到工作区，然后按1的步骤操作

- 已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

## 删除文件
假如在工作区添加一个新文件：test.txt，如果想删除它，使用rm命令：rm test.txt，这种情况下不能撤销删除。

如果将新文件test.txt添加到暂存区，然后删除它，仍然可以使用rm命令，此时可以使用git checkout -- file 撤销删除

如果我们确定要删除它，该怎么做呢？

>使用$ git rm，但是使用git rm命令前，必须将文件提交到版本库，提交版本库后，使用**git rm、git commit - m**就可以彻底删除文件。

另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：

>$ git checkout -- test.txt

>$ git checkout 其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

>**注意：从来没有被添加到版本库就被删除的文件，是无法恢复的！ **

### 小结
1.如果你用的rm删除文件，那就相当于只删除了工作区的文件，如果想要恢复，直接用git checkout -- <file>就可以 
  
2.如果你用的是git rm删除文件，那就相当于不仅删除了文件，而且还添加到了暂存区，需要先git reset HEAD <file>，然后再git checkout -- <file> 
  
3.如果你想彻底把版本库的删除掉，先git rm，再git commit 就ok了

4.命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失**最近一次提交后你修改的内容**。

>第4条举例：

>test.txt（2行文字） ——add——commit——rm——checkout——这样删除了你会获得test.txt（2行文字）

>test.txt （2行文字）——add——commit——修改增加test.txt的内容（3行文字）——rm——checkout——这样删除了你会获得test.txt（2行文字）

>于是，你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。

# 远程仓库
与Github建立联系：
由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：
第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

>$ ssh-keygen -t rsa -C "youremail@example.com"

你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。

如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容

### 小结
创建SSH key命令：

>$ ssh-keygen -t rsa -C "youremail@example.com"

## 添加远程库

现在的情景是，你已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作，真是一举多得。
首先，登录Github，然后创建一个新的仓库，仓库名字填入learngit，这样我们就创建了一个新的仓库。
目前，在GitHub上的这个learngit仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。
现在，我们根据GitHub的提示，在本地的learngit仓库下运行命令：

>$ git remote add origin git@github.com:XingYu9902/learngit.git

添加后，**远程库的名字就是origin**，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。

## 推送到远程仓库

- 第一次推送到Github

>$ git push -u origin master

- 后续推送到Github

>$ git push origin master 不再使用参数-u

## 从远程库克隆

>$ git clone git@github.com:username/repositoryname.git

或者使用https

# 分支管理

分支在实际中有什么用呢？假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代码全部写完再一次提交，又存在丢失每天进度的巨大风险。
现在有了分支，就不用怕了。你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。

## 查看分支

>$ git branch

## 创建分支

>$ git branch <branch-name>
  
## 切换分支

>$ git branch <branch-name>
  
## 创建+切换分支

>$ git checkout -b <branch-name>
  
  ## 合并某分支到当前分支
  
  >$ git merge <branch-name>  快速合并
  
  ## 普通模式合并分支
  
  >$ git merge --no-ff -m "description" <branch-name>
  
  >通常进行分支合并时，如果可以，Git会使用`Fast forward`模式，删除分支后，分支历史信息会丢失

>`--no-ff`表示禁用Fast forward模式，能看出曾做过合并

## 删除分支

>$ git branch -d <branch-name>
  
  ## 强行删除分支
  
  >$ git branch -D <branch-name>
  
  ## 查看分支合并图
  
  >$ git log --graph
  
  简洁查看:
  >$ git log --graph --pretty=oneline --abbrev-commit
  
  # Bug分支
  
>假设场景：我们正在研发某产品A的2.0版本。

1.我们在dev分支上研发2.0版本

2.这时，有用户反映在1.0版本上出现了Bug需要修复

3.这个时候我们就需要从dev分支上切换到有Bug的分支上

4.正常情况下，我们需要先把dev分支上的工作先提交后在切换分支

5.但是dev分支上的任务还没有完成，不能提交，所以我们需要先把dev存起来，使用stash

6.切换到有Bug分支

7.在有Bug的分支上新建一个分支Debug001

8.在Debug001上修复Bug

9.修复后在Bug分支上合并然后删除Debug001分支

10.最后切回dev分支，调出存储，继续开始工作。

## 保存工作现场

>$ git stash

## 查看保存的工作现场

>$ git stash list

## 恢复stash内容但不删除

>$ git stasg apply

## 删除stash

>$ git stash drop

## 恢复stash的同时删除

>$ git stash pop

### 小结

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

git stash 会保存当前工作进度，会把工作区和暂存区的改动保存起来。

当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场；

在master分支上修复的bug，想要合并到当前dev分支，可以用git cherry-pick <commit>命令，把bug提交的修改“复制”到当前分支，避免重复劳动。

# Feature分支

软件开发中，总有无穷无尽的新的功能要不断添加进来。添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。

# 多人协作

## 多人协作的工作模式

> 首先，可以试图用>$ git push origin <branch-name>推送自己的修改；
  
>如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

>如果合并有冲突，则解决冲突，并在本地提交；

>没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
  
>如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。
  
查看远程库信息

>$ git remote -v；

>本地新建的分支如果不能推送到远程，对其他人就是不可见的；

>从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；

>在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；

>建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；

>从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

> **因为这里开始学习的时候比较混乱，所以可能在笔记上记录的啰嗦了一些，我也就不另外修改了，一并放过来**

# Rebase

>这一节没有参看廖雪峰老师的教程，因为没看懂。

[Rebase详解](https://www.cnblogs.com/pinefantasy/articles/6287147.html)

