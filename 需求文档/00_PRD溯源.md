# PRD 溯源（Survey）

> 走查按本文锚点表逐项核对；PRD 变更时先更新本表，再动设计稿。

## PRD 来源

- 来源类型：Notion（挂在 Linear 项目 [Survey 1.0](https://linear.app/kira-learning/project/survey-10-bd3fef51c0f7/overview) 的资源栏，2026-09-09 经 Linear MCP 读取）。
- PRD 链接：[Survey Prototype & PRD](https://www.notion.so/kira-learning/PRD-Survey-35770a1b99248014a787c4111ada90bc)。
- 版本 / 最后更新时间：待填（需打开 Notion 页面核对）。

### 配套文档（同一资源栏）

| 文档 | 用途 | 链接 |
| --- | --- | --- |
| Survey Question Types (3) — Content & Answer Contract | 三种题型的内容与答案契约，题型相关设计以此为准 | [Notion](https://app.notion.com/p/kira-learning/Survey-3-3a370a1b992481029859d6b1cee780ec) |
| Survey API Reference | 接口参考，核对字段 / 状态取值时用 | [Notion](https://app.notion.com/p/kira-learning/Survey-API-Reference-39570a1b99248199b245ef187b6c1dc4) |
| Survey 1.0 Test Cases | QA 用例，走查 A 轨可对照 | [Notion](https://app.notion.com/p/kira-learning/Survey-39f70a1b992480069189df479b65f820) |

## 章节锚点表：Survey 1.0 PRD（前缀 `P-`）

> 待填：1.0 已上线，只在新功能 PRD 引用 1.0 章节（如 Overview §7.6、Teacher View §8）时按需建锚点。

| 锚点 | PRD 章节 | 对应设计文档 / 节点 |
| --- | --- | --- |
| P-01 | 待填 | 待填（Figma node_id + 链接） |

---

## 当前迭代：结果导出（前缀 `EXP-`）

### 来源

- Linear 工单：[APAC-5977 · [Export] Results Data Export](https://linear.app/kira-learning/issue/APAC-5977/export-results-data-export)（项目 Survey Feedback & Iteration · 优先级 High · 状态 In Progress · 负责人 Xiaoyue）。
- PRD：[[PRD] Survey Results Data Export](https://app.notion.com/p/kira-learning/PRD-Survey-Results-Data-Export-3d670a1b99248173bfb9d24e957a3b66)（Notion）。
  - 所属：Product Requirement Documents / PRDs / [PRD] Survey Feedback Iteration September（父页面）。
  - 依赖：Survey 1.0 Overview §7.1、§7.6、§7.8、§7.10；Teacher View §8。
  - 读取时间：2026-09-09（Notion MCP，页面最后编辑 2026-09-09 09:03 UTC，状态 unverified）。
- PM 约定（工单评论）：有问题先留 question doc（位置待填）。

### 章节锚点表

> 「设计涉及」= 是：需要出 Figma 稿或在稿中体现；否：文件内容 / 数据规格，工程实现，走查时只核对不画。

| 锚点 | PRD 章节 | 要点 | 设计涉及 | 对应设计文档 / 节点 |
| --- | --- | --- | --- | --- |
| EXP-01 | §1 Problem | 结果目前只能在产品内看；教师无法把数据用于内部报告、认证材料或与成绩册对比 | 背景 | — |
| EXP-02 | §2 Goal | 创建该 assignment 的教师可把该 assignment 的结果下载为文件；文件遵循与 Results 页相同的身份边界 | 背景 | — |
| EXP-03 | §3 Who Can Export | 仅 assignment 创建者可导出；参与者、guest、共享结果查看者**看不到**导出动作，也不能触发 | 是（非创建者视图无入口） | 待填 |
| EXP-04 | §4 Entry Point | `Export` 动作出现在教师端单个 assignment 的 Results 页 **header**；**Decision**：导出只在 assignment 级，Survey Detail 页不放导出动作，多个 assignment 分别导出 | 是（主入口） | 待填 |
| EXP-05 | §5.1 两种模式共有内容 | 问卷标题、assignment 名、响应模式、导出时间；原始 section / 题目顺序、题干、题型（量表含点数与全部标签）；每题结果与 Results 页一致（各选项 / 量表点的计数与百分比、量表均值）；每题应答数；总应答数与基于名册的应答率（guest 计入总数、不计入应答率，Overview §7.6.4） | 否 | — |
| EXP-06 | §5.2 Anonymous | 只含汇总与去标识的开放题；绝不含姓名、邮箱、头像等身份信息，也不含 guest 名（Overview §7.10） | 否（隐私规则） | — |
| EXP-07 | §5.2.1 按题组织 | **Decision**：匿名导出按题组织，每题各自一个响应列表；顺序每题独立随机，跨题、跨次导出都不保持同序 | 否 | — |
| EXP-08 | §5.2.2 开放题原文 | **Decision**：匿名导出包含开放题原文，按题组织并按 §5.2.1 独立随机 | 否 | — |
| EXP-09 | §5.2.3 无最低应答阈值 | **Decision**：不论应答数多少都包含开放题文本，与教师在 Results 已可见范围一致；匿名保护靠按题组织 + 独立乱序 | 否 | — |
| EXP-10 | §5.3 Identified | 同样按题组织；每条答案含受访者姓名、邮箱（有则）、答案（含开放题）、提交时间；不含 guest（实名问卷不允许 guest 提交，Overview §7.10） | 否 | — |
| EXP-11 | §6 XLSX Format | **Decision**：导出一个 XLSX，不提供格式选择器；点 `Export` 直接开始下载；文件可在 Excel 与 Google Sheets 打开 | 是（点击即下载，无弹窗 / 选项） | 待填 |
| EXP-12 | §6.1 Sheet 结构 | Anonymous：`Overview` / `Question Summary` / `Open-ended Responses`；Identified：`Overview` / `Question Summary` / `Responses` | 否 | — |
| EXP-13 | §6.2 `Overview` sheet | 字段：Survey title / Assignment name / Response mode / Collection period / Exported at / Participants / Submitted / Guest responses / Total responses / Response rate；无名册时 Participants、Submitted、Response rate 显示 `N/A`，Guest responses 与 Total responses 照实 | 否 | — |
| EXP-14 | §6.3 `Question Summary` sheet | 列：Section / Question # / Question / Type / Responses / Option-Scale label / Count / Percentage / Mean；一个选项或量表点一行，题目信息重复；Mean 仅量表题有值 | 否 | — |
| EXP-15 | §6.4 `Open-ended Responses`（Anonymous） | 列：Section / Question # / Question / Response；按题分组，无受访者与时间信息；顺序按 §5.2.1 | 否 | — |
| EXP-16 | §6.5 `Responses`（Identified） | 列：Section / Question # / Question / Respondent name / Email / Submitted at / Response；一答一行按题分组；跳题不生成行；未提交者不含 | 否 | — |
| EXP-17 | §6 文件名 | `{Survey title} — {Assignment name} — Results.xlsx`；文件名不支持的字符替换为空格，不改产品内标题 | 否 | — |
| EXP-18 | §7 零应答 | `Export` **禁用**，hover 显示原因 | 是（禁用态 + tooltip） | 待填 |
| EXP-19 | §7 无名册但有应答 | 应答率显示 `N/A`，总应答数照实 | 否（文件内容） | — |
| EXP-20 | §7 导出中 | 进度可见；完成前不能再次触发 | 是（进行中态） | 待填 |
| EXP-21 | §7 失败 | 显示**行内错误**并可重试；教师可继续查看 Results | 是（错误态） | 待填 |
| EXP-22 | §7 大数据量 | 绝不静默截断；无法完成时给出明确错误并允许重试 | 是（复用 EXP-21 错误态） | 待填 |
| EXP-23 | §7 已过期 / 锁定的 assignment | Export 仍可用 | 是（状态覆盖检查：过期 / 锁定态 header 仍有入口） | 待填 |

## 说明

- 锚点编号一经分配不复用；PRD 章节删除时该行标「已废弃」，不删行。前缀：`P-` = Survey 1.0 PRD，`EXP-` = 结果导出 PRD；后续新功能另起前缀。
- PRD 说不清的地方不替 PM 猜，进 `待确认问题清单.md`。
