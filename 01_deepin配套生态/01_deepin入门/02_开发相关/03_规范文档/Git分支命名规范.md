---
title: Git 分支命名规范
description: 适用于 deepin 相关项目的分支命名规范文档
published: true
date: 2022-10-19T08:49:58.622Z
tags: 规范文档
editor: markdown
dateCreated: 2022-09-01T05:05:21.032Z
---

> 注：此规范适用于各个项目仓库本身，故仅适用于具有直接向对应仓库直接进行推送权限的贡献者，对于发起 Pull Request 的形式参与代码贡献的贡献者可忽略此规范。
{.is-info}

> 另注：若您是 deepin 员工且从事 **非**社区版 版本的开发，则请以公司另外提供的分支管理规范文档为准。
{.is-warning}

GitHub 下的 linuxdeepin 组织中包含了 Deepin 社区版所涉及的所有开源项目，也包含了非社区版项目的相应仓库或分支。为方便管理和维护，也方便社区可以更好的理解 Deepin 的代码组织方式和利用项目代码，这些项目遵循一定的分支命名规范以便开发协作和管理。以下文档涵盖社区版相关的分支名称规范，用以给 Deepin 开源社区参考。

# 分支概览

deepin 社区版为滚动发布制，一般没有维护分支，`master` 分支即为研发基线分支。

对于开发者，若需要多个提交才能完成一个特性时，由于研发过程使用 GitHub 的 Fork + Pull Request 模式，故也不需要单独创建研发分支。但特殊情况下，若确需使用研发分支，则可使用 `develop/*` 作为临时的特性研发分支。

当项目发布时，若有维护计划，则使用 `release/${系统版本代号}` 或 `release/${tag}` 作为发布分支。

如上可概括为：

- `master` 研发主干，开发分支
- `develop/*` 仅特殊情况下允许使用的临时研发分支
- `release/*` 版本发布和旧版本维护分支

# 版本号约定

我们会在开发告一段落时，不定期发布软件版本。为了方便管理，我们使用了类似 [semver](https://semver.org/lang/zh-CN/) 的版本号格式约定，格式为：

主版本号.功能版本.修复版本

版本号会体现在社区版发布的 git tag 中，也会体现在非社区版的维护分支中。