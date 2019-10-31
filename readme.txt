## 指令集合
>$ mkdir learngit  创建一个仓库<learngit>
>$ cd learngit       进入仓库内
>
>**pwd**命令用于显示当前目录。
>**ls**显示当前目录
>**ls -ah**显示隐藏目录

>**git add** 将文件添加到暂存区（stage）
>**git commit -m** 将文件添加到仓库（Repository）
>**git diff** 比较的是工作区文件与暂存区文件的区别
>**git diff --cached** 比较的是暂存区的文件与仓库分支里（上次git commit 后的内容）的区别
>**git diff HEAD -- filename** 比较工作区和仓库分支里的区别
>**git status** 掌握仓库当前状态
>**git reset --hard HEAD^** 回退到上一个版本
>**git reset --hard HEAD^^** 回退到上二个版本
>**git reset --hard commit_id** 回退commit_id版本
>**git log** 查看提交历史，以便确定要回退到哪个版本
>**git reflog** 查看命令历史，以确定要回到未来的哪个版本
>**git checkout -- filename** 把filename文件在工作区的修改全部撤销，有两种情况。（--很重要）
