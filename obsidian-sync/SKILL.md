---
name: obsidian-sync
description: >-
  将 Markdown 笔记、指南、总结或对话产出同步保存到用户的 Obsidian 笔记库，
  并自动匹配其 PARA 目录结构与 Frontmatter 模板。当用户要求保存、导出或同步内容到
  Obsidian 时使用。
---

# Obsidian Sync（同步笔记到 Obsidian）

将 Markdown 内容直接写入用户本地的 Obsidian Vault。

## 笔记库路径

- **Vault 根目录**：`/Users/richard/Library/Mobile Documents/iCloud~md~obsidian/Documents/Notes`

## 目录结构（PARA 体系）

- `00_Daily/<YYYY>/` — 每日日记（`YYYY-MM-DD.md`）
- `10_Personal/`（个人知识库）
  - `01_Inbox/` — 待整理的外部文章、速记与灵感碎片
  - `02_Projects/` — 个人短期项目
  - `03_Areas/` — 个人长期领域（如 `Software/`、`身份证明/`）
  - `04_Resources/` — 整理成型的个人参考资料、指南与模板（如 `AI/`、`Templates/新资料模板.md`）
  - `05_Archives/` — 个人归档
- `20_Work/`（工作知识库）
  - `01_Projects/` — 工作项目
  - `02_Areas/` — 工作长期领域
  - `03_Resources/` — 工作参考资料
  - `04_Archives/` — 工作归档

## Frontmatter 规范

统一在文档顶部按 `10_Personal/04_Resources/Templates/新资料模板.md` 的格式添加 YAML Frontmatter：

```yaml
---
type: <guide | note | reference | summary>
category: <分类名称，例如 AI编程>
tag:
  - <标签1>
  - <标签2>
created: <YYYY-MM-DD>
---
```

## 执行步骤

1. **确定目标目录**：
   - 结构化的指南、教程或通用技术资料默认放入 `10_Personal/04_Resources/<主题>/`（若明显属于特定工作内容则放入 `20_Work/03_Resources/<主题>/`；不确定时先询问用户）。
   - 未经整理的外部摘录或临时想法放入 `10_Personal/01_Inbox/`。
   - 若目标子目录下可能已有同类笔记，先查看目录内容以保持命名风格一致并避免重复。
2. **格式化内容**：
   - 补全顶部 YAML Frontmatter（`type`、`category`、`tag` 列表以及当天的 `created` 日期 `YYYY-MM-DD`）。
   - 保持标准 GitHub Flavored Markdown 格式。
3. **写入并反馈**：
   - 直接将 `.md` 文件写入 Obsidian 目标路径。
   - 回复时附上可点击的 `file://` 链接，并说明选择的目录和标签。
