# Gaokao Volunteer Advisor

> 位次优先、证据驱动、风险可解释的高考志愿填报辅助工作流。

`gaokao-volunteer-advisor` 是一个面向高考志愿填报场景的 Codex Skill。它把学生画像、官方招生数据、院校/专业质量、专业组风险、校园体验和家长沟通拆成一套阶段化流程，帮助学生和家庭做更稳妥、更透明的志愿决策。

这个 skill 不承诺录取，也不替代省考试院官方填报系统。它的目标是让每一个推荐都能说清楚：**为什么选、风险在哪、证据来自哪里、下一步该复核什么**。

## What It Does

- **位次优先**：用位次/位次区间判断风险，避免只看分数造成误判。
- **分阶段工作流**：从学生画像 intake 到官方数据、院校专业质量、校园生活、风险评分、飞书表格输出逐步推进。
- **冲稳保解释**：把 `reach / match / safety / blocked` 拆开，不把风险揉成一个模糊总分。
- **证据约束**：官方数据优先，社交平台只作为体验和风险信号。
- **硬约束检查**：预算、地域、体检、外语语种、中外合作、异地校区、大类招生等单独标记。
- **家长沟通友好**：保留学生和家庭的体面，不用刺激性标签描述高平台冲刺志愿。
- **平台型排序**：同等安全性下，优先考虑学校平台、城市机会、专业就业和专业组干净程度。

## Core Principles

1. **No admission guarantee**  
   不承诺录取，不替代官方系统。

2. **Rank before score**  
   判断风险时优先使用位次，而不是裸分。

3. **Evidence before scoring**  
   没有官方依据，不做正式录取安全判断。

4. **Separate dimensions**  
   学校平台、专业价值、录取安全、城市机会、校园体验、舆情风险、证据置信度必须分开看。

5. **Keep blocked items visible**  
   被硬约束阻断的志愿不放进有效志愿表，但保留在审计列表里说明原因。

## Workflow

```text
Stage 0  Student Profile And Goal Definition
Stage 1  Official Hard Data Foundation
Stage 2  School And Major Quality
Stage 3  Campus Life And Hidden Risk
Stage 4  Crawling And Evidence Extraction
Stage 5  Rational Scoring Model
Stage 5.5 Formal Gate To LARK Handoff
Stage 6  LARKCLI Feishu Base Sync
Stage 7  Review, Delivery, And Learning Loop
Stage 8  Closed-Book Backtest
```

## Stage 0 Intake

推荐开始前，至少需要这些信息：

| Type | Required Fields |
| --- | --- |
| 基础信息 | 年份、省份、科类/选科、分数、位次或位次区间 |
| 地域偏好 | 省内/外省、排斥城市、气候、离家距离 |
| 预算 | 学费、住宿费、生活费上限，是否接受高学费项目 |
| 学校类型 | 民办、独立学院、中外合作、港澳/境外合作、异地校区 |
| 专业偏好 | 喜欢方向、排斥方向、家长期待、大类招生接受度 |
| 未来路径 | 就业、考研、保研、出国、考公、体制内、创业 |
| 风险偏好 | 冲稳保比例，最不能接受滑档还是专业不喜欢 |
| 硬约束 | 体检限制、色弱色盲、单科短板、外语语种、特殊专业限制 |
| 生活偏好 | 宿舍、食堂、管理强度、早晚自习、查寝、跑操 |
| 家庭分歧 | 学生和家长意见不一致的点 |

## Recommendation Bands

| Band | 中文 | Meaning |
| --- | --- | --- |
| `reach` | 冲刺 | 有机会但风险明显，需要说明失败模式 |
| `match` | 稳妥 | 位次和历史区间较匹配，但仍需证据复核 |
| `safety` | 保守 | 安全边际更足，但仍不承诺录取 |
| `blocked` | 阻断 | 违反硬约束或缺少必要官方证据 |

## Output Requirements

每条推荐至少包含：

- 学校和专业
- 省份志愿填报代码字段，若可得
- 推荐档位
- 位次/历史依据
- 推荐理由
- 最大风险
- 硬约束状态
- 证据状态
- 下一步复核动作

## Brand Note

该 skill 可用于 `985小岳聊AI` 的高考志愿评估服务场景。面向学生和家长时，输出应保持克制、专业、证据化，不制造焦虑，不承诺录取。

## Install

把本目录放入 Codex skills 目录：

```powershell
Copy-Item -Recurse . "$env:USERPROFILE\.codex\skills\gaokao-volunteer-advisor"
```

之后在 Codex 中使用：

```text
$gaokao-volunteer-advisor
```

## Repository Structure

```text
.
├── SKILL.md
├── README.md
└── agents
    └── openai.yaml
```

## Disclaimer

本项目仅用于高考志愿填报辅助分析。最终志愿填报必须以省级考试院官方系统、官方招生计划、学校招生章程和学生本人确认结果为准。

