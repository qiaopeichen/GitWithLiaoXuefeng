git branch -a：查看所有分支
git status：查看修改状态
git diff：查看细节差异
git checkout --force：强制把远程更新到本地，会覆盖本地文件 //存疑
git tag：查看以往版本，然后git checkout 历史版本名
gitk：图形化界面
git checkout 分支名：切换分支
git reset --soft HEAD~1：撤销commit
git clean -df 清除本地添加的不同文件
git add -u 仅提交修改过和删除的文件，忽略自动添加的文件
git push origin master:refs/for/master 将commit后的文件提交到某个分支上（例如master）

/**王哲 start*/
git fetch --all 把服务器上别人更新的代码down下来
git reset --hard origin/master
git pull //直接覆盖本地

git stash 保存当前代码
git pull 将服务器代码拉下来
git stash pop 将刚才保存的代码和服务器拉下来的代码合并
/**王哲 end*/

2018/03/07
git提交到网页上的代码后，发现有问题需要重新提交，
1.修改本地需要重新改的文件
2.git commit  --amend  这里加-m的话 不规范，加了-m就多提交了一条
3.git push 推代码

git文件夹上面的蓝色加号 意思是add了 但还没有commit

提交顺序：
git add 
git commit 
git pull
git push


git pull
如果失败
git stash
git pull
git stash pop



git add .
git commit -m ""

git pull --rebase
/**乔培宸*/
Your branch is ahead of 'origin/branch_Amigo_StoryLocker_1.5.0' by 2 commits.
$ git reset --soft HEAD~1
$ git commit -m "254906 重构Preference" --amend
$ git push origin branch_Amigo_StoryLocker_1.5.0:refs/for/branch_Amigo_StoryLocker_1.5.0


git status
git add -u
git add <filename>
git commit -m "254906 demo"
git push origin branch_Amigo_StoryLocker_1.5.0:refs/for/branch_Amigo_StoryLocker_1.5.0

git stash
git pull --rebase
git stash pop
git commit --amend
git push origin branch_Amigo_StoryLocker_1.5.0:refs/for/branch_Amigo_StoryLocker_1.5.0

git reset --soft HEAD~1 // 撤销 commit
git reset HEAD // 撤销add

git add .  // 所有添加、修改的文件，不包括删除的文件
git add -u // 仅监控已经被add的文件 (update)
git add -A // 上面两个功能的合集

/**廖雪峰*/
git log --pretty=oneline //单行打印log
commit id //版本号 通过SHA1算法计算出来的16进制数
HEAD //表示当前版本
git reset --hard HEAD~1 // 回退到上一个commit版本
git reset --hard 3628164 // 指定回到某个版本号的版本
git reflog // 查看所有分支的所有操作记录，包括已经被删除的commit记录
现在总结一下：
  ● HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。
  ● 穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
  ● 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。
git diff // 工作区和暂存区的比较 work dict  stage
git diff --cached // 暂存区和分支的比较 stage  master
cat <filename> // 打开某文件
git checkout -- <filename> // 丢弃工作区的修改，回到最近一次commit或add时的状态
如果当前没到暂存区，就回到版本库状态
如果已经到暂存区又修改，就回到暂存区状态。
// 其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除。

git checkout <branch>//切换某一分支
git reset HEAD // 把暂存区的修改回退到工作区

又到了小结时间。
场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。
场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

git checkout -b dev
// 创建并切换到dev分支，相当于以下两个命令 git branch dev + git checkout dev
git merge <branchname> // 将指定分支合并到当前分支
git branch -d <branchname> // 删除某分支

Git鼓励大量使用分支：
查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>
创建+切换分支：git checkout -b <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name>

小结
当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
用git log --graph命令可以看到分支合并图。

/**20180312*/
git stash save -a ""
git stash pop stash@{id}  pop出来，并且删除stash
git stash apply stash@{id} pop出来，不删除stash
git stash drop stash@{id}
git stash clear 删除所有stash
git stash show 查看当前 stash 状态
git reset --soft 将HEAD重置到某一个commit，缓存区和工作区不变，原HEAD和重置后所有的变更集都放在stage区
git reset --hard 重置HEAD到某一个commit，重置index以便反应HEAD的变化，重置working copy，你所有的本地修改将丢失。/*如果我们希望彻底丢掉本地修改但是又不更改branch所指向的commit，则执行git reset --hard = git reset --hard HEAD*/
git reset --mixed 默认参数，重置HEAD到另外一个commit，并且重置index以便和HEAD相匹配，working copy不会被更改，HEAD和重置后所有变更将作为local modifications保存在working area中，被标识为local modification or untracked via git status，但是并未staged的状态，可以中心检视然后再做修改和commit。

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

git 创建远程分支：前提：本地有dev分支，然后 git push orgin dev 。即可创建git远程分支

2018-3-15
p4merge:
 灰色：共同基版本 
 黄色：别人的
 绿色：我的
git log --author=qiaopc

// 修改颜色
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

