# systematic-debugging

[English](./README.md)

面向 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 的结构化 **五阶段排错** 方法：**先根因，后改代码**。

## 为什么需要

Claude Code 写代码很强，但遇到 bug 时默认往往是「随机改到好为止」。本 Skill 强制流程：

1. **Phase 0：上下文回忆** — 以前见过类似问题吗  
2. **Phase 1：根因调查** — 读报错、复现、跟数据流  
3. **Phase 2：模式对比** — 找正常样本，对比差异  
4. **Phase 3：假设验证** — 一次只动一个变量  
5. **Phase 4：实现修复** — 先写失败用例，再单一补丁  

铁律：**未完成根因调查不得进入「试修复」**。

## 安装

```bash
git clone https://github.com/runesleo/systematic-debugging-skill ~/.claude/skills/systematic-debugging
```

或将 `SKILL.md` 复制到 `~/.claude/skills/systematic-debugging/SKILL.md`。

## 使用

出错时可自动触发；也可手动 `/debug`，或在 `CLAUDE.md` 中写明遇 bug 先走本 Skill。

## 核心思想

| | 系统化 | 乱试补丁 |
|--|--------|----------|
| 修复耗时 | 约 15–30 分钟 | 常达数小时 |
| 一次修对率 | ~95% | ~40% |
| 引入新 bug | 极少 | 常见 |

## 红旗话术

若模型说「先 quick fix 以后再查」「改 X 试试看」「不太懂但可能有效」——Skill 会把流程拉回 Phase 1。

## 定制

Skill 即单文件 Markdown，可按项目扩展模式、Phase 0 知识库集成、领域红旗等。

## 许可 / 作者

MIT。作者信息见英文 [README](./README.md)。
