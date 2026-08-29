<p align="center">
  <img src="assets/icon.png" alt="wenbiao-open-prompts" width="128" height="128" />
</p>

<h1 align="center">wenbiao-open-prompts</h1>

<p align="center">
  <strong>文标开源</strong>：招标文件解析 / 评分点拆解 / 技术标目录与章节草稿 Prompt 套件
</p>

<p align="center">
  <a href="https://aiwenbiao.cn">官网</a> ·
  <a href="https://aiwenbiao.cn/guides">方法文</a> ·
  <a href="https://aiwenbiao.cn/sources">官方发布</a> ·
  <a href="LICENSE">MIT License</a>
</p>

---

## 这是什么

`wenbiao-open-prompts` 是面向招投标场景的 **Prompt 工具箱**：把「读标 → 拆分 → 定目录 → 分章写 → 风险检」这套方法，用可复制的 Prompt 形式开源出来。

你可以：

- 拿到 **DeepSeek / GPT / Claude / 本地模型** 里直接用
- 作为团队内部的标准写作流程模板
- 先在本仓库学会「先结构后成文」，再到 [文标官网](https://aiwenbiao.cn) 用完整工作流出稿

## 解决什么问题

写标书最耗时的往往不是打字，而是：

1. **读不清招标文件**：废标项、响应表、评分表散落在几百页里
2. **评分点没拆透**：写了很多，但对不上分、或高分项写太浅
3. **一句话生成全书**：结构偏了就全盘返工，成本极高

本套件的核心思想是：**先拆点、先目录、再分章写草稿**。

## 技术标 6 步（与 Prompt 对应）

| 步骤 | 做什么 | Prompt |
|---|---|---|
| 1 解析 | 抽废标项 / 响应表 / 评分摘要 | [01-tender-parse.md](prompts/01-tender-parse.md) |
| 2 拆分 | 评分点 → 可写章节 + 证据类型 | [02-score-points.md](prompts/02-score-points.md) |
| 3 目录 | 目录对齐评分点，分配字数 | [03-catalog-outline.md](prompts/03-catalog-outline.md) |
| 4 字数 | 按分值粗分篇幅（在 03 中一起完成） | 同上 |
| 5 草稿 | 一次只写一章，降低幻觉 | [04-chapter-draft.md](prompts/04-chapter-draft.md) |
| 6 检查 | 废标项对照 + 高分项覆盖 | [05-risk-check.md](prompts/05-risk-check.md) |

更完整方法论：[docs/methodology.md](docs/methodology.md) · [官网：技术标怎么写](https://aiwenbiao.cn/guides/how-to-write-tech-bid)

## 仓库结构

```text
wenbiao-open-prompts/
  assets/
    icon.png               # 项目图标
    logo.svg               # 文标品牌 SVG
  prompts/
    01-tender-parse.md     # 招标文件解析
    02-score-points.md     # 评分点拆解
    03-catalog-outline.md  # 技术标目录
    04-chapter-draft.md    # 单章草稿
    05-risk-check.md       # 提交前风险检查
  examples/
    sample-score-table.md  # 虚构示例评分表
  docs/
    methodology.md         # 方法论摘要
  CONTRIBUTING.md
  LICENSE                  # MIT
```

## 快速开始（推荐路径）

### 0. 准备

- 任意 LLM（推荐：DeepSeek、GPT、Claude；也可用本地模型）
- 一份招标文件摘录，或至少一张评分表
- 练手可先用 [examples/sample-score-table.md](examples/sample-score-table.md)

### 1. 先拆评分点（最重要）

1. 打开 [prompts/02-score-points.md](prompts/02-score-points.md)
2. 把 System 与 User 复制到对话框
3. 在 User 区粘贴你的评分表
4. 得到：可写章节表 + Top5 高分项 + 风险项

### 2. 定目录

1. 打开 [prompts/03-catalog-outline.md](prompts/03-catalog-outline.md)
2. 把上一步的表格贴进去
3. 得到：二级目录 + 字数分配 + 对照表

### 3. 分章写草稿

1. 用 [prompts/04-chapter-draft.md](prompts/04-chapter-draft.md)
2. **一次只写一章**，写完再换下一章
3. 事实不足时保留「【待补：…】」，不要让模型编造

### 4. 提交前检查

1. 用 [prompts/05-risk-check.md](prompts/05-risk-check.md)
2. 对照废标项与高分项
3. **人工终审** 后再提交

若已有完整招标文件，可先跑 [01-tender-parse.md](prompts/01-tender-parse.md) 再进入上述流程。

## 各 Prompt 简要

### 01 招标文件解析

从摘录中抽：基本信息、废标/否决项、响应表、评分摘要、交付与工期、待确认清单。  
**只解析，不写正文。**

### 02 评分点拆解

输出 Markdown 表：`ID | 评分项 | 分值 | 类型 | 建议章节 | 证据类型 | 摘录 | 风险`。  
再附 Top5 高分项与易失分项。

### 03 技术标目录

目录必须能回指评分点；含字数区间与对照表。  
**先结构，后文字。**

### 04 单章草稿

按章写作；缺事实时用待补占位；禁止编造资质/合同/检测编号。

### 05 提交前风险检查

废标项对照、高分项覆盖、常见硬伤快检、人工必核 Top10。  
**不是法律意见，不能替代合规审核。**

## 使用建议

- **模型选择**：长文档解析偏大上下文窗口；章节草稿可用性价比高的模型
- **温度**：解析/拆分偏低（稳）；草稿可稍高，但仍须人工改
- **分段输入**：招标文件过长时，先贴评分办法与废标章节，再补其他
- **版本管理**：每次 Prompt 输出建议存成独立 Markdown，方便回溯与对比

## 红线（必读）

1. AI 输出只是 **草稿**，须 **人工审核** 后才可提交
2. **不保证中标**，不做任何中标承诺
3. **不编造** 资质、业绩、设备参数、合同编号等事实
4. 涉及密件、审批、价格的内容，以你司合规流程为准

## 与文标产品

| | 本仓库 | [文标](https://aiwenbiao.cn) |
|---|---|---|
| 定位 | 开源 Prompt + 方法论 | 在线写标工作流 |
| 适用 | 自学、团队复制、接入自有 LLM | 上传招标文件 → 拆点 → 导出 |
| 入口 | 本 README | https://aiwenbiao.cn |

两者互补：先用开源 Prompt 理解方法，再用产品提效。

## 贡献

欢迎提 Issue / PR：更稳的 Prompt、更好的表格模板、虚构示例与文档勘误。  
见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## License

[MIT](LICENSE)

## Links

- 官网：https://aiwenbiao.cn
- 技术标怎么写：https://aiwenbiao.cn/guides/how-to-write-tech-bid
- 评分点怎么拆：https://aiwenbiao.cn/guides/split-score-points
- 官方渠道与发布：https://aiwenbiao.cn/sources
- GitHub：https://github.com/hanbon-labs/wenbiao-open-prompts
