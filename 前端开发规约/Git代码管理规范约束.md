# Git代码管理规范约束

## 1. git commit message规范

```
# 主要type 
feat: 增加新功能 
fix: 修复bug 

# 特殊type 
docs: 只改动了文档相关的内容 
style: 不影响代码含义的改动，例如去掉空格、改变缩进、增删分号 
build: 构造工具的或者外部依赖的改动，例如webpack，npm 
refactor: 代码重构时使用 
revert: 执行git revert打印的message 

# 暂不使用type 
test: 添加测试或者修改现有测试 
perf: 提高性能的改动 
ci: 与CI（持续集成服务）有关的改动 
chore: 不修改src或者test的其余修改，例如构建过程或辅助工具的变动
```

### Commitizen工具使用

Commitizen是一个格式化commit message的工具

大量的代码提交，必然会产生大量的commit log，而每一次commit是阶段性的Ending，应记录着这一阶段所完成的事以及关注点，尽可能详细具体；且提供更多的历史信息，方便快速浏览；可以过滤某些commit（比如文档改动），便于快速查找信息；可以直接从commit生成Change log。所以log的格式就是关键所在，而Commitizen可以完美的解决这些问题。


## 2. gitflow规范

### 分支管理
- feature分支
- test分支
- master分支
- hotfix分支

### feature分支

feature分支, 也可以叫做个人分支，是从已发版的master分支checkout出来的新分支，代表了一个新的生产线，主要用来开发新的功能，团队同学都可以从master checkout自己的个人分支。

### test分支

test分支是用来提测的公共分支，当个人分支功能开发完成需要提测，有两种提测方式：

1. 如果代码跟版发布，需要先rebase test分支, 然后将个人分支推到远端，通过提MR的方式将个人分支合并到test分支提测

2. 如果个人分支代码需要单独发布，则需要从feature分支再checkout一个分支来做上面的操作，保证个人分支代码独立，方便测试通过后合并到master。

### master分支

master分支是用于发布生产的公共分支，需要保证绝对的安全，所以不要轻易的合并代码到master，正常情况下，当一个版本代码在test分支测试通过，发布生产都是从test分支全量合并到master分支，然后发布生产。

当存在需要独立发布的情况，测试通过后，则需要先rebase master到个人分支，再通过提MR合并到master。

### hotfix分支

hotfix分支与feature分支类似，也是从master拉取出来的个人分支，主要作用是做热修复，修复后的代码因为需要单独发布，所以要用第二种提测方式进行提测，测试通过后再合到master。

### 合并规则

- 通过rebase合并代码，本地避免merge操作
- 禁止本地操作test或master等公共分支
- 合并代码到公共分支需要通过MR进行Code Review

### SourceTree工具使用

SourceTree是Git代码管理可视化工具，有丰富的git命令可视化操作选择，方便查看git提交历史，分支提交合并详细情况。