# git操作手册
## 本地repo的常规操作
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
## 由本地repo关联远程repo
1. 在github建立repo
2. 在git bash相应目录下关联
git remote add origin git@github.com:hl-matrix/learngit.git
3. 将分支信息提交到远程repo
git push -u origin master
git push origin master
## 建立远程repo，克隆到本地的文件系统中（保存有.git）
1. 在git bash中cd到目标目录下
cd git
2. clone到文件系统中的目录下，目录名为（远程repo的名字），带有.git
git clone git@github.com:hl-matrix/gitskills.git
3. 在git bash中cd到克隆的文件目录下执行本地操作
