# code-commenter（Java + 前端中文代码注释 Skill）

这是一个可在支持 Agent Skills 的 Codex / ChatGPT 环境使用的指令型 Skill。

## 文件结构

```text
code-commenter/
├── SKILL.md                 # 通用目标、中文规则、路由、流程、验收
└── references/
    ├── java.md              # Java / Javadoc / Spring 注释规范
    └── frontend.md          # JS / TS / React / Vue / HTML / CSS 注释规范
```

## 在 Codex 中安装

个人级：将整个 `code-commenter` 目录放到 `$HOME/.agents/skills/code-commenter/`。

项目级：将整个 `code-commenter` 目录放到 `<仓库根目录>/.agents/skills/code-commenter/`。

Codex 可通过 `$code-commenter` 显式调用；如未识别到新增 Skill，重新启动 Codex。

## 在 ChatGPT 中使用

具备 Skills 功能的 ChatGPT 环境可通过技能创建/导入功能添加该 Skill；能否直接导入目录或压缩包，取决于具体产品及工作区支持。按照 UI 提示选择或导入整个 Skill 包（不要只复制 `SKILL.md`，否则会丢失引用文件）。可在支持的界面中使用 `@code-commenter` 显式调用。

## 调用示例

- `$code-commenter 使用 smart 模式，为这个 Java Service 添加必要的中文注释；仅修改注释。`
- `$code-commenter 使用 full 模式，完善这个 TypeScript 模块的公共 API 注释。`
- `$code-commenter 使用 business 模式，解释 React 组件中的权限判断与状态流转。`
- `$code-commenter 使用 review 模式，检查 Vue 组件注释是否准确，不要修改文件。`

在 ChatGPT 中将 `$code-commenter` 替换为界面支持的 `@code-commenter` 或通过技能选择器调用。

## 使用建议

1. 首次应用时选择一两个 Java、TS/TSX 或 Vue 文件验证效果。
2. 检查 Diff，确保没有 Java/JS/TS/HTML/CSS 的非注释内容被改动。
3. 业务原因没有足够上下文时，宁可报告待确认项，也不要编造。
4. 后续可独立拆分 `references/frontend.md`，细化 React 与 Vue 规范。
