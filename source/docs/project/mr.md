title: Merge Request 流程/规范
---

## Fork 项目

- 打开 `<group>/<project>`，fork项目到自己的个人中心

- clone自己个人中心的项目到本地

```bash
$ git clone http://git.jc/<自己的用户名>/<project>.git
```

## 本地关联

添加项目的源仓库

```bash
$ git remote add upstream http://git.jc/<group>/<project>.git
```

```bash
$ git remote -v

origin  http://git.jc/<自己的用户名>/<project>.git (fetch)
origin  http://git.jc/<自己的用户名>/<project>.git (push)
upstream  http://git.jc/<group>/<project>.git (fetch)
upstream  http://git.jc/<group>/<project>.git (push)
```

通过 `fetch & rebase upstram` 远程同步代码

push 到自己的远程然后通过 `Merge Request` 的方式合并到项目

我们用 `fetch + rebase` 的方式同步代码，这与 `fetch + merge（pull）` 的区别在于[http://stackoverflow.com/questions/28140434/is-there-a-difference-between-git-rebase-and-git-merge-ff-only](http://stackoverflow.com/questions/28140434/is-there-a-difference-between-git-rebase-and-git-merge-ff-only)

## 示例

- 团队的远程仓库：`upstream`
- 自己fork的远程仓库：`origin`
- 本地clone origin的仓库：`local`

**假设我们在 `feature-xxx` 分支开发，要开发一个新页面 `newPage`**

1. 同步 `local/feature-xxx` 和 `upstream/feature-xxx`、`origin/feature-xxx` 的代码

```bash
//提交你本地的代码
$ git:(feature-xxx) git add file
$ git:(feature-xxx) git commit -m message
//将你本地的分支与远程服务器分支合并
$ git:(feature-xxx) git fetch upstream
$ git:(feature-xxx) git rebase upstream/feature-xxx
$ git:(feature-xxx) git push origin feature-xxx
```
如果 `rebase` 期间遇到冲突，先解决冲突（`git add .`，不要`commit`），然后：

```bash
$ git:(feature-xxx) git add .
$ git:(feature-xxx) git rebase --continue
```

2. 新建特性分支 `local/feature-newPage`

```bash
$ git:(feature-xxx) git checkout -b feature-newPage
Switch to a new branch 'feature-newPage'
$ git:(feature-newPage)
```

3. 进行本地开发操作，完成第一个功能（或创建了需要的文件）
4. 把本地分支推送到`origin`

```bash
$ git:(feature-newPage) git push origin feature-newPage
Total 0 (delta 0), reused 0 (delta 0)
To http://git.jc/用户名/mobile.git
 * [new branch]      feature-newPage -> feature-newPage
```

5. 继续进行本地开发，频繁的commit，按合理的颗粒度推送到`origin`（推送前，适当的用`git reabse -i `美化commit），便于大家看到任务进度
6. 开发完成，同步到最新代码，推送`feature-newPage`到`origin`，并登录`gitlab`修改`merge request`的title，去掉`WIP`标示

```bash
$ git:(feature-newPage) git fetch upstream
$ git:(feature-newPage) git rebase upstream/feature-xxx
$ git:(feature-newPage) git push -f origin feature-newPage
```

7. 等待`merge`，并同步进行新的开发任务

## Tips

在`commit`过程中尽量做到按功能点提交代码，但是也要做到尽量勤快的`commit`，所以要用`git rebase`去做合并提交的工作(没有push之前一切都还来得及！！！)

假设离你上次push你有三次commit，但是你只有一个功能点

```bash
$ git log --graph --oneline --all

* 017d1f0 commit 4
* 1e46126 commit 3
* 4f4b2f6 commit 2
* 4887144 commit 1
```


```bash
$ git rebase -i HEAD~3
```

```bash
pick 4f4b2f6 commit 2
pick 1e46126 commit 3
pick 017d1f0 commit 4
```

```
# Rebase 4887144..017d1f0 onto 4887144 (3 command(s))
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
#
```

按照说明用`r`去编辑commit，`s`去合并之前的commit

```bash
pick 4f4b2f6 commit 2
s 1e46126 commit 3
s 017d1f0 commit 4
```
合并后新的commit记录：

```bash
$ git log --graph --oneline --all

* e41ef96 xxx-feature
* 4887144 commit 1
```
