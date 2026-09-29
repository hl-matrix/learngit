# git操作手册
## 一、本地repo的常规操作
1. 保存到暂存区  
git add file  
git add .
2. 提交到git分支  
git commit -m "messages"
3. 查看状态  
git status
4. 查看日志  
git log  
git reflog 
5. 修改HEAD指针  
git reset --hard HEDA^  
git reset --hard HDAD~10  
git reset --hard [commit id]
6. 撤销修改/删除后恢复（已经commit，在git分支中保存过）  
git checkout -- file
7. 从暂存区撤回  
git reset HEAD file
## 二、由本地repo关联远程repo
1. 在github建立repo
2. 在git bash相应目录下关联  
git remote add origin git@github.com:hl-matrix/learngit.git
3. 将分支信息提交到远程repo  
git push -u origin master  
git push origin master
## 三、建立远程repo，克隆到本地的文件系统中（保存有.git）
1. 在git bash中cd到目标目录下  
cd git
2. clone到文件系统中的目录下，目录名为（远程repo的名字），带有.git  
git clone git@github.com:hl-matrix/gitskills.git
3. 在git bash中cd到克隆的文件目录下执行本地操作
## 四、分支操作
1. 创建并切换分支  
git checkout -b dev  
git switch -c dev
2. 查看分支  
git branch
3. 切换分支  
git checkout master  
git switch master
4. 合并分支  
git merge dev  
5. 删除分支  
git branch -d dev
6. 不同分支产生冲突时，无法合并，需要先解决冲突，再commit到主分支上。
7. 查看分支合并图  
git log --graph
## 五、工作中的分支管理
**工作模式：**  
在工作中，master分支一般是稳定的，用来做最后的软件发行版本提交。
团队内部创建一个公共分支dev用来合并各成员的工作部分，各成员各自创建自己的分支，做自己的模块工作，统一合并到dev分支上，最后整体讨论，通过，合并到master分支上   
**场景/问题：** 在dev分支工作任务未完成，收到改动master分支的bug。  
**思路：**
> 1. 希望回到master分支上并创建另一个分支用来修改bug，合并到master后，删除该分支。  
> 2. 在回到master之前，对于当前分支上未完成的工作需要先保存下来，修完bug后恢复。  

**具体操作：**  
一. 保存断点，用于恢复现场。
> 1. 保存现场：  
> git stash
> 2. 产看断点列表  
> git stash list  

二. 回到master分支，创建新分支，并修改bug
> 1. 创建新分支  
> git switch -c issue
> 2. 修改bug，add 并 commit  
> 3. 回到master分支，合并新分支到master上  
> git merge issue  
> 4. 删除修bug的分支  
> git branch -d issue
 
三. 回到dev分支重新工作  
> 1. 查看储存列表  
> git stash list  
> 2. 恢复现场  
> git stash pop：恢复并从list中删除痕迹  
> git stash apply **现场版本** ，git stash drop：从list中删除痕迹。

四. 在dev分支中完成相关bug的修改
> 1. 由于dev分支最早是基于master分支，在master分支中修改了bug，在dev分支中显示仍然还没有修改，此时无需重复修改一遍bug。
> 2. git cherry-pick **修改bug的版本号**：可将修复的工作复制到dev分支下，并自动完成一次提交，两次修改不是同一个，类似复制。
> 3. 此时继续自己未完成的工作，所有的完成后，add并且commit。
> 4. 回到master分支，合并dev分支上的内容，此时包括bug的修改和自己的模块工作。
