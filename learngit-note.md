## Git的三种状态
Git有三种状态、你的文件可能处于其中之一：**已提交（committed）、已修改（modified）和已暂存（staged）**。**已提交**表示数据已经安全的保存在本地数据库中。**已修改**表示修改了文件，但还没有保存到数据库中。**已暂存**表示对一个已修改文件的当前版本做了标记，使之包含在下一次提交的快照中。由此引入Git项目的三个工作区域的概念：Git仓库、工作目录以及暂存区域。

![2](https://github.com/XingYu9902/learngit/blob/master/images/Snipaste_2019-10-31_18-03-08.png)

>Git仓库目录时Git用来保存项目的源数据和对象数据库的地方。这是Git中最重要的部分，从其它计算机克隆仓库时，拷贝的就是这里的数据。

>工作目录是对项目的某个版本独立提取出来的内容。这些从Git仓库的压缩数据库中提取出来的文件，放在磁盘上供你使用或修改

>暂存区域是一个文件，保存了下次将提交的文件列表信息，一般在Git仓库目录中。有时候也被称作“索引”，不过一般说法还是叫暂存区域
![3](https://github.com/XingYu9902/learngit/blob/master/images/Snipaste_2019-10-31_17-56-26.png)
![4](https://github.com/XingYu9902/learngit/blob/master/images/Snipaste_2019-10-31_17-56-51.png)
![5](https://github.com/XingYu9902/learngit/blob/master/images/Snipaste_2019-10-31_18-57-03.png)

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
