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

<img src="./Images/gitflow.png" alt="Git Flow ����ͼʾ" width="600" />

***

> **feature**

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

***

> **hotfix**

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

***

> **release**

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

***

Git Flow �ŵ��������ɿأ�ȱ���Ƿ�֧������Ը��ӣ���Ҫ����ά��������֧��һ�����ڸ������ԺͿ�ܡ�  
�������ڵ�web��Ŀһ�㶼��CI/CD����������£�master��֧��develop��֧��𲻴�û��Ҫά���������ڷ�֧��
���Կ���ʹ��Github Flow

***

#### 2.Github Flow

Github Flow �� Git Flow �ļ򻯰汾��ר�����CI/CD������Github�Ĺ�������  
��ֻ��һ�����ڷ�֧`master`������� Git Flow �������

<img src="./Images/githubflow.png" alt="Github Flow ����ͼʾ" width="600" />

> 1. �ȴ�`master`��ȡ�·�֧�������ֹ��ܺͲ���
> 2. �·�֧������ɺ���`master`����һ��`Pull Request`
> 3. Pull Request����һ��֪ͨ���ñ���ע�⵽�����������һ�ֶԻ����ƣ����һ�������������Ĵ��롣�Ի������У��㻹���Բ����ύ����
> 4. ���Pull Request�����ܣ��ϲ���master�����²����ԭ�������������Ǹ���֧�ͱ�ɾ�������Ȳ����ٺϲ�Ҳ�ɡ���

***

### 3.Gitlab Flow

Gitlab FLow �� Git Flow �� Github Flow ���ۺϣ������������ߵ��ŵ㣬������Ӧ��ͬ���������ĵ��ԣ����е�һ����֧�ļ򵥺ͱ���  
����Gitlab.com�Ƽ�������

Gitlab Flow �����ԭ���`��������`��ֻ����һ��`master`����֧���������з�֧�����Σ�ֻ�����η�֧���ɵĸ��Ĳ������õ�������֧��
����Ϊ���������Ӧ��ͬ�������̡�

> **1. ��������**
>
> ������`master`��֧���ٽ��� `pre-production` �� `production` ���ֱ��Ӧ������Ԥ��������������  
> ���� --> ����  
> master --> pre-production --> production  
> ����������������bug���½�һ����֧��Ҫ�ϲ���master������`cherry-pick`�����Ρ�  
> ֻ�н���������������������Σ�ֱ�Ӻϲ������η�֧��

<img src="./Images/gitlabflowcicd.png" alt="Gitlab Flow ��������" width="400" />

***

> **2.�汾����**
> 
> ���ڰ汾��������Ŀ������������ÿ���ȶ��汾���� `master` ��֧����һ����֧���� `v1.0.0` `v1.1.0` �ȡ�
> �Ժ�ֻ���޸�bug����������ϲ�����Щ�ȶ��汾��֧��������Ҫ����С�汾�š�

<img src="./Images/gitlabflowversionpublish.png" alt="Gitlab Flow �汾����" width="400" />
