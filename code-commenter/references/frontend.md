# 前端注释规范

适用于 JavaScript、TypeScript、JSX/TSX、React、Vue 单文件组件（SFC）、HTML、CSS/SCSS 等。遵循主文件 `SKILL.md` 的简体中文默认规则与只修改注释的边界。

## 目录

1. 语言与语法选择
2. JS / TS 文档注释
3. React 与 JSX/TSX
4. Vue 单文件组件
5. HTML 与 CSS/SCSS
6. 工具指令与禁忌
7. 示例与自检

## 1. 语言与语法选择

| 文件/区域 | 可用注释形式 | 注意事项 |
| --- | --- | --- |
| `.js` / `.ts` | `//`、`/* ... */`、`/** ... */` | 公共 API 优先用 JSDoc/TSDoc 风格 |
| `.jsx` / `.tsx` 的逻辑区 | JavaScript / TypeScript 注释 | `return` 中的 JSX 需要 JSX 语法 |
| JSX 标签树内部 | `{/* 中文注释 */}` | 不可裸写 `//` 作为 JSX 子节点 |
| `.vue` 的 `<script>` | JS/TS 注释 | 尊重 `<script setup>` 上下文 |
| `.vue` 的 `<template>` | `<!-- 中文注释 -->` | 避免破坏指令、插槽和 DOM 结构 |
| `.vue` 的 `<style>` / `.css` / `.scss` | `/* 中文注释 */` | CSS 文件中不使用 `//`；SCSS 支持但不优先 |
| `.html` | `<!-- 中文注释 -->` | 避免敏感信息和不必要的标记噪声 |

在混合文件中按**当前语法区域**选注释形式，而不是只依赖扩展名。

## 2. JavaScript / TypeScript 文档注释

- 暴露给其他模块使用的函数、Hooks、复杂工具函数可使用 `/** ... */` 文档注释。
- 描述输入含义、默认值/空值约束、返回语义、可见副作用和失败边界；不重复 TypeScript 已表达的类型信息。
- TypeScript 适当沿用仓库已有的 TSDoc/JSDoc 标签风格，如 `@param`、`@returns`、`@throws`、`@deprecated`，标签说明使用中文。
- 在 JavaScript 中，只有项目工具链支持且确有价值时才添加 `@typedef`、`@template`、`@type` 等类型描述。
- 不虚构异步函数一定抛出何种异常，也不对未实现的取消能力作承诺。
- 不在注释中粘贴大段类型定义或与代码同步困难的示例数据。

## 3. React 与 JSX/TSX

重点解释：

- 自定义 Hook 的使用前提、返回值含义、共享状态语义和清理要求。
- `useEffect` 的外部同步目的、订阅/解绑理由；不逐一复述依赖数组。
- `useMemo` / `useCallback` 的性能依据（只有可证实时）；竞态消除、旧请求忽略、事件顺序、SSR/水合兼容等特殊处理。
- 复杂表单字段联动、权限展示、空状态和条件渲染的实际业务原因。

避免给每个 `useState`、`onClick`、简单 JSX 分支加注释；不要把 JSX 注释加到字符串内容或属性值中。

## 4. Vue 单文件组件

- `<script setup>` 中使用对应 JS/TS 注释语法；解释关键 `computed`、`watch`、生命周期钩子及请求竞争的原因。
- `<template>` 中使用 HTML 注释语法，仅解释复杂条件展示、插槽约束等非直观逻辑。
- `<style scoped>` 中使用 CSS 注释语法，重点说明穿透选择器、层叠和兼容原因。
- 不因为添加注释而拆改模板标签、指令绑定、响应式引用或 SFC 区块边界。
- 注意某些编译或 DOM 场景会保留/处理 HTML 注释；如可能影响快照、SSR 或渲染，选择写在脚本中或仅报告。

## 5. HTML 与 CSS/SCSS

- HTML 注释应解释不可见但重要的结构约束、兼容性或生成边界；不写“导航栏开始/结束”类无价值标记。
- CSS 注释解释覆盖第三方样式的原因、特殊选择器优先级、浏览器兼容回退及布局约束。
- 不为每条 CSS 声明添加注释；不写“设置颜色/设置宽度”等机械描述。
- CSS 注释使用 `/* ... */`，不要把 SCSS 的 `//` 写进普通 CSS。
- 避免在 HTML 注释中包含 `--` 序列或私密配置，确保注释语法合法。

## 6. 工具指令与禁忌

以下注释可能影响类型检查、lint、构建、覆盖率或格式化；**不要擅自翻译、清理、挪动、合并或删除**：

- `// @ts-ignore`、`// @ts-expect-error`、`// @ts-check`、`// @ts-nocheck`
- `/* eslint-disable */`、`// eslint-disable-next-line`、`/* global ... */`
- `// prettier-ignore`、`/* istanbul ignore next */` 等类似覆盖率指令
- `//# sourceMappingURL=...`、`// @license`、`/*! ... */`
- `/* #__PURE__ */`、代码生成占位符、框架/构建工具专用注释

同样保留 JSX/Vue/HTML 模板中可能被编译、测试快照或 SSR 依赖的特殊注释；不确定时不改动并说明风险。

## 7. 示例与自检

以下例子仅展示注释形式和有证据时的表述方式。

### TypeScript 公共函数

```ts
/**
 * 规范化搜索关键词，用于统一缓存键与请求参数。
 *
 * @param keyword 用户输入的搜索关键词
 * @returns 去除首尾空白并转换为小写后的关键词
 */
export function normalizeKeyword(keyword: string): string {
  return keyword.trim().toLowerCase();
}
```

### React JSX 内的注释

```tsx
return (
  <section>
    {/* 未完成身份验证时不展示敏感操作入口。 */}
    {verified && <SensitiveActions />}
  </section>
);
```

只有在上下文中确认 `verified` 确实代表身份验证时，才应使用上述业务说明。

### React Effect 的实现原因

```tsx
useEffect(() => {
  // 组件卸载或依赖变化后，取消当前订阅，避免旧事件继续更新状态。
  const unsubscribe = subscribeToUpdates(setData);
  return () => unsubscribe();
}, [subscribeToUpdates]);
```

### Vue 单文件组件

```vue
<template>
  <!-- 审核未通过的申请不提供提交入口。 -->
  <button v-if="canSubmit" @click="submit">提交</button>
</template>

<script setup lang="ts">
// 审核状态变化后重新计算可提交权限，避免沿用过期状态。
const canSubmit = computed(() => approvalStatus.value === 'APPROVED')
</script>

<style scoped>
/* 保持弹窗层级高于页面导航，避免被固定定位元素遮挡。 */
.dialog-overlay { z-index: 1000; }
</style>
```

注意：Vue 示例中的业务语义必须由项目代码或规范证实，不能仅依据变量名臆测。

### 前端自检

- 当前注释语法是否与 JS、TS、JSX、Vue template、CSS 区域匹配？
- TS 类型是否已充分自描述，注释是否只是重复类型？
- 是否保护了编译器、lint、格式化器、覆盖率与 source map 指令？
- 是否避免引入影响 SSR、DOM、快照或组件布局的模板注释？
- 是否未改动组件行为、响应式依赖、JSX 结构、CSS 选择器和构建配置？
