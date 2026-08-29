# wenbiao-open-prompts

> 文标开源：招标文件解析 / 评分点拆解 / 技术标目录 Prompt 集

**官网：[https://aiwenbiao.cn](https://aiwenbiao.cn)** · 方法文：[https://aiwenbiao.cn/guides](https://aiwenbiao.cn/guides) · 三方发布：[https://aiwenbiao.cn/sources](https://aiwenbiao.cn/sources)

本仓库**只开源 Prompt 与方法论**，**不包含**文标产品核心代码（读标引擎、代理调度、计费、导出等）。你可以把这些 Prompt 拿到任何 LLM（DeepSeek / GPT / Claude / 本地模型）里用。

## 为什么开源这些

写标书最耗时的不是打字，而是：

1. 把招标文件读清（废标项、响应表、评分表）
2. 把评分点拆成可写章节
3. 先定目录再写正文，避免一句话生成后全盘返工

文标技术标 6 步（详见 [docs/methodology.md](docs/methodology.md) 与 [官网指南](https://aiwenbiao.cn/guides/how-to-write-tech-bid)）：

解析 → 评分点 → 目录 → 字数分配 → 章节草稿 → 风险检查

## 仓库结构

`	ext
wenbiao-open-prompts/
  prompts/
    01-tender-parse.md      # 招标文件解析
    02-score-points.md      # 评分点拆解
    03-catalog-outline.md   # 技术标目录
    04-chapter-draft.md     # 单章草稿
    05-risk-check.md        # 提交前风险检查
  examples/
    sample-score-table.md   # 示例评分表（虚构）
  docs/
    methodology.md          # 方法论
  CONTRIBUTING.md
  LICENSE                   # MIT
`

## 快速开始

1. 打开 [prompts/02-score-points.md](prompts/02-score-points.md)
2. 把你的评分表（或招标文件摘录）贴进 User 区
3. 用任意 LLM 跑一遍，先得到「可写章节清单」
4. 再用 [03](prompts/03-catalog-outline.md) / [04](prompts/04-chapter-draft.md) 往下写
5. 提交前跑 [05-risk-check.md](prompts/05-risk-check.md)

若需要工作流产品（上传招标文件→自动拆点→导出 Word），请直接用：**[https://aiwenbiao.cn](https://aiwenbiao.cn)**

## 红线（必读）

1. AI 输出只是**草稿**，须**人工审核**后才可提交
2. **不保证中标**，不做任何中标承诺
3. **不编造**资质、业绩、设备参数、合同编号等事实
4. 涉及密件、审批、价格的内容，以你司的合规流程为准

## 与产品的关系

| | 本仓库 | 文标产品 |
|---|---|---|
| 内容 | Prompt + 方法 | 完整工作流 |
| 代码 | 无产品核心 | 闭源 |
| 适用 | 自学 / 团队内部复制 | 上传标书直接出稿 |
| 链接 | 本 README | [aiwenbiao.cn](https://aiwenbiao.cn) |

## License

[MIT](LICENSE)

## Links

- 官网：https://aiwenbiao.cn
- 技术标怎么写：https://aiwenbiao.cn/guides/how-to-write-tech-bid
- 官方渠道与发布：https://aiwenbiao.cn/sources
