# CTO 交接说明

本文档用于帮助 CTO 快速理解项目方向、当前产物和建议技术路径。

## 1. 项目本质

这个项目不是做一个普通 AI 应用，也不是做一个通用 Agent 平台。

项目本质是：

> 面向传统行业交付可上岗 AI 数字员工。

第一阶段选财税行业，是因为财税场景流程高频、资料密集、规则明确、人工重复劳动多、ROI 容易计算。

## 2. 第一阶段产品目标

交付一个本地化 AI 员工主机 Demo，能够演示：

```text
本地资料导入
  → AI 识别资料
  → 客户匹配与归档建议
  → 缺失资料判断
  → 生成客户催收话术
  → 人工确认
  → 模拟发送 / 记录状态
  → 老板日报
```

不需要一开始就做完整平台。

## 3. 推荐 MVP 数字员工

优先做 3 个：

1. 资料整理员
   - 处理本地文件
   - 识别资料类型
   - 匹配客户
   - 判断月份
   - 给出归档建议
   - 异常转人工

2. 客户催收员
   - 检查客户缺失资料
   - 生成催收话术
   - 人工确认
   - 模拟发送企微/飞书消息
   - 跟踪回复状态

3. 老板日报员
   - 汇总每日处理结果
   - 汇总缺失资料客户
   - 汇总异常风险
   - 汇总 AI 节省时间
   - 生成日报文本

## 4. 推荐技术架构

建议优先采用本地化桌面应用架构：

```text
Electron
  ├─ React + TypeScript 前端
  ├─ Node / Express 本地服务
  ├─ SQLite / better-sqlite3
  ├─ 本地文件资料库
  ├─ Model Gateway
  ├─ Agent Runtime
  ├─ Builder Engine
  └─ Audit Log
```

如果为了更快演示，也可以先做 Web 版 Mock Demo，再迁移 Electron。

## 5. 前端核心模块

建议从 `GUI高保真原型/index.html` 拆出以下组件：

- AppShell
- SidebarNavigation
- EmployeeHeader
- KPIGrid
- WorkListPanel
- MainWorkPanel
- ActionPanel
- ActivityLog
- DocumentPreview
- MessageEditor
- ReportPreview
- WorkflowBoard
- KnowledgeQA

核心思想：

> 不要为每个数字员工写一套页面，而是用统一组件 + EmployeeViewConfig 渲染。

## 6. 后端核心模块

建议拆成：

- LocalDatabaseService
- FileIngestionService
- DocumentClassifier
- CustomerMatcher
- TaskEngine
- AgentRuntime
- HumanApprovalService
- MessageChannelAdapter
- ReportGenerator
- AuditLogService

第一阶段可以大量使用 mock 和模拟动作，不必一开始接真实企微/飞书。

## 7. 关键数据模型建议

优先设计：

```text
DigitalEmployee
EmployeeViewConfig
EmployeeTask
Customer
CustomerDocument
DocumentFile
HumanApproval
RunLog
MessageDraft
DailyReport
```

## 8. Builder 第一版建议

Builder 第一版只做一个演示场景：

> 从一句话创建“财税客户催收员”。

示例输入：

```text
我想创建一个客户催收员，帮会计检查客户每月缺哪些资料，然后生成企微催收话术，发送前需要我确认。
```

Builder 输出：

- 岗位名称
- 岗位目标
- 输入数据
- 工作流程
- 人工确认节点
- 异常升级规则
- 话术风格
- GUI 模板配置
- 测试任务
- 上线清单

## 9. 近期开发建议

建议按这个顺序推进：

1. 初始化 React / Electron 工程
2. 接入 Tailwind / shadcn/ui
3. 实现统一 AppShell
4. 实现 3 个模板的 React 版
5. 设计 SQLite schema
6. 实现本地文件导入
7. 实现资料整理员 mock runtime
8. 实现客户催收员 mock runtime
9. 实现老板日报员 mock runtime
10. 再做 Builder 对话式创建流程

## 10. 风险提醒

不要一开始做太大：

- 不要先做完整 Agent 平台
- 不要先做自由拖拽低代码系统
- 不要先接很多行业
- 不要先接真实复杂业务系统
- 不要先做完整权限体系

先把财税 MVP 跑通。

## 11. 当前最重要的产品判断

这个项目的成败不在于“能不能创建很多 Agent”。

而在于：

> 能不能把一个传统行业里的真实岗位，交付成客户愿意付费的 AI 数字员工。

所以第一阶段一定要围绕具体岗位、具体流程、具体 ROI 做闭环。
