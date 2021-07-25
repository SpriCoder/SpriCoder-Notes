# 酒店管理系统

<!-- TOC -->

- [酒店管理系统](#酒店管理系统)
  - [Git规范](#git规范)
    - [开发规范](#开发规范)

<!-- /TOC -->

## Git规范

分支的命名限定在以下范围(master | dev | develop | release | feature/xxx | hotfix/xxx | fix/xxx ) xxx为任意内容

Eg. 1.feature/酒店信息管理    2.hotfix/订单流程更改 

每次commit时，添加的描述信息需要有一个特定的前缀，限定在以下范围(feat|doc|test|docs|chore|refactor|fix|style| perf): xxx    注意冒号后面有一个空格

Eg. 1.feat: 查看酒店信息功能完成  2.fix: 浏览酒店bug修复

以上限定是为了帮助同学们尽早熟悉GitFlow开发模式，关于GitFlow的更多信息，可以参考以下链接或自行谷歌百度

[https://github.com/xirong/my-git/blob/master/git-workflow-tutorial.md#23-gitflow%E5%B7%A5%E4%BD%9C%E6%B5%81](https://github.com/xirong/my-git/blob/master/git-workflow-tutorial.md#23-gitflow工作流)



### 开发规范

只有release分支可以进行Test环境部署，clone项目之后新建release分支

~~~bash
git checkout -b release
git add .
git commit -m 'feat: xxx'
git push --set-upstream origin release
~~~

