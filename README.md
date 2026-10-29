# Monee 职场英语

将口语化、零散的中文整理成准确、自然、简洁的商务英语，保留原意、立场和承诺程度。

这是为 Sea-Monee 信贷产品 PMO 工作场景设计的个人 Codex skill，主要支持与老板进行内部聊天，以及编写竞品报告的英文 PPT 文案。

## 两种模式

| 模式 | 适用场景 | 输出特点 |
| --- | --- | --- |
| 聊天 | 确认截止时间、汇报进展、提出请求、反馈问题 | 自然、礼貌、直接；短消息通常一两句 |
| PPT | 竞品数据、业务表现、报告要点 | 简洁标题与平行要点，突出指标、数字和时间 |

PPT 模式负责英文文案，不自动生成幻灯片文件；竞品调研、数据核实和业务建议需要另行提出。

## 安装

在支持 skills 的 Codex 环境中使用。仓库仅包含指令、说明和界面配置，无需额外安装 Python 或 Node.js 依赖。

安装到个人 skills 目录（需要 Git）：

```bash
monee_skills_dir="${CODEX_HOME:-$HOME/.codex}/skills"
monee_skill_dir="$monee_skills_dir/monee-business-english"

if [ -e "$monee_skill_dir" ] || [ -L "$monee_skill_dir" ]; then
  printf '%s\n' "目标目录已存在，未覆盖：$monee_skill_dir"
else
  mkdir -p "$monee_skills_dir"
  git clone https://github.com/theyun63-yvette/monee-business-english.git "$monee_skill_dir"
fi
```

目录约定参考 [OpenAI 官方 Codex 工作流指南](https://developers.openai.com/cookbook/examples/codex/iterating-development-workflows-with-codex) 中的 skill 安装位置说明。安装后在 Codex 中调用 `monee-business-english`；若当前会话尚未识别，可重新打开 Codex 后使用。

## 使用方法

在 Codex 对话中输入 skill 名称和中文内容，可以通过“聊天：”或“PPT：”指定模式：

```text
$monee-business-english 聊天：这个工作您什么时候需要呢？
```

```text
$monee-business-english PPT：粘贴你的中文竞品材料
```

也可以补充本次的受众、语气、长度或公司固定术语。这些明确要求优先于默认设置；不必每次重复填写岗位背景。

默认只输出一版可直接使用的英文。需要更直接、更委婉的版本或中文解释时，在请求中说明即可。

## 示例

### 老板聊天：保留承诺程度

输入：

> 我这边还没拿到最终数字，明天应该能给你，但不敢保证。

输出示例：

> I’m still waiting for the final figures. I expect to be able to share them tomorrow, but I can’t confirm that yet.

保留“预计但未确认”的含义，避免把它改成确定的交付承诺。

### 竞品 PPT：突出数字与口径

以下数据仅用于演示翻译与排版，未经本项目核实。

输入：

> 2025年，抖音生活服务平台GMV同比增长59%，生活服务消费用户数增长22%，支付订单量增长33%；商家动销门店数同比增长47%，达到1520万。

输出示例：

**Douyin’s local services business: 2025 performance**

- **GMV:** +59% YoY
- **Consumers:** +22%
- **Paid orders:** +33%
- **Stores with sales:** 15.2 million (+47% YoY)

用户数和支付订单量的比较基准在原文中未明确，因此暂不补写 YoY。“动销门店”保留产生销售的含义，不直接改为商家数或总门店数。

## 表达规则

- 可以调整句序、合并重复信息，但不新增事实、原因、截止时间或共识。
- 保留请求力度、紧迫性、责任归属和不确定性，不擅自增加道歉或承诺。
- 准确处理“万”“亿”、百分比与百分点、同比与环比，保留来源和限定条件。
- 优先使用常见、准确的英语及用户提供的公司术语，避免机械直译和冗长套话。
- 一般措辞差异直接处理；只有无法保留关键含义的歧义才追问，必要说明放在英文成稿之外。

## 文件结构

```text
monee-business-english/
├── README.md          # 安装、使用与示例
├── SKILL.md           # 核心指令、模式和表达规则
└── agents/
    └── openai.yaml    # Codex 中的显示名称与简介
```

完整行为以 [SKILL.md](SKILL.md) 为准；调整默认背景、语气或术语时编辑该文件，界面名称与简介在 [agents/openai.yaml](agents/openai.yaml) 中维护。
