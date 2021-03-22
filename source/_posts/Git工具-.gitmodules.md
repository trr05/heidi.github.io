---
title: Git工具.gitmodules
date: 2021-03-09 16:09:48
tags:
    - 开发工具
---
> 我们在项目目录中有时可能会见到这种文件.gitmodules
这个文件的应用场景：
> 某个工作中的项目需要包含并使用另一个项目，但又想两个项目同时独立

### 如何将一个项目作为另一个项目的子模块提交上去呢？
```
git submodule add 子模块的url
```
默认情况下 ，子模块会将子项目放到一个与仓库同名的目录中

### 克隆含有子模块的项目
按照正常的拉取代码的形式， 拉取下来的项目默认会包含子模块目录，但是目录内容为空
两种方式：
1. 运行两个命令：
```
git submodule init 用来初始化本地配置文件
git submodule update 从该项目中抓取所有数据并检出父项目中列出的合适的提交

```
2. git clone命令传递--recurse-submodules 选项，它就会自动初始化并更新仓库中的每一个子模块，包括可能存在的嵌套子模块

如果已经克隆了项目，但是忘记了--recurse-submodules，那么可以运行git submodule update --init将以上两个命令合并成一步。如果还要初始化、抓取并检出任何嵌套的子模块，可以使用git submodule update --init --recursive

### 在包含子模块的项目上工作
更新子模块：git submodule update --remote 子模块名字
加上子模块的名字可以更新固定的模块

### 推送
可以让Git在推送到主项目前检查所有子模块是否已推送
git push --recurse-submodules=check
如果任何提交的子模块改动没有推送那么“check“选项会直接使push操作失败
失败之后如何做？
进入到每一个子模块中然后手动推送到远程仓库，之后再次尝试这次推送
