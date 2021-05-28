# Study Git Flow

这个仓库用于学习 Git Flow 开发模式  
参考[阮一峰教程](https://www.ruanyifeng.com/blog/2015/12/git-workflow.html)

### Git三种广泛使用的工作流程

> 1. Git Flow
> 2. Github Flow
> 3. Gitlab Flow


#### 1.Git Flow

该流程存在两个长期分支
> 1. master主分支
> 2. develop开发分支

master分支用于对外发布版本，所以该分支所有提交都应该具有tag并且是稳定版本；  
develop分支用于日常开发，存放最新的开发版本

其次是三种短期分支
> 1. feature功能分支
> 2. hotfix补丁分支
> 3. release预发布分支

feature功能分支用于开发特定功能，是从develop分支上分出来的，最后在合并进develop

```git
#创建feature分支，推送到远程仓库
git checkout -b feature develop
git push -u orgiin feature
#进行功能开发。。。
#开发完成进行合并
git checkout develop
git merge --no-ff feature
#合并完成后删除分支
git branch -d feature
git push origin --delete feature   
```



hotfix补丁分支用于修复bug

