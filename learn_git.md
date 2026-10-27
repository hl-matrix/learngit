# git学习手册
## 一. 创建版本库
### 操作步骤
1. 在指定目录打开git bash  
2. 初始化：  
`git init`  
3. 定义个人信息：  
`git config --global user'name "你的名字"`  
`git config --global user.email "你的邮箱地址"`  
`--global参数：定义本地电脑的所有本地库同样的name和email`
4. 将工作区的文件输出到暂存区  
`git add .`  
`git add file1 file2...`
5. 提交并添加说明   
`git commit -m "说明信息"`
## 二. 时光机穿梭
### 操作步骤
1. 版本库回退到之前的版本（commit id）  
`git reset --hard (commit id)`  
`git reset --hard HEAD^`  
`git reset --hard HEAD~1`  
2. 撤销修改  
场景一: 在工作区修改,未stage到暂存区  
`git restore file`  
在工作区撤销修改  
场景二: 在工作区修改,并且stage到暂存区,但还未commit  
`git restore --staged file`  
撤回add操作,保留在工作区的状态,依然是修改后的file,即回到场景一  
3. 删除文件  
删除文件  
`rm file`  
场景一：希望删除  
`git rm/add file`  
`git commit -m "删除file"`  
场景二：后悔删除，希望撤销  
`git restore file`  
前提：前面的版本已经在分支中，即已经commit过，在.git的track下  
## 远程仓库
### 操作步骤
#### 本地库 -> 远程库
1. 在github建立远程仓库，即create a repo。
2. 将本地库关联到远程仓库  
`git remote add origin git@github.com:user's name/repo's name.git`  
3. 初次推送内容时  
`git push origin -u master`  
注：参数-u，是指--set-upstream  
#### 远程库 -> 本地库
1. 在github新建一个远程库，即create a repo。
2. 在本地克隆一个远程库，便于完成个人的模块化任务。  
`git clone git@github.com:user's name/repo's name.git`  
## 分支管理
### 理念
在团队协作的软件工程中，一般主干是稳定的，用于最终更新和提交软件版本，个人在主干外各自建立自己的分支，完成个人的模块化工作。
### 操作步骤
#### 分支的创建和合并
1. 创建并转移到新的分支  
`git switch -c dev`  
注：参数-c，是--create的缩写  
2. 观察创建的所有分支  
`git branch`  
3. 对于1的步骤同样可以拆解  
建立新的分支但不切换  
`git branch main`  
切换到新的分支  
`git switch main`  
4. 删除分支  
`git branch -d main`  
注：参数-d，是--delete的缩写  
5. 在分支中完成相关任务时，需要add和commit，因为git是记录修改；然后切换到主分支，再合并  
**假设**：在dev分支中完成相关工作后，需要合并到主干master上，需要先切换到master主干上  
git merge dev  
注：默认是采用fast forward快速合并，结果是回看历史（git log）时，看不出切换分支，合并的显式操作过程，仍呈现出笔直的时间线。  
6. 分支管理策略，不采用ff的快速合并  
`git merge --no-ff -m "提交说明" dev`  
注：可以显式的看出修改痕迹。  
7. 查看日志  
#### 处理bug
**场景**：我正在完成工作任务（离结束遥遥无期），但突然收到市场的紧急反馈，急需修复一个在master分支上的bug，此时我是在我创建的分支上完成我的工作，面临不能退出我的分支（因为在自己的分支上一定要add和commit再退出，不要徒增麻烦），又要在别的分支上修改的两难境遇。  
**方法**：保存自己分支的断点现场，退出到别的分支完成任务后，再返回自己的分支，恢复现场后继续工作  
1. 
