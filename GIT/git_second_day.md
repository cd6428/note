1.远程分支和本地分支![1601263248469](C:\Users\ADMINI~1\AppData\Local\Temp\1601263248469.png)

(1)远程有origin/dev分支,本地有dev分支,使用git branch --set-upstream dev origin/dev命令建立两者之间的联系

(2)远程有origin/dev分支,本地没有,可以使用git switch -c dev origin/dev指令创建本地的dev分支,并且两者之间建立联系

(3)本地有dev分支,远程没有,可以使用git push origin dev向远程仓库推送dev分支,远程仓库会创建一个dev分支,与本地dev分支相互联系







2.情境:从主分支上创建一个dev分支,在dev分支上面修改某一个文件,回到主分支合并,并不会发生冲突问题,git会使用fast/faward模式来快速合并,但是如果回到主分支后如果刚好更改了这个文件的同一个地方并且提交,再去合并dev分支,那么这个时候也许就会发生冲突,手动解决冲突,并且提交.





3.什么样的情况下会发生冲突?

(1)如上所述,分支合并,如果你想查看分支的合并情况可以使用指令git log --graph --oneline指令

使用(git rm -r 文件夹名)指令可以删除git仓库中的文件夹  

(2)当你向远程仓库push时,也许会提示报错,因为你有可能和你的同事更改了某个文件的相同位置的代码,此时你是push不上去的,所以先git pull拉取远程仓库最新的代码,此时会提示冲突,手动解决冲突,提交,重新push.





4.例如bootstrap项目,我们如何克隆并且提交自己的修改?

首先进入bootstrap的项目地址,点击右上角的fork按钮,在自己的github账号下克隆一个bootstrap项目,之后从自己的账号下克隆bootstrap项目至本地,不能直接从bootstrap的项目地址直接克隆至本地,因为没有权限,修改之后无法push,当从自己的github地址上克隆bootstrap至本地后可以修改并且正常push到自己的远程仓库中,如果你希望bootstrap可以接受你的修改你可以发起一个pull request请求,但是对方是否接受这就不一定了.





5.git remote -v查看与远程库的关联信息

git remote rename origin abc把远程库名称由origin修改为abc

git remote remove origin删除远程库名称





6.分支相关指令

git branch 查看当前分支状态

git branch dev创建dev分支

git switch dev切换到dev分支

git switch -c dev创建并且切换到dev分支

git merge dev合并dev分支(注意合并的主次关系,只有在主分支上合并次级分支)

git branch -d dev删除dev分支

git branch -D dev强制删除dev分支





7.配置相关的用户信息

git config --global user.name 'xxx'

git config --global user.email 'xxx'

查看配置信息git config --list

