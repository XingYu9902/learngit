## Git的三种状态


## 创建版本库
  >在Windows系统下，尽量确保目录名没有中文，防止发生奇怪的错误。

  >1.cd d:  进入d盘

  >2.mkdir \<repository-name\>  创建库
  
  >3.cd \<repository-name\> 进入库内
  
 >补充， pwd命令显示当前目录路径, ls显示当前目录，ls -ah显示隐藏目录
 
 ## Git配置
 在下载安装好git后，需要对Git进行配置
 >$ git config --global user.name "Your Name"          Your Name为GitHub用户名
 
 >$ git config --global uesr.email "email@example.com"      email为Github的注册邮箱

## 将文件添加到版本库
### 使用vi编辑器
>1.vi \<file-name\> 创建、修改文件

>2.按i进入编辑模式

>3.编辑完成按ESC，选择一下命令操作：

![1](https://github.com/XingYu9902/learngit/blob/master/images/dasda.png)

>查看文件内容 cat \<file-name\>

>4.git add \<file-name\>

>5.git commit -m "描述"

>注意，可以先多次`git add`,最后一次`git commit`
