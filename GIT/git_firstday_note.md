1.git log --online和git log --pretty=oneline两个命令之间的区别是什么?

前者只显示7位的commitId,后者全部显示commitId.除此之外没有别的区别

前者只显示7位的commitId,后者全部显示commitId.



2.版本回退.

git reset --hard HEAD回退到当前版本,也就是上次commit的版本.

git reset --hard HEAD^回退到上一个提交的版本

git reset --hard HEAD^^回退到倒数第二个提交的版本,以此类推

git reset --hard HEAD commitId 跳转到指定id的那个版本


![1601126394239](C:\Users\ADMINI~1\AppData\Local\Temp\1601126394239.png)


3.git reflog显示命令历史,之前操作命令的历史

git log是提交历史,显示commit的历史记录




4.git上传文件踩坑

出错:! [rejected] master -> master (fetch first) error: failed to push some refs to ' 。。。' 

因为所要上传的github仓库中的readme文件不在本地仓库目录中,通过如下命令进行代码合并.

git pull --rebase origin master 

重新进行推送即可





5.git当中通过rm删除文件和直接在文件夹中删除文件有什么不一样吗?通过文件夹删除文件那么版本库中这个文件还存在吗?





6.git add .

表示添加所有文件到暂存区





7.如何修改最后一次commit时的备注?

git commit --amend    ----->      a   --------->   修改备注  -------->   esc   ---------->   shift+:   --------->  wq  

通过如上流程来进行最后一次提交时备注的修改

commit的时候必须写上备注,这是一个好的习惯





8.如何把暂存区的文件撤销到工作目录中?

git restore --staged a.js

git rm --cached a.js 

两者之间是等效的.





9.删除操作

已经commit的文件如何删除?   git rm a.js

在暂存区中的文件还没有commit如何进行删除?  git rm -f a.js





10.如何撤销所有的修改(未提交的)?

git checkout .







11.origin指的是仓库的地址,就算换成别的名字指向的也是同样的仓库地址.



12.github推送的权限问题.需要将公钥粘贴到远程的git库中.



13.删除git库中文件夹的操作

git rm -r js(删除js文件夹)

git rm -f index.js(删除index.js文件)















