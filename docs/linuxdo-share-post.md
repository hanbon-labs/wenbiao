# 我把「标书评分点拆解」做成了开源 Prompt 工作流（wenbiao）

> 适用：linux.do 分享创造 / 开源
> 仓库：https://github.com/hanbon-labs/wenbiao
> 官网：https://aiwenbiao.cn
> License：MIT · Release：https://github.com/hanbon-labs/wenbiao/releases/tag/v0.1

![wenbiao](https://raw.githubusercontent.com/hanbon-labs/wenbiao/main/assets/og-card.png)

---

## 0. 先说清楚：这不是另一个「AI 写标书神器」广告

做技术标时，最痛的不是「会不会写」，而是：

1. 招标文件里的**评分点** 没拆清楚，就开始写长文
2. 章节写得很漂亮，但**对不上分**
3. 模型容易**空编业绩 / 资质**，后面人工改到崩

所以我把一套「**先拆评分点，再写技术标**」的阶段工作流开源了：

- 仓库名：**wenbiao**
- 产品名：**文标**（只有中文名）
- 开源内容：5 个可复制 Prompt + 虚构评分表 / 拆解示例 + harness 架构说明
- 你可以：拿 DeepSeek / GPT / Claude / 任意 LLM **直接粘贴用**

> **红线**：AI 输出只是**草稿**，须**人工审核**；**不保证中标**；**不编造** 资质 / 业绩 / 检测编号。

如果觉得有用，欢迎 **Star / Fork**：https://github.com/hanbon-labs/wenbiao

---

## 1. 为什么不要「一句话生成全书」

| 纯聊天框 | 本仓库工作流 |
| --- | --- |
| 一次对话生成全书，结构偏了全盘返工 | 先拆点、先目录，再分章写 |
| 中断后难恢复 | 每阶段产出可落盘、可复用 |
| 看不清做到哪一步 | 5 个 Prompt 对应 5 个阶段 |
| 容易编造业绩资质 | Prompt 写死：缺事实写「待补」 |
| 责任边界模糊 | 输出是草稿，责任在投标人 |

核心句：**评分点没拆清，就不要开写长文。**

---

## 2. 总体架构（开源 vs 产品）

开源解决「方法 + Prompt」；官网解决「上传文件后自动跑完整链路」。

![开源 vs 产品](https://raw.githubusercontent.com/hanbon-labs/wenbiao/main/assets/linuxdo/arch-open-vs-product.png)

### 2.1 harness agent（产品侧架构标签）

**harness agent** 是工作流架构标签，不是英文产品名。产品正式名称是 **文标**。

> Harness Agent = 意图路由 + 阶段化 Run/Job + Worker 执行 + 事件可观测 + 人工审稿闸口。

![harness agent](https://raw.githubusercontent.com/hanbon-labs/wenbiao/main/assets/linuxdo/arch-harness.png)

三道人工闸口：**目录确认 → 章节审稿 → 导出前终审**。

---

## 3. 仓库结构与五阶段

```text
wenbiao/
  README.md
  docs/harness-agent.md
  docs/methodology.md
  prompts/01-tender-parse.md
  prompts/02-score-points.md   # core
  prompts/03-catalog-outline.md
  prompts/04-chapter-draft.md
  prompts/05-risk-check.md
  examples/sample-score-table.md
  examples/sample-score-breakdown.md
  assets/
```

![5 阶段](https://raw.githubusercontent.com/hanbon-labs/wenbiao/main/assets/linuxdo/flow-5steps.png)

| 步 | Prompt | 产出 |
| --- | --- | --- |
| 1 | [01-tender-parse](https://github.com/hanbon-labs/wenbiao/blob/main/prompts/01-tender-parse.md) | 废标项、评分摘要、待确认 |
| 2 | [02-score-points](https://github.com/hanbon-labs/wenbiao/blob/main/prompts/02-score-points.md) | 可写章节表 + Top5 |
| 3 | [03-catalog-outline](https://github.com/hanbon-labs/wenbiao/blob/main/prompts/03-catalog-outline.md) | 目录 + 评分点对照 |
| 4 | [04-chapter-draft](https://github.com/hanbon-labs/wenbiao/blob/main/prompts/04-chapter-draft.md) | 单章草稿（缺事实写「待补」） |
| 5 | [05-risk-check](https://github.com/hanbon-labs/wenbiao/blob/main/prompts/05-risk-check.md) | 废标对照 / 覆盖 / Top10 |

---

## 4. 10 分钟实操（任意 LLM）

下面按「打开 → 复制 → 粘贴 → 对照」，图已嵌入，可直接复制发帖。

![实操时序](https://raw.githubusercontent.com/hanbon-labs/wenbiao/main/assets/linuxdo/flow-sequence.png)

### Step 1：打开虚构评分表

https://github.com/hanbon-labs/wenbiao/blob/main/examples/sample-score-table.md

![sample-score-table](https://raw.githubusercontent.com/hanbon-labs/wenbiao/main/assets/linuxdo/shot-sample-score-table.png)

| 序号 | 评分项 | 分值 | 说明 |
|---|---|---|---|
| 1 | 总体技术方案 | 10 | 完整性、针对性 |
| 2 | 实施方案与进度 | 8 | 计划可执行 |
| 3 | 质量保证措施 | 6 | 过程与验收 |
| 4 | 售后服务方案 | 6 | 响应时效 |
| 5 | 项目团队配置 | 5 | 岗位与经验（勿编造） |
| 6 | 风险识别与应对 | 5 | 针对性 |

### Step 2：复制「02 · 评分点拆解」 Prompt

https://github.com/hanbon-labs/wenbiao/blob/main/prompts/02-score-points.md

![prompts/02-score-points](https://raw.githubusercontent.com/hanbon-labs/wenbiao/main/assets/linuxdo/shot-prompt-02.png)

把 System + User 整段复制到 DeepSeek（或任意聊天框），再把评分表贴到 User 末尾。

```text
你是技术标评分点拆解助手。目标是把每一条评分点变成可执行的写作任务。
规则：不写大段正文；不编造业绩资质；客观/主观分开；输出 Markdown 表。

| ID | 评分项 | 分值 | 类型 | 建议章节 | 证据类型 | 原文摘录 | 风险 |

再给：Top5；易废标/失分 3 条；章节优先顺序。
```

### Step 3：粘到 LLM（示意对话）

![LLM 对话示意](https://raw.githubusercontent.com/hanbon-labs/wenbiao/main/assets/linuxdo/shot-llm-chat.png)

> 上图是按仓库示例做的**效果示意**（虚构评分表），你可用 DeepSeek / GPT / Claude 照同样步骤复现。AI 草稿须人工审核。

### Step 4：对照示例输出

https://github.com/hanbon-labs/wenbiao/blob/main/examples/sample-score-breakdown.md

![sample-score-breakdown](https://raw.githubusercontent.com/hanbon-labs/wenbiao/main/assets/linuxdo/shot-sample-breakdown.png)

你跑出来的表，应接近示例：每条有 ID / 建议章节 / 证据类型 / 风险备注；并有 Top5 与「易废标/失分」提示。

### Step 5：03 → 人工改目录 → 04（一章一章） → 05

1. 把拆解表贴进 [03](https://github.com/hanbon-labs/wenbiao/blob/main/prompts/03-catalog-outline.md)
2. **人工改目录**
3. [04](https://github.com/hanbon-labs/wenbiao/blob/main/prompts/04-chapter-draft.md) **一次只写一章**；缺事实写「待补」
4. [05](https://github.com/hanbon-labs/wenbiao/blob/main/prompts/05-risk-check.md) 提交前风险检查

---

## 5. 「先拆再写」 vs 「先写后对分」

![先拆 vs 先写](https://raw.githubusercontent.com/hanbon-labs/wenbiao/main/assets/linuxdo/compare-first-score.png)

| 先写后对分 | 先拆评分点再写 |
| --- | --- |
| 章节好看但对不上分 | 每章挂评分点 ID |
| 高分项漏响应 | Top5 先写 |
| 模型容易空编 | 「待补」占位 |
| 返工成本高 | 目录确认后再扩写 |

---

## 6. 开源仓库 vs 官网产品

| | wenbiao（开源） | 文标（产品） |
| --- | --- | --- |
| 重点 | Prompt + 方法 + 示例 | 上传后自动跑链路 |
| 适用 | 自学 / 团队 / 自有 LLM | 快速出可改草稿 |
| 许可 | MIT | 产品服务条款 |
| 链接 | https://github.com/hanbon-labs/wenbiao | https://aiwenbiao.cn |

站内方法文：

- https://aiwenbiao.cn/guides/split-score-points
- https://aiwenbiao.cn/guides/half-day-first-draft
- https://aiwenbiao.cn/guides/how-to-write-tech-bid

Discussion：https://github.com/hanbon-labs/wenbiao/discussions/1

---

## 7. 红线

1. AI 只是草稿，须人工审核
2. 不保证中标
3. 不编造资质 / 业绩 / 参数 / 编号
4. 密件、审批、价格以你司合规为准

---

## 8. 求 Star / Fork

1. **Star**：https://github.com/hanbon-labs/wenbiao
2. **Fork** 到自己账号，按行业改 Prompt
3. Issue / Discussion

---

## 友链 / 社区认可

本项目积极参与并认可 [LINUX DO](https://linux.do) 社区（[linux.do](https://linux.do)）。

---

*仓库 https://github.com/hanbon-labs/wenbiao · 官网 https://aiwenbiao.cn · 不构成中标承诺.*
