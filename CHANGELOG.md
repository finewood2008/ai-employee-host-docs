# 变更记录

## 2026-04-27

### 新增

- 初始化 AI 数字员工主机产品文档仓库。
- 新增完整商业计划书：`01-商业计划书.md`。
- 新增 Agent Builder 产品设计：`02-Agent-Builder产品设计.md`。
- 新增数字员工 GUI 模板库：`04-数字员工GUI模板库.md`。
- 新增 7 类 GUI 高保真 HTML 原型：`GUI高保真原型/index.html`。
- 新增面向 CTO 协同开发的 README。

### 当前重点

第一阶段建议聚焦财税行业 MVP：

- 资料整理员
- 客户催收员
- 老板日报员

形成闭环：

```text
资料整理 → 缺失判断 → 客户催收 → 人工确认 → 任务归档 → 老板日报
```

### 后续建议

- CTO 确认 Electron / React / SQLite 技术架构。
- 将 HTML 高保真原型拆为 React 组件。
- 设计 EmployeeViewConfig 配置模型。
- 开始实现本地文件导入和资料整理员 MVP。
