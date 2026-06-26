# 贡献指南

这份指南说明如何参与本项目共建。项目采用 **Fork + Pull Request** 模式：贡献者在自己的 Fork 仓库中修改内容，再通过 Pull Request 请求合并到主仓库。

这种方式适合多人协作。主仓库像“正式出版区”，个人 Fork 像“个人工作区”。个人工作区允许试错，正式出版区只接收经过评审的内容。

## 一、协作模型

### 核心分支

主仓库长期保留两个公共分支：

- `main`：稳定分支，代表阶段性可交付成果。
- `dev`：日常集成分支，贡献者的 Pull Request 默认提交到这里。

普通成员不要直接向主仓库推送代码，也不要在主仓库创建个人长期分支。所有个人开发分支都放在自己的 Fork 仓库中。

### 角色分工

| 角色 | 建议权限 | 主要职责 |
| --- | --- | --- |
| 总管理员 | Admin | 仓库配置、主分支保护、最终合并、争议裁定 |
| 模块负责人 | Write | 模块 PR 初审、冲突协助、任务拆分、日常答疑 |
| 普通成员 | Read | Fork 后贡献内容、提交 PR、同步主仓更新 |

这里的权限遵循最小权限原则。最小权限原则的意思是：一个人只拿完成当前职责所必需的权限。它的反面是“全员高权限”，短期看方便，长期会带来误删分支、强推覆盖、主仓混乱等风险。

## 二、适合贡献什么

欢迎贡献：

- AI 前沿行业项目案例、项目说明、复盘材料。
- 具体项目的安装部署、环境配置、接口文档、使用教程。
- 数据清洗、评测、RAG、Agent、ASR、知识库等实践资料。
- 文档修正，例如错别字、失效链接、表述不清、目录混乱。
- Issues 中的问题反馈、资料线索、任务建议。

不建议一次 PR 混入多个无关主题。例如，一个 PR 同时改登录接口、补行业报告、重排目录，会让评审困难。更好的做法是拆成多个小 PR。

## 三、第一次参与：环境准备

### 1. Fork 主仓库

进入主仓库页面，点击右上角 **Fork**，把主仓库复制到自己的 GitHub 账号下。

如果不熟悉 Fork，可以参考 GitHub 官方文档：[Fork a repo](https://docs.github.com/en/get-started/quickstart/fork-a-repo)。

### 2. 克隆自己的 Fork 仓库

把下面命令中的 `你的用户名` 和 `仓库名` 换成自己的实际信息：

```bash
git clone https://github.com/你的用户名/仓库名.git
cd 仓库名
```

### 3. 添加主仓库为 upstream

`origin` 通常指向自己的 Fork 仓库，`upstream` 指向社区主仓库。后续同步最新内容时，需要从 `upstream` 拉取。

```bash
git remote add upstream https://github.com/主仓库所有者/仓库名.git
git remote -v
```

如果能看到 `origin` 和 `upstream` 两组地址，说明远程仓库配置完成。

## 四、每次贡献：标准流程

### 1. 同步主仓库最新内容

每次开始新任务前，先让本地 `dev` 分支追上主仓库：

```bash
git checkout dev
git pull upstream dev
```

如果本地还没有 `dev` 分支，可以先执行：

```bash
git fetch upstream
git checkout -b dev upstream/dev
```

### 2. 创建个人任务分支

基于最新 `dev` 创建一个新分支：

```bash
git checkout -b docs/你的名字-贡献说明
```

分支命名建议：

| 类型 | 用途 | 示例 |
| --- | --- | --- |
| `docs/` | 文档更新 | `docs/zhangsan-update-readme` |
| `feature/` | 新功能或新项目 | `feature/lisi-rag-demo` |
| `fix/` | Bug 修复 | `fix/wangwu-login-error` |
| `data/` | 数据或资料整理 | `data/zhaoliu-clean-report` |

一个分支只做一件事。分支存活时间建议控制在 7 天内，避免长期不同步导致大量冲突。

### 3. 修改内容并本地检查

根据任务修改文档、代码或资料。提交前至少检查：

- Markdown 标题层级是否清晰。
- 链接是否能打开。
- 命令、路径、文件名是否准确。
- 如果改了代码，是否已经运行相关测试或启动验证。
- 中文文档统一使用 UTF-8 编码。

### 4. 提交改动

```bash
git status
git add .
git commit -m "docs: 补充社区共建说明"
```

提交信息建议使用简洁前缀：

- `docs:` 文档更新
- `feat:` 新功能或新项目
- `fix:` 问题修复
- `refactor:` 重构
- `test:` 测试相关
- `chore:` 构建、配置、维护类改动

### 5. 推送到自己的 Fork 仓库

```bash
git push origin docs/你的名字-贡献说明
```

### 6. 发起 Pull Request

在 GitHub 页面点击 **Compare & pull request**。

注意目标分支：

- base repository：社区主仓库
- base branch：`dev`
- compare branch：你 Fork 仓库里的个人任务分支

填写 PR 时，请说明：

- 这次改了什么。
- 为什么要改。
- 是否关联某个 Issue。
- 做过哪些自测或检查。
- 是否有需要评审者重点看的地方。

GitHub 官方 Pull Request 说明见：[About pull requests](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)。

## 五、评审与合并

PR 提交后，会由模块负责人或管理员评审。

评审可能出现三种结果：

- 直接通过并合并。
- 要求修改后再合并。
- 暂不合并，并说明原因。

如果评审者提出修改意见，在自己的任务分支继续修改并提交即可，同一个 PR 会自动更新：

```bash
git add .
git commit -m "docs: 根据评审意见调整贡献流程"
git push origin docs/你的名字-贡献说明
```

PR 合并后，可以删除个人 Fork 仓库里的任务分支。下次贡献时重新从最新 `dev` 创建新分支。

## 六、常见问题

### Fork、Branch、Pull Request 分别是什么

- Fork：把主仓库复制一份到自己的账号下。它是你的独立工作区。
- Branch：同一个仓库里的并行工作线。一个任务建议对应一个分支。
- Pull Request：请求主仓库把你的改动拉进去。它既是合并请求，也是讨论和评审记录。

可以用写作类比理解：Fork 是复印一本书到自己的书桌上，Branch 是开一个专题草稿，Pull Request 是把整理好的章节提交给编辑审核。

### 为什么不让所有人直接推送到主仓库

多人直接推送看似省事，但会带来三个问题：

- 难追溯：不知道某个改动为什么进入主仓。
- 难回滚：错误提交和正确提交混在一起。
- 难协作：分支越来越多，冲突越来越频繁。

Fork + PR 的价值在于隔离风险。用数学方式看，可以把主仓库状态记为 \(S\)，每个人的改动记为 \(\Delta_i\)。直接推送相当于把所有 \(\Delta_i\) 立即叠加到 \(S\) 上；PR 模式则是在合并前先检查每个 \(\Delta_i\)，只把通过评审的改动合入 \(S\)。

### 发生冲突怎么办

先同步主仓库最新 `dev`：

```bash
git fetch upstream
git checkout dev
git pull upstream dev
git checkout 你的任务分支
git merge dev
```

然后按 Git 提示解决冲突，重新提交并推送。如果冲突较大，可以在群里找模块负责人协助。

### 不会写代码也能贡献吗

可以。社区共建不只包括代码，也包括文档、资料整理、案例复盘、错误修正、Issue 反馈和使用经验。很多高价值贡献都来自把复杂经验讲清楚。

### 一个 PR 应该多大

越小越好，但要保持完整。一个理想 PR 应该能用一句话说清楚目的，例如：

- “补充 canbe_asr 项目的部署说明”
- “修复登录接口文档中的参数名错误”
- “新增一个 RAG 评测数据集说明”

如果一句话说不清，通常应该拆分。

## 七、管理员建议配置

为了让协作流程长期稳定，建议仓库管理员配置：

- 为 `main` 和 `dev` 开启分支保护。
- 要求 PR 后才能合并。
- 要求至少 1 名评审者通过。
- 开启新提交后旧审批失效。
- 禁止 force push。
- 禁止删除受保护分支。
- 开启合并后自动删除 head branch。
- 使用 Issues 记录任务，避免只在群聊中口头分配。

这些配置不影响普通成员贡献，但能显著降低主仓库被误操作的风险。
