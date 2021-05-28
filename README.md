# Study Git Flow

����ֿ�����ѧϰ Git Flow ����ģʽ  
�ο�[��һ��̳�](https://www.ruanyifeng.com/blog/2015/12/git-workflow.html)

### Git���ֹ㷺ʹ�õĹ�������

> 1. Git Flow
> 2. Github Flow
> 3. Gitlab Flow

***

#### 1.Git Flow

�����̴����������ڷ�֧
> 1. master����֧
> 2. develop������֧

master��֧���ڶ��ⷢ���汾�����Ը÷�֧�����ύ��Ӧ�þ���tag�������ȶ��汾��  
develop��֧�����ճ�������������µĿ����汾

��������ֶ��ڷ�֧
> 1. feature���ܷ�֧
> 2. hotfix������֧
> 3. releaseԤ������֧

<img src="./gitflow.png" alt="Git Flow ����ͼʾ" width="600" />

feature���ܷ�֧���ڿ����ض����ܣ��Ǵ�develop��֧�Ϸֳ����ģ�����ںϲ���develop��֧  
���Բ���feature-*��������ʽ

```git
#����feature��֧�����͵�Զ�ֿ̲�
git checkout -b feature develop
git push -u orgiin feature
#���й��ܿ���������
#������ɽ��кϲ�
git checkout develop
git merge --no-ff feature
#�ϲ���ɺ�ɾ����֧
git branch -d feature
git push origin --delete feature   
```

hotfix������֧�����޸�bug���Ǵ�master��֧�Ϸֳ����ģ�����ںϲ���master��develop��֧  
���Բ���fixbug-*��������ʽ

```git
#����hotfix��֧�����͵�Զ�ֿ̲�
git checkout -b fixbug master
git push -u orgiin fixbug
#����bug�޸�������
#�޸���ɽ��кϲ�
#�ϲ���master���汾��һ��Ϊ���Σ�bug�޸�һ��������һ�ΰ汾��
git checkout master
git merge --no-ff fixbug
git tag -a v0.1.x
git push --tags
#�ϲ���develop
git checkout develop
git merge --no-ff fixbug
#�ϲ���ɺ�ɾ����֧
git branch -d fixbug
git push origin --delete fixbug   
```

releaseԤ������֧���ڷ�����ʽ�汾ǰ�����޸�bug�ȹ������Ǵ�develop��֧�Ϸֳ����ģ����ϲ���master��develop��֧
���Բ���release-*��������ʽ

```git
#����hotfix��֧�����͵�Զ�ֿ̲�
git checkout -b release develop
git push -u orgiin release
#���в��Ժ�bug�޸�������
#�����޸���ɽ��кϲ�
#�ϲ���master���汾��һ��Ϊ���Σ�releaseһ�����ǰ���ΰ汾��
git checkout master
git merge --no-ff release
git tag -a vx.x.0
git push --tags
#�ϲ���develop
git checkout develop
git merge --no-ff release
#�ϲ���ɺ�ɾ����֧
git branch -d release
git push origin --delete release   
```


