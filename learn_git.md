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
