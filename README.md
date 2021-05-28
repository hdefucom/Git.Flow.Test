# Study Git Flow

这个仓库用于学习 Git Flow 开发模式  
参考[阮一峰教程](https://www.ruanyifeng.com/blog/2015/12/git-workflow.html)

### Git三种广泛使用的工作流程

> 1. Git Flow
> 2. Github Flow
> 3. Gitlab Flow

***

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

<img src="./gitflow.png" alt="Git Flow 流程图示" width="600" />

feature功能分支用于开发特定功能，是从develop分支上分出来的，最后在合并进develop分支  
可以采用feature-*的命名形式

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

hotfix补丁分支用于修复bug，是从master分支上分出来的，最后在合并进master和develop分支  
可以采用fixbug-*的命名形式

```git
#创建hotfix分支，推送到远程仓库
git checkout -b fixbug master
git push -u orgiin fixbug
#进行bug修复。。。
#修复完成进行合并
#合并到master，版本号一般为三段，bug修复一般迭代最后一段版本号
git checkout master
git merge --no-ff fixbug
git tag -a v0.1.x
git push --tags
#合并到develop
git checkout develop
git merge --no-ff fixbug
#合并完成后删除分支
git branch -d fixbug
git push origin --delete fixbug   
```

release预发布分支用于发布正式版本前测试修复bug等工作，是从develop分支上分出来的，最后合并进master和develop分支
可以采用release-*的命名形式

```git
#创建hotfix分支，推送到远程仓库
git checkout -b release develop
git push -u orgiin release
#进行测试和bug修复。。。
#测试修复完成进行合并
#合并到master，版本号一般为三段，release一般迭代前两段版本号
git checkout master
git merge --no-ff release
git tag -a vx.x.0
git push --tags
#合并到develop
git checkout develop
git merge --no-ff release
#合并完成后删除分支
git branch -d release
git push origin --delete release   
```


