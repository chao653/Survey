# Rating Grid 结果页（结果卡片 + View Details）

> Figma 文件：[Survey 1.0 - Design Draft](https://www.figma.com/design/jEvNyDqXbaksOd6u07p7SX/Survey-1.0---Design-Draft?node-id=13460-17257) · 页面 `Rating Grid`
> 规则依据：PRD [[PRD] Survey Rating Grid Question Type](https://app.notion.com/p/3da70a1b992481afb110e774a52137d2) §6 Results

## 2026-10-16 · PM Design Review 2 / 3：结果卡片、View Details、Section tab 改到位

- 任务来源：Linear [APAC-6309](https://linear.app/kira-learning/issue/APAC-6309/pm-design-review-2-rating-grid-and-rating-scale-ui-iteration-2)；PM 复查后开的 Review 3 [APAC-6383](https://linear.app/kira-learning/issue/APAC-6383)（子票 APAC-6384 结果卡片、APAC-6385 Highest/Lowest mean、APAC-6386 View Details、APAC-6387 Section tab）。
- 结果状态：已完成（待 PM 复查）。

### 为什么新建组件

旧稿的结果卡片是 `Kira Custom Components (TO BE ARCHIVED)` 库里的 `Survey Card / Rating Grid / Teacher / Result`，母版不在本文件，改了也要发布库才会同步；按 `figma-preferences.md`，旧库不再用于新稿。所以在本文件新建本地组件，原有帧里的实例全部换成新组件。旧库组件本身没有动。

### 涉及节点

| 模块 | node_id | 链接 |
| --- | --- | --- |
| 新组件区 `Components · Rating Grid Result (Design Review 2)` | `16074:18647` | [打开](https://www.figma.com/design/jEvNyDqXbaksOd6u07p7SX/Survey-1.0---Design-Draft?node-id=16074-18647) |
| 组件集 `Survey Card / Rating Grid / Result` | `16083:18724` | [打开](https://www.figma.com/design/jEvNyDqXbaksOd6u07p7SX/Survey-1.0---Design-Draft?node-id=16083-18724) |
| 教师端 Identified · 默认 | `13539:50870` | [打开](https://www.figma.com/design/jEvNyDqXbaksOd6u07p7SX/Survey-1.0---Design-Draft?node-id=13539-50870) |
| 教师端 · Similar means / Row with no responses / No responses yet / 8 statements / 2-point / 7-point | `13542:38` / `13542:768` / `13542:1190` / `13542:1505` / `13542:1979` / `13542:2381` | 同 section |
| 教师端 · View Details 抽屉 | `13913:20313` | [打开](https://www.figma.com/design/jEvNyDqXbaksOd6u07p7SX/Survey-1.0---Design-Draft?node-id=13913-20313) |
| 教师端 · Anonymous | `14050:20959` | [打开](https://www.figma.com/design/jEvNyDqXbaksOd6u07p7SX/Survey-1.0---Design-Draft?node-id=14050-20959) |
| 学生端 Shared Results · Results shared / Shared, no reply / Skipped a question | `13617:38` / `13617:285` / `13617:854` | [打开](https://www.figma.com/design/jEvNyDqXbaksOd6u07p7SX/Survey-1.0---Design-Draft?node-id=13617-38) |
| 新列标题 `Rating Grid / Teacher / Result · New states` | `16087:18729` | 同 section |
| 新帧 · Hover on a narrow segment | `16087:18743` | [打开](https://www.figma.com/design/jEvNyDqXbaksOd6u07p7SX/Survey-1.0---Design-Draft?node-id=16087-18743) |
| 新帧 · Tie for highest | `16087:19048` | [打开](https://www.figma.com/design/jEvNyDqXbaksOd6u07p7SX/Survey-1.0---Design-Draft?node-id=16087-19048) |
| 新帧 · Tie for lowest | `16087:19496` | [打开](https://www.figma.com/design/jEvNyDqXbaksOd6u07p7SX/Survey-1.0---Design-Draft?node-id=16087-19496) |
| 新帧 · One response | `16087:19939` | [打开](https://www.figma.com/design/jEvNyDqXbaksOd6u07p7SX/Survey-1.0---Design-Draft?node-id=16087-19939) |
| 新帧 · View Details - Hover column header | `16089:19849` | [打开](https://www.figma.com/design/jEvNyDqXbaksOd6u07p7SX/Survey-1.0---Design-Draft?node-id=16089-19849) |
| 新帧 · View Details - Full screen | `16089:20134` | [打开](https://www.figma.com/design/jEvNyDqXbaksOd6u07p7SX/Survey-1.0---Design-Draft?node-id=16089-20134) |

组件集变体（`State`）：Default `16074:18648` · Similar means `16074:18788` · Tie for highest `16074:18918` · Tie for lowest `16074:19053` · One response `16074:19190` · Row with no responses `16077:18667` · No responses yet `16077:18794` · 8 statements `16077:18807` · 2-point scale `16078:18698` · 7-point scale `16078:18804`。布尔属性 `Individual responses`（默认开，Anonymous 和学生端关）。

### 操作摘要

结果卡片（对应 APAC-6384 / 6385，教师 Identified、Anonymous、学生 Shared Results 共用一个组件）：

- 题干下一行 `Based on N responses`；去掉每行的 `Based on N responses` 和底部 `40–42 responses per statement`。
- 某行作答人数少于 N 时写 `35 of 38 answered this statement`，等于 N 不写。
- 全员跳过的行只写 `No responses for this statement`（虚线占位），不显示均值，也不再写 `Based on 0 responses`。
- 图例移到第一条陈述上方，浅灰底，标签多时换行。
- 彩条上写百分比（按该行作答人数算）：≥30% 写「档位名 + 百分比」，8%–30% 只写百分比，<8% 不写字；悬停显示「档位名 · 百分比」（见 Hover 帧）。彩条高 16→24px 以放下文字。
- `Highest` / `Lowest` 改为 `Highest mean` / `Lowest mean`，按显示的一位小数比较；并列最高只藏 Highest、并列最低只藏 Lowest；全部相同或只有 1 份回答都不标；全员跳过的行不参与比较。补了 Tie for highest / Tie for lowest / One response 三个状态。
- 彩条色段用 Scale 约束，实例拉宽缩窄时按比例缩放（学生端面板 1036 宽已验证）。

View Details（对应 APAC-6386）：

- 去掉上方 `Statements` 列表；列头直接写「序号 + 陈述原文」，最多 3 行，超出省略，悬停 Tooltip 看全文（见 Hover column header 帧）。
- 格子写「分值 + 档位名」（如 `4 Agree`），底色用该档彩条颜色 20% 透明度；去掉 `Strongly Disagree → Strongly Agree` 刻度图例，表下只留 `-- Skipped, not counted in that statement's mean`。
- 列宽固定 184px 不挤压；放不下时横向滚动：参与者列固定（右侧分隔线），右边缘渐隐 + 底部滚动条提示还有更多列。
- 补全屏帧：面板铺满 1440，5 列平分，列头全文不截断；右上角图标换成退出全屏 `CornersIn`。

Section tab（对应 APAC-6387，教师端 9 帧 + 学生端 3 帧）：

- tab 只写节名（`Course Satisfaction`），去掉含义不明的数字。
- 去掉 tab 下方重复的节名标题，只留一行 `4 questions in this section`；学生端 Shared Results 在 tab 下补同一行。

用到的组件和 token：

- 组件：Badge Outline（`ShadCN-Default`）、Tooltip（`ShadCN-Default`）、`User` / `CaretRight` / `CornersIn`（`Design System 2.0 Icons`）、题号条 `Preview mode - Question number + Points`、Avatar。
- 颜色 token（`Design System 2.0 Foundations`）：`text/primary`、`text/secondary`、`text/tertiary`、`text/invert`、`text/brand/default`、`text/positive`、`text/warning`、`border/primary`、`border/secondary`、`border/positive`、`border/warning`、`separator/primary`、`surface/layer/primary`、`surface/layer/secondary`、`fill/neutral/surface`。
- 文字样式：沿用原卡片的 `text/base/medium`、`text/sm/*`、`text/xs/regular`；彩条文字用 `text/xxs/semibold`。
- 彩条配色（`#e5484d` → `#1dad5b`）沿用旧稿，库里没有对应 token，保持写死。

### 结论分类

已确认（工单 + PRD §6 原文）：

- 上面「结果卡片」「View Details」两部分的全部规则。

设计判断：

1. 结果卡片在本文件新建本地组件，不改旧库组件（原因见上）。
2. Section tab 方案：tab 去掉数字，tab 下方不再重复节名，只写 `4 questions in this section`；学生端同步补这一行。
3. 彩条文字颜色按亮度判断：只有 Strongly Disagree 的红色段用白字，其余用深色字。两种颜色在红色上的对比度接近，白字与 PM 参考图一致。
4. 统一 mock 数据：N=38（与页头 38 responses 一致）；5 条陈述改成互不相同（旧稿第 1、4、5 条相同，PRD 不允许重复）；第 2 条故意写长，用来演示 View Details 的 3 行截断；学生端右上 `50 responses` 改为 `38 responses`。
5. `Highest mean` / `Lowest mean` 沿用原来的绿 / 橙描边徽标，只改文案。
6. One response 帧同步改了页头数字（1/62、2% completion、61 unsubmitted）。

需用户确认：

1. Section tab 方案（APAC-6387 写明由设计出方案）。
2. 旧库 `Survey Card / Rating Grid / Teacher / Result`、`Student / Result` 未改；若其他文件还引用旧库组件，那里仍是旧样式。是否需要在库文件里同步、或标记弃用。
3. PM 参考图里有 `Individual responses (24 total)` 和抽屉标题 `View Details (3 total)`，工单没有列为要改的点，本次沿用 `Individual responses`、不带总数。

### 截图

- 改前：`参考截图/2026-10-16-RatingGrid-改前-教师端Identified结果页.png`、`参考截图/2026-10-16-RatingGrid-改前-ViewDetails抽屉.png`
- 改后：`参考截图/2026-10-16-RatingGrid-结果卡片组件集.png`、`参考截图/2026-10-16-RatingGrid-教师端Identified结果页.png`、`参考截图/2026-10-16-RatingGrid-学生端SharedResults.png`、`参考截图/2026-10-16-RatingGrid-ViewDetails抽屉.png`、`参考截图/2026-10-16-RatingGrid-ViewDetails悬停列头.png`、`参考截图/2026-10-16-RatingGrid-ViewDetails全屏.png`
