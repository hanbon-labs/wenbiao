# 开源：标书评分点拆解 Prompt (wenbiao / MIT)

**GitHub**: https://github.com/hanbon-labs/wenbiao
**官网**: https://aiwenbiao.cn

![封面](https://cdn.jsdelivr.net/gh/hanbon-labs/wenbiao@main/assets/og-card.png)

---

## 1. 这个仓库解决什么

做技术标最常见的坑：**评分点还没拆清，就开写长文**

开源了一套「先拆点、再分章写」 Prompt:

- 5 Prompt (DeepSeek / GPT / Claude)
- 虚构评分表 + 拆解示例
- 产品 **文标** / repo **wenbiao**

> 红线：AI 草稿须人工审核；不保证中标；不编造

---

## 2. 五步怎么跑

![五阶段](https://cdn.jsdelivr.net/gh/hanbon-labs/wenbiao@main/assets/linuxdo/flow-5steps.png)

1. 01 解析
2. 02 拆评分点
3. 03 目录 -> 人工确认
4. 04 单章
5. 05 风险检查

---

## 3. 10 分钟实操

### 3.1 打开评分表

https://github.com/hanbon-labs/wenbiao/blob/main/examples/sample-score-table.md

![评分表](https://cdn.jsdelivr.net/gh/hanbon-labs/wenbiao@main/assets/linuxdo/shot-sample-score-table.png)

### 3.2 复制 Prompt 02

https://github.com/hanbon-labs/wenbiao/blob/main/prompts/02-score-points.md

![Prompt 02](https://cdn.jsdelivr.net/gh/hanbon-labs/wenbiao@main/assets/linuxdo/shot-prompt-02.png)

粘到 LLM, 再贴评分表.

### 3.3 得到拆解表

![LLM](https://cdn.jsdelivr.net/gh/hanbon-labs/wenbiao@main/assets/linuxdo/shot-llm-chat.png)

![示例输出](https://cdn.jsdelivr.net/gh/hanbon-labs/wenbiao@main/assets/linuxdo/shot-sample-breakdown.png)

对照: https://github.com/hanbon-labs/wenbiao/blob/main/examples/sample-score-breakdown.md

### 3.4 接着

- 03 目录 -> 人工改
- 04 一次一章; 缺事实写「待补」
- 05 检查

---

## 4. 开源 vs 官网

| | wenbiao | 文标 |
| --- | --- | --- |
| | Prompt+方法 | 上传自动跑 |
| | https://github.com/hanbon-labs/wenbiao | https://aiwenbiao.cn |

---

## 5. Star / 友链

Star: https://github.com/hanbon-labs/wenbiao

本项目认可 [LINUX DO](https://linux.do)

