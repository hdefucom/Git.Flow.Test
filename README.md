# Study Git Flow

����ֿ�����ѧϰ Git Flow ����ģʽ  
�ο�[��һ��̳�](https://www.ruanyifeng.com/blog/2015/12/git-workflow.html)

### Git���ֹ㷺ʹ�õĹ�������

> 1. Git Flow
> 2. Github Flow
> 3. Gitlab Flow


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

feature���ܷ�֧���ڿ����ض����ܣ��Ǵ�develop��֧�Ϸֳ����ģ�����ںϲ���develop

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



hotfix������֧�����޸�bug

