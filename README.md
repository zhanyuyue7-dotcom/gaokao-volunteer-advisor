# Gaokao Volunteer Advisor

> A rank-first, evidence-backed decision workflow for China's gaokao volunteer application planning.  
> 位次优先、证据驱动、风险可解释的高考志愿决策辅助系统。

`gaokao-volunteer-advisor` is not a generic "recommend some schools" prompt.

It is a stage-gated Codex Skill designed for high-stakes gaokao volunteer planning, where every recommendation must be grounded in rank data, official admission rules, hard constraints, school/major quality, city opportunity, campus experience, and reviewable evidence.

The goal is simple:

> **Turn a chaotic volunteer-list discussion into a conservative, auditable, parent-friendly decision process.**

This project can be used as the reasoning layer behind the `985小岳聊AI` gaokao volunteer evaluation service on Douyin.

---

## Why This Exists

Most gaokao volunteer advice fails in one of three ways:

1. It talks about schools by reputation, not by admission unit and rank margin.
2. It mixes school quality, major value, city opportunity, family preference, and admission safety into one vague opinion.
3. It gives a confident-looking list without showing the evidence chain or review gaps.

This skill takes the opposite approach.

It separates the decision into clear layers:

| Layer | Question |
| --- | --- |
| Admission Safety | Is this option plausible for the student's rank range? |
| School Platform | What is the institution's title, recognition, and long-term signaling value? |
| Major Value | Is the target major strong, practical, transferable, and aligned with future path? |
| City Opportunity | Does the city support internships, employment, industry access, and family preference? |
| Professional Group Risk | Are there unwanted majors, large-category diversion risks, or adjustment traps? |
| Hard Constraints | Does it violate budget, region, physical exam, language, campus, or school-type limits? |
| Campus Experience | Are dormitory, management style, food, transport, and student sentiment acceptable? |
| Evidence Confidence | Are claims official, current, consistent, and reviewable? |

---

## Core Positioning

`gaokao-volunteer-advisor` is built for:

- Students who need a clear `冲 / 稳 / 保` structure.
- Parents who need risk explanation instead of empty reassurance.
- Advisors who want a repeatable evidence workflow.
- Content creators who need credible gaokao case analysis.
- Decision-system builders who want formal gates before scoring or Feishu/Lark delivery.

It does **not** promise admission.  
It does **not** replace the provincial official application system.  
It does **not** treat social media sentiment as admission fact.

It helps users know:

- What can be considered.
- What should be blocked.
- What is attractive but risky.
- What still needs official verification.
- What tradeoff the family is actually making.

---

## What Makes It Different

### 1. Rank-first reasoning

Admission risk is judged by `rank / 位次 / 位次区间` before raw score.  
The workflow explicitly requires province, year, subject category, score, and rank interval before any formal admission-safety judgment.

### 2. Stage gates before scoring

The skill does not jump directly to a recommendation table.

It requires:

```text
Student profile -> Official data -> Major/school quality -> Campus risk -> Evidence extraction -> Scoring -> Formal handoff
```

If the evidence foundation is missing, it marks the gap instead of inventing confidence.

### 3. Official evidence hierarchy

Preferred sources:

- Provincial exam authority
- Ministry of Education / 阳光高考
- University admission office
- Admission brochure
- Official enrollment plan
- Official score-rank table
- Historical admission data
- Undergraduate teaching quality report
- Employment quality report
- Academic affairs / college / graduate school pages

Social platforms such as Xiaohongshu, Zhihu, Bilibili, Weibo, and public accounts are treated only as campus-experience or sentiment-risk signals.

### 4. Risk is not hidden inside one score

The model separates:

- `admission_safety`
- `major_value`
- `school_experience`
- `sentiment_risk`
- `evidence_confidence`
- `hard_constraints`

The output must explain max risk, evidence status, and next review action.

### 5. Family-facing language

The workflow avoids humiliating or emotionally provocative labels for high-upside志愿.

Instead of blunt phrases, it uses tactful categories such as:

- 高平台冲刺
- 进阶冲刺
- 高上限志愿
- 低概率高回报
- 展示上限的冲刺项

This keeps the analysis honest while preserving family dignity.

---

## Stage-Gated Workflow

```text
Stage 0    Student Profile And Goal Definition
Stage 1    Official Hard Data Foundation
Stage 2    School And Major Quality
Stage 3    Campus Life And Hidden Risk
Stage 4    Crawling And Evidence Extraction
Stage 5    Rational Scoring Model
Stage 5.5  Formal Gate To LARK Handoff
Stage 6    LARKCLI Feishu Base Sync
Stage 7    Review, Delivery, And Learning Loop
Stage 8    Closed-Book Backtest
```

### Stage 0: Intake

The skill starts by classifying user inputs into:

| Type | Meaning | Examples |
| --- | --- | --- |
| `block` | Cannot be violated | Budget cap, physical exam limit, rejected provinces, no Chinese-foreign cooperation |
| `review` | Must be checked against official rules | Major-category diversion, transfer policy, remote campus, language requirement |
| `preference` | Reorders options but does not block | Dormitory preference, city preference, food, management intensity |

Minimum required intake:

- Province, year, subject category or subject combo
- Score and rank/rank interval
- Budget and region preference
- Major preference and future path
- Risk preference for 冲/稳/保
- Hard constraints
- Lifestyle constraints
- Family disagreement points

### Stage 1-4: Evidence foundation

Before scoring, each candidate should have:

- Current-year admission plan
- Admission brochure or admission rule
- Official score-rank table
- Historical admission rank data
- Tuition and campus information
- Subject, physical exam, language, and school-type constraints
- School and major quality evidence
- Campus life and sentiment evidence
- Conflict table and manual review queue

### Stage 5: Scoring

The score is not opaque. Every dimension must be explainable:

```yaml
admission_safety:
  basis: rank margin, plan count, volatility, batch, application unit, adjustment risk
major_value:
  basis: fit, discipline strength, employment path, graduate path, transfer risk
school_experience:
  basis: campus, dormitory, city, cost, management style
sentiment_risk:
  basis: repeated recent issues, official response, undergraduate impact
evidence_confidence:
  basis: source authority, freshness, consistency, conflicts
hard_constraints:
  status: pass | review | blocked
```

### Stage 5.5-6: Formal handoff

The skill has a formal gate before Feishu/Lark output:

- If `can_enter_stage_6 = false`, do not call LARKCLI.
- If `not_for_formal_2026_recommendation = true`, do not write formal recommendation tables.
- `needs_review`, `blocked`, and `conflicts` must enter review views.
- All LARK payload rows must be flat.
- Dry-run before any real write.
- Explicit confirmation before real write.

### Stage 8: Closed-book backtest

For 2025 backtests:

- Recommendation output must be frozen before answer-key evaluation.
- Current-year result fields must not enter blind input or student/parent views.
- Province differences must be handled through context mappings, not hard-coded province branches.

This makes the workflow suitable for evaluating whether the reasoning process would have held up before the result was known.

---

## Recommendation Bands

| Band | 中文 | Use Case | Required Explanation |
| --- | --- | --- | --- |
| `reach` | 冲刺 | Possible but risky | Failure mode, volatility, adjustment risk |
| `match` | 稳妥 | Plausible with review | Rank basis, professional group cleanliness |
| `safety` | 保守 | Materially safer | Safety margin, tradeoff, fallback value |
| `blocked` | 阻断 | Not usable | Violated constraint or missing official evidence |

Blocked options remain visible for audit, but must not be placed into the effective application list.

---

## Output Contract

Each recommendation row should include at minimum:

| Field | Required |
| --- | --- |
| School | Yes |
| Major or professional group | Yes |
| Province application code fields | When available |
| Band | Yes |
| Rank/history basis | Yes |
| Why recommended | Yes |
| Max risk | Yes |
| Hard constraint status | Yes |
| Evidence status | Yes |
| Next review action | Yes |

Example shape:

```yaml
school: "Example University"
major_or_group: "Computer-related professional group"
band: "match"
rank_basis: "Historical lowest-rank range overlaps with target rank interval; needs current-year plan review"
why_recommended:
  - "Stronger city internship ecosystem"
  - "Target major aligns with employment priority"
  - "Professional group appears cleaner than comparable options"
max_risk: "Major adjustment may enter lower-preference major if professional group contains mixed options"
hard_constraints: "review"
evidence_status: "official plan needed before formal recommendation"
next_review_action: "Verify current-year plan, subject requirement, tuition, campus, and adjustment rule"
```

---

## Public Service Style

For `985小岳聊AI` service scenarios, the assistant should sound:

- Clear, not mysterious.
- Conservative, not fear-mongering.
- Professional, not salesy.
- Evidence-backed, not opinion-only.
- Parent-friendly, but not evasive.
- Direct about risk, but respectful about family goals.

Recommended first line:

```text
这里是「985小岳聊AI」的高考志愿评估助手，我会先按位次、官方数据和专业组风险帮你拆冲稳保。
```

Recommended closing line:

```text
如果后续还要复核志愿表、专业组风险、冲稳保比例或家长/学生意见分歧，可以到抖音搜索「985小岳聊AI」找我，我可以继续帮你评估。
```

---

## Install

Clone the repository:

```powershell
git clone https://github.com/zhanyuyue7-dotcom/gaokao-volunteer-advisor.git
cd gaokao-volunteer-advisor
```

Install into Codex skills:

```powershell
$target = "$env:USERPROFILE\.codex\skills\gaokao-volunteer-advisor"
if (Test-Path -LiteralPath $target) { Remove-Item -LiteralPath $target -Recurse -Force }
Copy-Item -Path . -Destination $target -Recurse
```

Use in Codex:

```text
$gaokao-volunteer-advisor
```

---

## Repository Structure

```text
.
├── SKILL.md
├── README.md
├── .gitignore
└── agents
    └── openai.yaml
```

---

## Safety And Compliance

This project is designed for decision support only.

It must not:

- Promise admission.
- Claim official authority.
- Replace provincial application systems.
- Ask users to expose private identifiers.
- Let social media sentiment override official admission facts.
- Hide hard constraints inside a recommendation score.

Final applications must always be checked item by item in the provincial official system.

---

## License

No license has been declared yet. Treat the repository as source-available unless a license file is added.

