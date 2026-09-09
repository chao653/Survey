# Survey 项目入口

> 新会话先读本文件，再按任务类型读对应必读文件。历史决策见 `决策日志.md`（先读顶部 5 条）。

## 1. 项目范围

### 产品背景（Survey 1.0，已上线）

- 一句话范围：Survey 是 Kira 的课程问卷功能——教师在课程中快速创建问卷（可从 prompt / starter / 模板 / 空白开始，Kira AI 补问缺失信息并生成可审阅草稿）、指派给班级或个别学生；学生以匿名或实名模式作答（允许跳题提交）；教师在 Results 页用 AI Summary 读整体模式，并以 Instructor Response 回应学生；关键反馈转成非评估数据供 Student Atlas 使用。（来源：Linear 项目描述，2026-09-09 读取）
- Linear 项目：[Survey 1.0](https://linear.app/kira-learning/project/survey-10-bd3fef51c0f7/overview)（initiative Survey · lead Xiaoyue · 设计团队 APAC - Design · 状态 In Progress，起止 2026-06-23 → 2026-09-07；七个里程碑中 Product / Design / Design Review / Implementation / Release 已 100%，Testing 99%、Design QA & Polish 98%）。
- 1.0 PRD：[Survey Prototype & PRD](https://www.notion.so/kira-learning/PRD-Survey-35770a1b99248014a787c4111ada90bc)（Notion，来自 Linear 项目资源）。新功能的 PRD 引用 1.0 PRD 章节（如 Overview §7.6）时，到这里查。

### 当前迭代：结果导出（Results Data Export）

- Linear 工单：[APAC-5977 · [Export] Results Data Export](https://linear.app/kira-learning/issue/APAC-5977/export-results-data-export)（项目 Survey Feedback & Iteration · 里程碑 Product Roadmap · 优先级 High · 状态 In Progress · 负责人 Xiaoyue）。
- PRD：[[PRD] Survey Results Data Export](https://app.notion.com/p/kira-learning/PRD-Survey-Results-Data-Export-3d670a1b99248173bfb9d24e957a3b66)（Notion，隶属「[PRD] Survey Feedback Iteration September」；2026-09-09 经 Notion MCP 读取，锚点 EXP-01～EXP-23 见 `需求文档/00_PRD溯源.md`，已确认规则见 `需求文档/01_产品规则.md`）。
- 一句话需求：教师（仅 assignment 创建者）在单个 assignment 的 Results 页 header 点 `Export`，直接下载一个 XLSX；Anonymous / Identified 两种模式导出内容不同，匿名模式绝不泄露身份。
- 设计涉及面：Results 页 header 的 `Export` 入口，以及它的 默认 / 禁用（零应答，hover 提示）/ 导出中 / 失败（行内错误 + 重试）四个状态；非创建者视图不显示该入口。文件内部结构（sheet / 列）是工程规格，不出 Figma 稿。
- PM 约定（工单评论，Xiaoyue）：有问题先留 question doc。本地先记 `需求文档/待确认问题清单.md`，question doc 位置待填。

## 2. 任务路由表

| 任务类型 | 必读文件 |
| --- | --- |
| 设计系统 / token / 基础组件 | `设计执行/规范/design.md` + `设计执行/规范/components.md` + `设计执行/规范/icons.md` |
| Figma 读写 / 绘制 | `设计执行/规范/figma-preferences.md`（必读，固化 token / 组件来源）+ `设计执行/规范/figma-layer-naming.md` + `需求文档/01_产品规则.md` |
| 卡片类产出（需求说明卡、节点标题卡） | `设计执行/规范/需求说明与节点卡片规范.md` |
| 英文 UI 文案撰写 / 大小写走查 | `设计执行/规范/写作规范.md` |
| 页面编排与交付检查 | `设计执行/规范/命名规范.md` |
| Figma 操作记录落盘 | `设计执行/日志/`（格式见其 `README.md`） |
| 历史决策与口径追溯 | `决策日志.md`（新会话先读顶部 5 条） |
| 多方案探索（HTML demo） | `设计方案/README.md` |
| 设计走查 | `走查/00_走查清单框架.md` |
| 验收报告 | `设计执行/验收/验收报告模板.md` |
| 产品网站取数 / 截图 / 行为验证 | `需求调研/登录说明.md`（本地文件，已 gitignore；首次从 `需求调研/登录说明.template.md` 复制生成）。用 Playwright MCP；原始产物按抓取需求分类存 `需求调研/抓取结果/<抓取需求>/`，一个需求一个文件夹；基于抓取产出的调研文档归 `需求调研/调研文档/` |
| Linear 工单 | `Linear/AGENTS.md` |
| PRD 溯源 / 待确认问题 | `需求文档/00_PRD溯源.md` + `需求文档/待确认问题清单.md` |

## 3. 决策顺序

用户当前指令 > 用户指定的节点 / PRD 范围 > `需求文档/01_产品规则.md` 已确认规则 > 本地执行文档与走查结论 > 通用判断。

冲突影响业务规则或交付结论时，先请用户确认，不自行拍板。

## 4. Figma 工具铁律

- 一律用 Figma MCP 读写 Figma；不可用时说明原因，经用户确认后才可换途径。
- 在 Figma 完成操作后，把记录写入 `设计执行/日志/`（按类型组文件，格式见其 `README.md`）。
- 走查轮次产物（报告、修改清单、截图）归 `走查/`，不放进 `设计执行/日志/`，两边不混。

## 5. 输出要求

- 简体中文、大白话。
- 结论区分三类：「已确认」/「设计判断」/「需用户确认」。
