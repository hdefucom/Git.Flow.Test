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

<img src="./Images/gitflow.png" alt="Git Flow 流程图示" width="600" />

***

> **feature**

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

***

> **hotfix**

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

***

> **release**

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

***

Git Flow 优点是清晰可控，缺点是分支过多相对复杂，需要长期维护两个分支，一般用于各种语言和框架。  
但是现在的web项目一般都会CI/CD，这种情况下，master分支和develop分支差别不大，没必要维护两个长期分支。
所以可以使用Github Flow

***

#### 2.Github Flow

Github Flow 是 Git Flow 的简化版本，专门配合CI/CD，它是Github的工作流程  
他只有一个长期分支`master`，相对于 Git Flow 简单了许多

<img src="./Images/githubflow.png" alt="Github Flow 流程图示" width="600" />

> 1. 先从`master`拉取新分支，不区分功能和补丁
> 2. 新分支开发完成后向`master`发起一个`Pull Request`
> 3. Pull Request既是一个通知，让别人注意到你的请求，又是一种对话机制，大家一起评审和讨论你的代码。对话过程中，你还可以不断提交代码
> 4. 你的Pull Request被接受，合并进master，重新部署后，原来你拉出来的那个分支就被删除。（先部署再合并也可。）

***

### 3.Gitlab Flow

Gitlab FLow 是 Git Flow 和 Github Flow 的综合，它吸收了两者的优点，既能适应不同开发环境的弹性，又有单一主分支的简单和便利  
它是Gitlab.com推荐的做法

Gitlab Flow 的最大原则叫`上游优先`，只存在一个`master`主分支，他是所有分支的上游，只有上游分支采纳的更改才能引用到其他分支。
它分为两种情况适应不同开发流程。

> **1. 持续发布**
>
> 建议在`master`分支外再建立 `pre-production` 和 `production` ，分别对应开发、预发、生产环境。  
> 上游 --> 下游  
> master --> pre-production --> production  
> 例如生产环境出现bug，新建一个分支先要合并到master，在逐步`cherry-pick`到下游。  
> 只有紧急情况，才允许跳过上游，直接合并到下游分支。

<img src="./Images/gitlabflowcicd.png" alt="Gitlab Flow 持续发布" width="400" />

***

> **2.版本发布**
> 
> 对于版本发布的项目，建议做法是每个稳定版本都从 `master` 分支拉出一个分支，如 `v1.0.0` `v1.1.0` 等。
> 以后，只有修复bug才允许将代码合并到这些稳定版本分支，并且需要更新小版本号。

<img src="./Images/gitlabflowversionpublish.png" alt="Gitlab Flow 版本发布" width="400" />
