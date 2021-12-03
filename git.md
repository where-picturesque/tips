### 日常操作


```
<!--拉取代码-->
git clone  git@/http://  //克隆仓库
git branch  //查看本地分支
git checkout branch-xxx  //切换至xxx分支
git checkout -b frontend-staging3 origin/frontend-staging3  //从远程仓库origin/frontend-staging3分支创建新分支frontend-staging3  并立即切换到新分支
git pull  //将与本地当前分支同名的远程分支 拉取到本地当前分支上(需先关联远程分支)


<!--代码提交-->
git status //查看当前状态
git add ./[文件名]  //暂存（所有、某文件）更改
git commit -m '备注'   //  提交到本地版本库
git commit --amend -m "add test container" // 修改提交，追加
git push [remoteName/origin] [localBranchName]  //推送到localBranchName分支到远程仓库的localBranchName同名分支
git push [remoteName/origin] [localBranchName]:[remoteBranch]  //推送到远程仓库

<!--代码合并-->
git checkout 被合并分支
git pull <origin> <远程分支>:<本地分支>  //拉取指定分支到本地分支
git pull <origin> <远程分支>  //将远程指定分支 拉取到 本地当前分支上
git merge 要合并的分支（mylocalBranchName）  //合并分支，切换到被合并分支，git merge 双向的
如果有冲突,解决冲突
git status
git add .
git commit -m 'merge'
git push orign frontend-staging3

git merge --abort //撤销合并

```
#### 回滚pull

```
git reflog  //查看版本
get reset --hard HEAD@{n}  //本地回退到对应版本，commit、merge都可使用

git reset --soft HEAD^   留下更改的代码
git push --force //如果已经push代码，想要回退远程代码版本，先回退本地版本，再把本地版本强制推送到远程分支，因为此时本地分支落后于远程。
```
#### 版本

```
git tag  //查看版本
git tag -r   //查看远程版本
git branch branch_0.1 master 从主分支master创建branch_0.1分支
```

```
git remote prune origin   //显示远程已被删除的分支
git branch -d <分支名>
```

#### 撤销操作
- git diff  未暂存的代码（未执行git add），可通过git diff 查看本地修改
- git checkout -- [filename | .] 撤销文件修改，且无法通过git找回，不可反悔。
- git diff --staged 查看暂存区修改(add 后)
- git reset . 撤销暂存区的修改
- git reset --soft HEAD^   撤回到指定提交，且留下更改的代码
- get reset --hard HEAD@{n}  撤回到指定提交，放弃修改

##### revert
reset是撤销连续的提交

revert可以撤销提交历史中的某次提交

```
git revert commitid //merge的ID 不需要revert，会提示无revert
git push //会生成新的commitID，原来的提交历史仍然存在
如果有冲突 add. commit push 解决冲突，或者 git revert -no-commit

```
撤销revert，则git revert （撤销操作生成的commitID）

## 子模块

初始化：git submodule update --init

切换分支 git submodule foreach git checkout dev


## rebase
合并commit

git rebase -i commitID(要合并目标的前一个commit)/HEAD~n(n=>合并几个commit)

会显示n次commit历史，pick 使用提交,squash 融合到上一个提交。如果几个commit都是pick，则不合并。
pick A;pick B;pick C

还可以更换commit的顺序： pick A;pick C;pick B

如果更改远程 git push origin branch --force

git log

git rebase --abort

git rebase master//在master最新commit点上提交当前分支的commit，不会按照commit时间重排顺序，且当前分支之前的commit hash会改变