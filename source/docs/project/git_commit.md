title: Git 规范
---

## 分支管理

- 管理员从 `develop` 创建 feature-* 分支，注意此处需将该分支置为 `Protected`
- 开发人员参考 【Merge Request 流程/规范】将项目 Fork 到本地，之后根据功能点提交，并发起 Merge Request
- 相关人员（管理员、项目负责人）进行 `Code Review`，将代码合并到 feature-* 分支
- 提测时，由管理员将 feature-* 分支合并到 `develop` 分支，开始自测
- 自测完成后，将 develop 分支合并到 `release` 分支，然后构建测试环境
- 测试通过，将 release 分支合并到 `master` 分支，由测试人员进行回归
- 上线时，由管理员根据上线日期添加 `Tag`，eg. '20180101'
- 最后，管理员将 master 分支合并到 `develop`

## 线上问题修复流程

- 管理员从 `master` 创建 hotfix-* 分支，注意此处需将该分支置为 `Protected`
- 开发人员参考 【Merge Request 流程/规范】将项目 Fork 到本地，之后根据功能点提交，并发起 Merge Request
- 相关人员（管理员、项目负责人）进行 `Code Review`，将代码合并到 hotfix-* 分支
- 提测时，直接在 hotfix-* 分支发版测试
- 测试通过，将 hotfix-* 分支合并到 `master` 分支，由测试人员进行回归
- 上线时，由管理员根据上线日期添加 `Tag`，eg. '20180101'
- 最后，管理员将 master 分支合并到 `develop`

## 提交规范

Commit Message 第一行的提交类型必须是以下类型之一：`feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `chore`, `revert`

### feat -- 实现新功能(feature)

当新需求或新功能的实现完成并测试通过时，开发人员需提交该部分变更的代码，并且按照上述的 Commit Message 格式编写提交注解。

E.g: `feat: add listView components to bill search page`

### fix -- 解决bug

当Bug修复完成并确认已经彻底解决时，开发人员需提交该部分变更的代码，并且按照上述的 Commit Message 格式编写提交注解。 

E.g.1: `fix: when submit button has ever been triggered, do not trigger again.(#1871)` 
E.g.2: `fix: fix the NullPointException when updating bill.(#1891)`

### docs -- 只针对文档(documention)变更

如果提交的改动只是针对文档的变更，则提交类型可以设为 `docs`。

E.g: `docs: add the document of Git Commit Message Guideline`

### style -- 代码样式(style)变更(格式化代码，不影响代码原意)

如果提交的改动只是针对代码样式或者格式的变更，则提交类型可以设为 `style`。

E.g: `style: reformat service layer code`

### refactor -- 代码重构(refactor)(既不是解决bug也不是实现新功能)

如果提交的改动是针对代码重构的，则提交类型可以填写为 `refactor`。

E.g: `refactor : refactor default search function`

### test -- 添加缺少的测试(test)代码

添加的代码为测试相关的代码，则提交类型可以填写为 `test`。

E.g: `test: add unit test for user login function`

### perf -- 优化系统性能(performance)

若提交的改动是针对系统性能的优化的，则提交类型填写为 `perf`。

E.g: `perf: improve the performance of filtering the required bill list`

### chore -- 针对构建过程或者辅助工具的变更

chore: 日常零碎变更，这里主要是针对构建过程、辅助工具、抑或是其他无关主题代码的变更。

E.g: `chore: add css preprocessor trees`

### revert -- 回滚提交

如果当次提交是为了还原上一次提交，那么提交的消息需要以 `revert: ` 开头，后面跟着要还原的提交的消息头。消息体的内容可以描述为：`This reverts commit <要还原的提交的hash编码>`。

## Merge Request 流程/规范

- 打开 `<group>/<project>`，fork项目到自己的个人中心

- clone自己个人中心的项目到本地

```bash
$ git clone http://git.jc/<自己的用户名>/<project>.git
```

### 本地关联

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

如果 rebase 失败，可以退出 rebasing 状态，使用命令

```bash
$ git rebase --abort
```

### 示例

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

### Tips

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
