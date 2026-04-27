# systematic-debugging-skill

**English:** [README.en.md](./README.en.md)

---

面向 Claude Code 的**单文件 Skill**：用 **Phase 0 上下文回忆 → Phase 1 根因调查 → Phase 2 模式对比 → Phase 3 假设验证 → Phase 4 实现** 的强制顺序，约束「先找根因再改代码」；`SKILL.md` 写明未完成前一阶段不得进入下一阶段。

## When to use

- 出现 **Bug、测试失败、意外行为、性能问题、构建失败、集成故障** 等需要归因的技术问题，且在给出修复方案**之前**（与 `SKILL.md` frontmatter `when_to_use` 及正文「Use for ANY technical issue」列表一致）。
- 时间紧、想「先改一行试试」或已试过多次补丁仍失败——`SKILL.md` 明确把这些列为**更应**走流程的情形。
- 多组件链路上需要在边界加日志取证后再判断故障点（见 `SKILL.md` Phase 1「Gather Evidence in Multi-Component Systems」）。

## When NOT to use

- **没有**可调查的缺陷或失败现象、也不存在「意外行为 / 性能 / 构建 / 集成」类待诊断问题时——Iron Law 与 Phase 4 的「Create Failing Test Case」均以**存在待修复问题**为前提（见 `SKILL.md` Overview / Phase 4）。
- 纯概念问答、与当前代码失败无关的泛读，而不进入任何修复闭环时，本 Skill 的阶段闸门与「NO FIXES WITHOUT ROOT CAUSE」约束不对齐。
- 无法遵守「Phase 0 输出未完成不得进入 Phase 1」等硬门槛的执行环境，应先调整流程而非跳过 `SKILL.md` 中的违规定义。

## Quick Start

```bash
git clone https://github.com/runesleo/systematic-debugging-skill ~/.claude/skills/systematic-debugging
```

或手动将 `SKILL.md` 复制到 `~/.claude/skills/systematic-debugging/SKILL.md`。

在对话中可手动引用本技能；或在 `CLAUDE.md` 中写明遇到错误时先按 `SKILL.md` 执行（与仓库内英文说明一致）。

## 典型场景

- CI 红：先对照 Phase 0/1 拉齐日志与最近变更，再动代码。
- 线上偶发：先稳定复现与数据流追踪，再提交单点修复。
- 已两次以上补丁仍失败：按 `SKILL.md` Phase 4 中「3+ fixes failed」与 Red Flags，应暂停堆修复、上升为架构与根因讨论，而非继续猜补丁。

## 仓库结构（贡献者）

| 路径 | 说明 |
|------|------|
| `SKILL.md` | 技能全文：五阶段、红线表、Quick Reference；行为变更只改此文件。 |
| `LICENSE` | 许可证。 |
| `SECURITY.md` | 安全披露与联系方式。 |
| `CODE_OF_CONDUCT.md` | 社区行为准则。 |
