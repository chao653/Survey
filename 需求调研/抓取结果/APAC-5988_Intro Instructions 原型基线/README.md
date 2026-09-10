# APAC-5988 · Intro Instructions 原型基线截图

> 抓取需求：为设计任务 [APAC-5988 · [Design] Add Intro Instructions](https://linear.app/kira-learning/issue/APAC-5988/design-add-intro-instructions) 记录原型现状，作为出稿与走查的对照基线。
> 抓取日期：2026-09-10。来源：原型 `https://survey007.vercel.app/`（有密码门，密码只记在本地 `需求调研/登录说明.md`，不进 git）。
> 抓取方式：Playwright + 无头 Chrome，视口 1440x900；内容通过原型自身的编辑器输入（示例文字与占位图均为抓取时临时生成，非真实数据）。
> 原型是内联 React 单文件，行为结论以其源码为准，截图为佐证。

## 文件索引

| 文件 | 内容 | 看点 |
| --- | --- | --- |
| `00-linear-附图1-*.png` / `00-linear-附图2-*.png` | Linear 工单原附图 | 附图黄框圈的是 **section 级** Instructions（「Describe what this section covers.」），不是本工单的 survey 级 |
| `10-editor-instructions-empty-collapsed.png` | 编辑器 · Instructions 卡 · 空 · 收起 | 画布顶部第一张卡；药丸 `Optional`；副标题「Add context or guidance for participants before they start.」 |
| `11-editor-instructions-empty-expanded.png` | 编辑器 · 空 · 展开 | 工具栏 B / I / U / 无序 / 有序 / 链接 / 图片；placeholder「Add context, expectations, or anything participants should know before they begin.」；底部「Appears on the survey intro page」；**无字数计数器** |
| `12-editor-instructions-filled-expanded.png` | 编辑器 · 已填 · 展开 | 药丸变 `Added`，副标题变「Shown to participants before they start.」；右下出现 `Clear instructions` |
| `13-editor-instructions-filled-collapsed.png` | 编辑器 · 已填 · 收起 | 收起后只靠药丸 `Added` + 副标题提示有内容 |
| `14-editor-section-instructions-expanded.png` | 编辑器 · section 级 Instructions · 展开 | 与 survey 级同一组件；placeholder「Add a short note for this section.」；兄弟需求，设计应共用组件 |
| `15-editor-instructions-2000chars-3images.png` | 编辑器 · 2,000 字符 + 3 图 | 编辑区固定最大高度内滚动；**没有计数器、没有上限、没有超限态、没有图片数量 / 大小校验** |
| `20-student-intro-baseline.png` | 学生 Intro · 无说明（现状基线） | 现有默认内容顺序：课程标签 → 标题 → 引导语 → 题数 / 开放时间卡 → 隐私横幅 → 可跳题提示 → Start Survey |
| `21-student-intro-with-instructions.png` | 学生 Intro · 有说明 | Instructions 卡插在引导语之后、信息卡之前 |
| `22-student-intro-long-content.png` | 学生 Intro · 2,000 字符 + 3 图（整页） | 信息卡、隐私横幅、Start Survey 全被推到首屏之下；原型无折叠 / Read more |
| `30-states.png` | 原型 Boundary States 目录 | 覆盖 Results / AI Insights / Assignment / Multiple choice / Section flow，**没有任何 Instructions 相关状态** |
| `40-teacher-results-list.png` | 教师 Results 页 | 两处旁证：① header 右上已有 `Export` 外框按钮（与 APAC-5977 相关）；② 「Respond to Participants」富文本计数器为 `0/600 Words`——现有先例按**词**计数、灰色不变红 |
| `45-survey-detail-actions.png` | Survey 详情 · Edit survey 锁定 | 原型的锁是 **survey 级**：任一 assignment 为 active / expired / 有回复即锁，整个编辑器进不去；同一 survey 下 Active + Upcoming + Expired 并存 |
| `46-survey-locked-dialog.png` | 锁定对话框 | 「This survey is locked」+ `Make a copy`；原型没有「进编辑器但只读」的形态 |

## 原型与工单的差异（抓取时确认的事实，分析见会话 / 待确认问题清单）

1. 上限：工单 2,000 **字符** + 超限态；原型编辑器按**词**计数、到上限硬截断、注释明写「没有超限态」，且 Intro 这处根本没传上限。
2. 图片：工单最多 3 张、JPG / PNG / WebP、单张 5MB；原型无数量与大小校验，文件选择器还接受 GIF。
3. 锁定：工单要求 Instructions 卡有只读态；原型只有 survey 级整体锁 + 对话框。
4. 链接：原型工具栏有链接按钮但用 `window.prompt`；工单未提链接。
5. `Clear instructions`：原型有，工单未提。
6. 学生端长内容：原型无折叠；工单未提学生端状态。
