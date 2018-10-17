# QOS开发者社区

本文介绍了 QOS 开发者社区生态建设情况。

## 一、社区简介

QOS开发者社区，为开发者搭建从创新到商业应用的桥梁。QOS 开发者社区是一个 QOS 开发爱好者的聚集地，QOS 开发者社区将给所有的开发者提供一个任何人都可以参与贡献的开源社区。社区的宗旨是打造完善、自由、民主的公链生态平台。

## 二、开发平台

QOS开发团队选择 GitHub 作为代码托管平台，同时也是开发协作平台，它提供的大量易用、贴心的功能来适应不同规模的团队进行协作开发。

> GitHub 于 2008 年 4 月 10 日正式上线，除了 Git 代码仓库托管及基本的 Web 管理界面以外，还提供了订阅、讨论组、文本渲染、在线文件编辑器、协作图谱（报表）、代码片段分享（Gist）等功能。目前，其注册用户已经超过千万，托管版本数量也是非常之多，其中不乏知名开源项目ethereum、fabric等。

## 三、项目现状

目前 QOS 项目的多个子项目已经进入开发阶段，代码已经在 GitHub 上开源，关于项目的所有进展都可以在这个地址[https://github.com/QOSGroup](https://github.com/QOSGroup)查阅

GitHub主页截图
![img](https://raw.githubusercontent.com/QOSGroup/static/master/qosgroup-github.png)

子项目简介：

* qbase

  QOS区块链通用框架,实现了通用的存储、交易和QCP跨链协议,可以基于此框架开发QOS公链和其他联盟区块链

* qos

  基于qbase实现的qos公链，实现QOS基础双层代币和QOS激励机制，代币发行、转账等交易，并支持QCP跨链协议

* qstars

  QOS 联盟链及公链SDK

* cassini

  Cassini 是以QCP协议为基础实现的跨链交易中继服务，实现对异构区块链跨链交易的获取、验证和共识等中继支持

随着社区的进一步发展壮大，预计还会有很多新的子项目加入，敬请关注。

## 四、加入社区

开发者可以在[QOSGroup](https://github.com/QOSGroup)主页中任意选择一个感兴趣项目参与进来。

在 GitHub 页面中，有多种参与方式

* 报告代码、文档中出现的Bug
* 建议新的程序功能特性
* 领取新手任务
* 修复Bug，提交新代码
* 完成新功能特，提交新代码

Issues主页截图
![img](https://raw.githubusercontent.com/QOSGroup/static/master/qosgroup-issue.png)

`good first issue`: 新手任务，实现起来相对比较简单，适合新开发者快速熟悉社区的协作流程

## 五、新手上路

本节内容会详细描述开发者怎么成为社区的代码贡献者

### 1. 注册GitHub账号

首先必须是 GitHub 的注册用户，打开[GitHub](https://github.com)，按照页面向导即可完成

### 2. Fork项目代码

在[QOSGroup](https://github.com/QOSGroup)主页中选择一个感兴趣项目，然后点击Fork按钮即可

![img](https://raw.githubusercontent.com/QOSGroup/static/master/qosgroup-qbase.png)

### 3. 选取任务

从新手任务中，选取一个Issue来实现

![img](https://raw.githubusercontent.com/QOSGroup/static/master/qbase-issue.png)

### 4. 打开文件

在自己的 GitHub 主页，找到qbase仓库，在页面中打开文件`docs/transction_design.md`，并点击修改按钮

![img](https://raw.githubusercontent.com/QOSGroup/static/master/qbase-doc-tx.png)

### 5. 修改代码

按照Markdown的语法对文档进行修改，然后提交

![img](https://raw.githubusercontent.com/QOSGroup/static/master/qbse-commit.png)

注：完成上一个步骤后，就会自动调到一个创建PR的页面，默认是向自己的仓库创建合并请求，这不是我们的本意，直接点击`Code`标签忽略这个页面

### 6. 创建合并请求（Pull Request）

这时候，页面会主动提示用户创建合并请求

![img](https://raw.githubusercontent.com/QOSGroup/static/master/qbase-create-pr.png)

在这个页面，点击`Compare & pull request`按钮即可创建合并请求，然后填写一些说明信息，再点击`Create pull request`就完成了第一次代码贡献

![img](https://raw.githubusercontent.com/QOSGroup/static/master/qbase-open-pr.png)

### 7. 查看合并请求（PR）

在这个页面，GitHub会自动进行CI验证和覆盖率的统计，项目核心开发者会在这儿对修改的代码进行review，如果代码没问题的话，管理员会把修改合并到主干分支。

![img](https://raw.githubusercontent.com/QOSGroup/static/master/qbase-ci-pr.png)

下图是一个代码覆盖率的报告

![img](https://raw.githubusercontent.com/QOSGroup/static/master/qbase-cov-pr.png)

一般情况下，代码合并请求（PR）会很快被核心开发者处理、合并。如果提交的代码有问题的话，核心开发者会对代码进行注释，告诉PR的提交者需要怎么修改代码，然后再重新提交。

### 8. 完成合并请求（PR）

下图是已经合并的PR状态

![img](https://raw.githubusercontent.com/QOSGroup/static/master/qbase-merged-pr.png)

恭喜，到这里，你完成了第一个PR，已经成为开源社区的代码贡献者了！

## 六、高手进阶

上一节的内容是描述直接利用GitHub页面提供的功能进行代码贡献，但是大多数情况下，如果想对代码更深入的修改和调试的话，还是需要用到命令行工具，大家下一步要做的就是熟悉git工具的使用
