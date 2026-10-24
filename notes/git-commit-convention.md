# Git 提交信息规范与约束方式

## 规范

遵循 Conventional Commits：

```
type(scope): subject

body

footer
```

- **type** 必须是：`feat` `fix` `docs` `style` `refactor` `perf` `test` `build` `ci` `chore` `revert`
- **scope** 可选，括号包裹，写模块或目录名
- **subject** 英文祈使句，首字母小写，不加句号，整行 ≤ 72 字符
- **body** 与标题空一行，说明**为什么**而非做了什么，每行 ≤ 72 字符
- **footer** 破坏性变更写 `BREAKING CHANGE:`，关联 issue 写 `Closes #123`

禁止 AI 署名（`Co-Authored-By: Claude`、`🤖 Generated with ...`），禁止中文标题行。

完整规则与示例见全局 agent 指令文件（`~/.claude/CLAUDE.md`）。

## 为什么不用 git hook 强制

试过用 `core.hooksPath` 指向全局 hook 目录，**已回退**。原因是它有一个静默破坏性的副作用。

### 机制

git 的钩子默认从每个仓库自己的 `.git/hooks/` 读取。设置 `core.hooksPath` 后，git **只查新目录，完全忽略 `.git/hooks/`**。

关键点：这对**所有钩子类型**生效，不只是 `commit-msg`。`pre-push`、`post-checkout`、`post-merge` 等一并改道。

### 实际踩到的坑

某个使用 Git LFS 的仓库有 4 个由 LFS 生成的钩子：

```
post-checkout / post-commit / post-merge / pre-push  →  git lfs <event> "$@"
```

这些钩子负责把 LFS 指针文件替换成真实内容。全局 `core.hooksPath` 生效后，git 在新目录找不到同名钩子，就当作没有钩子直接跳过：

- 检出时 LFS 文件不被还原，工作区全是几百字节的指针文本
- 推送时大文件可能没真正上传
- **git 不报任何错误**，因为"找不到钩子"是合法状态

这是它比"配置写错"更危险的地方：失败是静默的。

### 结论

全局 `core.hooksPath` 会绕过所有仓库的 LFS、husky、pre-commit 等既有钩子，不适合作为默认配置。

如果将来确实需要机械强制，可选：

1. 单仓库设置 `core.hooksPath`，确认该仓库无其他钩子
2. 用 `includeIf "gitdir:<path>/"` 把配置限定到特定项目，不影响其他仓库
3. 改用 `pre-commit` 框架，它自己管理钩子链，不与其他钩子冲突

## 采用的方案

只用全局 agent 指令文件（`~/.claude/CLAUDE.md`）的指令层约束。

- 全局生效，所有项目、所有会话自动加载
- 能说明**为什么**并给出示例，比机械拦截更容易被正确应用
- 零风险，不影响 git 本身的任何行为
- 局限：只约束 agent，手动提交不受限制，也可能偶尔遗漏

## 小结

- 提交信息统一用英文标准格式，面向人的文档用中文
- 时间：2026-10-25
