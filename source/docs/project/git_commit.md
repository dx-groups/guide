title: Git 提交规范
---

## 提交类型

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
