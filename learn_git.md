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
