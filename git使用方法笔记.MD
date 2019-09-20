### 简单命令

- 配置信息列表 git config --list
- git init 初始化本地仓库 第一次使用
- git status 查看文件状态 (红色就是没有添加到暂存区,绿色就是已经添加到了暂存区,绿色红色都没有(目前工作区文件都已提交到了本地仓库))
- git add 文件名 (将文件添加到 暂存区)
- git add . (将所有文件添加到 暂存区)
- git remote rm origin 重新定向地址
- git commit -m'提交信息' 暂存区内容 提交到本地仓库
- git remote add origin {url} 设置远程仓库地址 第一次使用的时候需要设置
- git push origin master 上传到远程仓库
  #### tips
- 一个本地仓库只对应一个远程仓库
