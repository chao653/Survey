# Rating Grid · 教师端 Results 页 · 状态梳理

- 来源：产品原型 https://survey007.vercel.app/ （`Kira — Survey Prototype · page-states-v1`）
- 抓取日期：2026-09-18
- 页面路径：Teacher → Results（`Midterm Course Feedback — Results`，Anonymous）→ Course Satisfaction 第 1 题 Rating Grid → 右下角「状态」→ 状态切换器 → `Rating Grid · Results`
- 依据：原型页面实际表现 + 原型源码里的 `RG_RESULTS_STATES` / `RG_RESULTS_PAYLOAD` / `RatingGridRows` 三段（源码即原型定义，不是产研正式规则）
- 截图：`需求调研/抓取结果/RatingGrid-Results状态/`
- 结论标注：**原型已定** = 原型里有明确表现；**需确认** = 原型没覆盖或表现与描述有出入，要找产品拍板

---

## 一、卡片骨架（所有状态共用）

| 区域 | 内容 | 备注 |
| --- | --- | --- |
| 卡片头左 | 题型标签 `● Rating Grid`（紫点 + 灰字） | 与 Rating Scale / Multiple choice 卡片同一套 |
| 卡片头右 | 小字 `Compare means` + 粗体 `N statements`；零回收时粗体改为 `No responses yet` | 这是 Rating Grid 独有的头部摘要，Rating Scale 那里对应位置是 ⭐ Mean |
| 题干 | 一行问题文案 | |
| 主体 | 每条陈述一行，行与行之间用分隔线；**没有**题级别的 `Based on N responses` 尾行 | Rating Scale 卡片有题级 Based on，Rating Grid 改成了逐行 Based on |

每一行（一条陈述）的结构，从上到下：

1. `序号. 陈述文案` + 可选的 `Highest` / `Lowest` 小标签
2. 右侧 `Mean` 小字 + `4.3 /5`（紫色粗体 1 位小数 + 灰色 `/量表点数`）
3. 分布条：一条横向堆叠色带，各档按占比分宽度，红→黄→绿渐变（颜色按量表点数插值生成）；某档有人选时最少 3px 宽；hover 显示 `档位标签: xx%`
4. 分布条下方一排量表档位标签（Strongly Disagree … Strongly Agree），等宽居中，9px 灰字，过长截断
5. `Based on N responses`（N=1 时是 `response`）

> 注意：行里**不直接显示各档百分比数字**，只在 hover 时出现；Rating Scale 卡片则是每档都印 `xx%`。见第五节「需确认」。

---

## 二、8 个状态一览

状态切换器里 `Rating Grid · Results` 主题下共 8 个状态，全部标为 `Prototype`（无 `Production` 来源）。

| # | 状态名 | 触发条件（原型描述） | 页面表现 | 截图 |
| --- | --- | --- | --- | --- |
| 1 | Mean comparison | 各条陈述差异明显 | 均值最高行打 `Highest`（绿字 + 整行淡绿底），最低行打 `Lowest`（橙字 + 整行淡橙底） | `01_mean-comparison.png` |
| 2 | Uneven row N | 参与者跳过了部分行 | 每行各自的 `Based on N` 不同（42 / 28 / 19 / 41），Highest / Lowest 照常 | `02_uneven-row-n.png` |
| 3 | Row with N=0 | 某条陈述所有人都跳过 | 该行 Mean 显示 `—`，分布条换成虚线框占位 `No responses for this statement`，不显示档位标签，`Based on 0 responses`；该行不参与 Highest / Lowest 比较 | `03_row-with-n0.png` |
| 4 | Similar means | 差异很小 | 所有行不打 Highest / Lowest，也没有底色 | `04_similar-means.png` |
| 5 | No responses yet | 已发布但零回收 | 主体换成一个虚线框空态：`No responses yet` + `Distribution and means appear once participants answer this question.`；卡片头右侧摘要变 `No responses yet` | `05_no-responses-yet.png` |
| 6 | 8 statements | 到行数上限 | 8 行，卡片拉长，跟随页面滚动，没有折叠 / 分页 | `06_8-statements.png` |
| 7 | 2-point bars | 量表到下限 | 分布条只有红 / 绿两段，标签只有 `Disagree` / `Agree`，Mean 是 `x.x /2` | `07_2-point-bars.png` |
| 8 | 7-point bars | 量表到上限 | 七段色带 + 七个标签（含 Somewhat Disagree / Somewhat Agree），Mean 是 `x.x /7` | `08_7-point-bars.png` |

### 各状态的取数细节（来自原型 mock，便于对照）

- **Mean comparison**：4 行均值 4.27 / 3.53 / 4.15 / 4.10，N = 42 / 40 / 41 / 42 → 第 1 行 Highest、第 2 行 Lowest。
- **Uneven row N**：均值同上，N 改成 42 / 28 / 19 / 41。只影响 Based on 文案。
- **Row with N=0**：第 2 行 `dist` 全 0、`mean: null`、`n: 0`。因为第 2 行被排除，Lowest 移到第 4 行（4.10）。
- **Similar means**：4 行均值**完全相同**（都是 3.82）。见第五节：原型判定「相似」的实现是「全部相等」，不是「差值小于阈值」。
- **No responses yet**：数据是空数组。
- **8 statements**：8 行，5 点量表，均值 4.27 / 3.53 / 4.15 / 4.10 / 3.88 / 4.02 / 3.68 / 4.15。
- **2-point / 7-point**：题目同一批 4 条陈述，只改量表点数与 preset labels。

---

## 三、行级规则（从原型行为归纳）

以下规则来自 `RatingGridRows` 的实际逻辑，Anonymous 与 Identified 两个 Results 页共用同一块。

| 规则 | 内容 | 状态 |
| --- | --- | --- |
| 均值格式 | 1 位小数（4.27 → `4.3`），后缀 `/点数`，点数取该行分布条段数 | 原型已定 |
| 逐行 N | 每行显示自己的 `Based on N responses`，N 为该陈述实际作答人数（跳过不计） | 原型已定 |
| Highest / Lowest 判定 | 只用 N>0 且 mean 非空的行参与；`mean === max` 打 Highest，`mean === min` 打 Lowest；**max === min 时两者都不打** | 原型已定 |
| 并列 | 多行均值同为最高（或最低）时，**这几行都打**同一个标签（代码是相等判断，没有唯一性限制） | 原型已定（但没有对应 demo 状态） |
| 比较精度 | Highest / Lowest 用原始均值比（4.27 vs 4.15），显示用 1 位小数；理论上可能出现两行都显示 `4.2` 但只有一行打 Highest | 需确认 |
| N=0 行 | Mean `—`，虚线占位框，不显示档位标签，Based on 0，**不参与**最高 / 最低比较 | 原型已定 |
| 整题空态 | 数组为空时整块换成空态框；卡片头摘要同步变 `No responses yet` | 原型已定 |
| 分布条 | 段宽 = 该档人数 / 该行总人数；有人选的档最少 3px；hover title `标签: xx%` | 原型已定 |
| 档位标签 | 用题目自定义标签（长度与点数一致时），否则用 preset（agreement / frequency / quality / satisfaction / likelihood / importance）对应点数的标签 | 原型已定 |
| 行高亮底色 | Highest 行 `emerald 4%` 淡绿底，Lowest 行 `amber 4%` 淡橙底，左右各外扩 8px 圆角 | 原型已定 |
| 行数 | 2 ~ 8 行；Results 卡片不做折叠，长了就跟页面一起滚 | 原型已定 |
| 量表点数 | 2 ~ 7 点，分布条段数与标签数随之变化 | 原型已定 |
| Skip logic | 原型里 Skip logic 是 `Not scheduled`，且只影响 Teaching & Materials 一节，Rating Grid 这题不在分支路径上，卡片没有 `Shown to X of Y respondents` 的表现 | 原型未覆盖 |

---

## 四、Identified（实名）Results 页的差异

路径：Teacher → Assignments → `Midterm Course Feedback` → `PHYS 150`（Identified）卡片。截图 `09_identified-individual-responses.png`。

- 上半部分与 Anonymous 完全一致（同一个 `RatingGridRows`），只是卡片头**没有** `● Rating Grid` 题型标签，只保留右侧 `Compare means / N statements`。
- 多一个 `Individual responses (N)` 折叠按钮，N = 在这题至少答了一行的人数。
- 展开后是一张矩阵表（跟 Assessment monitor 的参与者矩阵同款）：
  - 第一列 `Participants`：头像缩写 + 姓名，固定 196px
  - 后面每条陈述一列，列头只显示序号 `1 2 3 4`，hover 列头看完整陈述，固定 56px
  - 单元格 40×40 圆角色块，填该学生选的**档位序号**（1~点数），底色取该档分布条颜色的 20% 透明度
  - 跳过的格子显示 `--`
  - 表下方图例：`Columns are the statements above · cell shows the scale point`、色块 1→点数 + `Strongly Disagree → Strongly Agree`、`-- skipped, not counted in that statement's mean`
- **Identified 页没有接状态切换器**，只有默认那一组数据（等同 Mean comparison）。N=0 行、零回收、2/7 点、8 行这些边界在实名页没有 demo。

---

## 五、需要和产品确认的点

| # | 问题 | 背景 |
| --- | --- | --- |
| 1 | 「Similar means」的判定阈值是多少？ | 状态描述写的是「差异很小 / 均值接近时不强调」，但原型实现是**所有行均值完全相等**才不打标签。真实数据里 3.82 vs 3.83 这种情况按原型会照常打 Highest / Lowest。需要产品给阈值（例如 max − min < 0.1）或明确就按相等处理。 |
| 2 | Highest / Lowest 并列时怎么办？ | 原型会给所有并列行都打标签，没有 demo 状态。需要确认是「都打」还是「都不打」还是「只打第一个」。 |
| 3 | 比较用原始均值还是显示值？ | 见第三节「比较精度」。两行显示同为 `4.2` 却只有一行 Highest，老师会觉得不对。建议比较也按 1 位小数四舍五入后的值。 |
| 4 | 只剩 1 行有数据（其他行 N=0）时要不要打 Highest？ | 按原型逻辑 max === min → 不打。合理，但没有 demo，确认一下。 |
| 5 | 各档百分比要不要直接显示？ | Rating Grid 行里只显示档位标签，百分比要 hover；Rating Scale 卡片每档都印 `xx%`。同一页两种题型信息密度不一致，且 hover 在触屏上不可用。 |
| 6 | 要不要题级别的 `Based on` / 回答人数？ | 卡片头只有 `N statements`，没有「多少人答了这题」。老师想知道整题回收量得自己看各行 N。 |
| 7 | Identified 页的边界状态 | N=0 行、零回收、8 行 × 7 点等边界在实名页的矩阵表里怎么表现（比如零回收时 Individual responses 按钮是否隐藏）原型没覆盖。 |
| 8 | 分布条颜色语义 | 红→绿渐变默认「右边 = 好」。frequency / importance 这类 preset 的右端（Always / Important）不一定是「好」，是否需要按 preset 切换配色，原型没有区分。 |
| 9 | 8 行上限在 Results 卡片里的体验 | 原型是直接拉长跟页面滚。是否需要折叠 / 「展开全部」，看产品对 Results 页整体长度的接受度。 |

---

## 六、截图清单

| 文件 | 内容 |
| --- | --- |
| `01_mean-comparison.png` | 状态 1 · Highest / Lowest 标注 |
| `02_uneven-row-n.png` | 状态 2 · 每行 Based on N 不同 |
| `03_row-with-n0.png` | 状态 3 · 某行 N=0 的占位与 Mean `—` |
| `04_similar-means.png` | 状态 4 · 均值相同，无强调 |
| `05_no-responses-yet.png` | 状态 5 · 整题零回收空态 |
| `06_8-statements.png` | 状态 6 · 8 行上限 |
| `07_2-point-bars.png` | 状态 7 · 2 点量表 |
| `08_7-point-bars.png` | 状态 8 · 7 点量表 |
| `09_identified-individual-responses.png` | Identified 页 · Individual responses 矩阵展开 |

抓取方式：无头 Chrome 1440 宽，隐藏原型的浮动工具栏与状态切换按钮后对卡片元素截图。
