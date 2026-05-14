---
name: management-framework-selector
description: "管理框架智能选择器 - 根据任务特征自动选择并应用PDCA/SMART/SWOT/5W2H等管理框架 | Intelligent management framework selector - automatically select and apply PDCA/SMART/SWOT/5W2H frameworks based on task characteristics"
version: 1.0.0
author: Mr.Von + WorkBuddy
updated: 2026-05-14
agent_created: true
---

# 管理框架选择器 v1.0 | Management Framework Selector v1.0

根据用户任务特征，智能选择并应用合适的管理框架（PDCA/SMART/SWOT/5W2H），支持后续添加新的管理工具。
Intelligently select and apply suitable management frameworks (PDCA/SMART/SWOT/5W2H) based on user task characteristics. Supports adding new frameworks later.

---

## 触发条件 | Trigger Conditions

**中文触发词** — 当用户说以下任一关键词时，加载此Skill：
- "管理XX项目/任务" / "Manage XX project/task"
- "规划XX" / "Plan XX"
- "分析XX问题" / "Analyze XX problem"
- "拆解XX任务" / "Break down XX task"
- "用PDCA/SMART/SWOT/5W2H"
- "制定XX目标/计划" / "Set XX goal/plan"

**English trigger keywords** — Load this skill when user says:
- "manage XX project/task"
- "plan XX" / "create a plan for XX"
- "analyze XX problem"
- "break down XX task"
- "use PDCA/SMART/SWOT/5W2H"
- "set a SMART goal for XX"
- "swot analysis for XX"
- "create a project framework for XX"

---

## 框架选择矩阵 | Framework Selection Matrix

| Task Characteristics | Recommended Framework | Description |
|---------|---------|------|
| 项目执行、有阶段性、需要闭环 <br> Project execution, phased, needs closure | **PDCA** | Plan→Do→Check→Act cycle |
| 目标设定、KPI制定、需要可衡量 <br> Goal setting, KPI definition, needs measurability | **SMART** | Specific/Measurable/Achievable/Relevant/Time-bound |
| 战略分析、竞品分析、环境分析 <br> Strategic analysis, competitor analysis, environment analysis | **SWOT** | Strengths/Weaknesses/Opportunities/Threats |
| 问题拆解、原因分析、信息收集 <br> Problem breakdown, root cause analysis, info gathering | **5W2H** | What/Why/Who/When/Where/How/How much |
| 复杂任务（多维度）<br> Complex tasks (multi-dimensional) | **PDCA + SWOT Combo** | Strategy + Execution |

**选择流程 | Selection Process**：
1. 分析用户意图和任务特征 / Analyze user intent and task characteristics
2. 对照上方矩阵，推荐1-2个框架 / Recommend 1-2 frameworks based on the matrix above
3. 展示推荐理由，等待用户确认 / Show recommendation reasoning, wait for user confirmation
4. 用户确认后，加载对应框架的详细流程 / After user confirms, load detailed flow of the corresponding framework

---

## 框架1：PDCA（项目执行闭环）| Framework 1: PDCA (Project Execution Loop)

### 适用场景 |适用场景
- 项目有清晰的阶段性 / Project has clear phases
- 需要执行→检查→改进的闭环 / Needs execute→check→improve loop
- 周期性任务（如月度报告、季度复盘）/ Periodic tasks (monthly reports, quarterly reviews)

### 执行流程 | Execution Flow

#### P - Plan（计划阶段 | Plan Phase）
创建以下任务（使用TaskCreate）| Create the following tasks (using TaskCreate):
1. **"P-定义项目目标" | "P-Define project goals"**
   - 描述：明确项目最终交付物、成功标准 | Define final deliverables, success criteria
   - activeForm: "定义项目目标中" | "Defining project goals"
   
2. **"P-制定执行计划" | "P-Create execution plan"**
   - 描述：拆解任务清单、时间表、资源分配 | Break down task list, timeline, resource allocation
   - activeForm: "制定执行计划中" | "Creating execution plan"
   
3. **"P-识别风险与依赖" | "P-Identify risks & dependencies"**
   - 描述：列出潜在风险、依赖项、应急预案 | List potential risks, dependencies, contingency plans
   - activeForm: "识别风险中" | "Identifying risks"

完成后，向用户展示计划，等待确认进入Do阶段。
After completion, show the plan to the user, wait for confirmation before entering Do phase.

#### D - Do（执行阶段 | Do Phase）
1. **"D-执行任务1~N" | "D-Execute tasks 1~N"** (根据P阶段的计划创建 | Created based on P-phase plan)
   - 逐个标记in_progress，执行后标记completed | Mark in_progress one by one, mark completed after execution
   
2. **"D-记录执行过程" | "D-Record execution process"**
   - 描述：记录关键决策、问题、偏差 | Record key decisions, issues, deviations
   - activeForm: "记录执行过程中" | "Recording execution process"

#### C - Check（检查阶段 | Check Phase）
1. **"C-对比实际vs计划" | "C-Compare actual vs plan"**
   - 描述：对比进度、质量、成本与计划的偏差 | Compare schedule, quality, cost vs plan deviations
   - activeForm: "对比分析中" | "Comparing and analyzing"
   
2. **"C-分析问题根因" | "C-Analyze problem root cause"**
   - 描述：用5Why法或鱼骨图分析偏差原因 | Use 5Why or fishbone diagram to analyze deviation causes
   - activeForm: "分析根因中" | "Analyzing root cause"

#### A - Act（改进阶段 | Act Phase）
1. **"A-制定改进措施" | "A-Formulate improvement actions"**
   - 描述：针对C阶段发现的问题，制定改进行动 | Formulate improvement actions for problems found in C phase
   - activeForm: "制定改进措施中" | "Formulating improvement actions"
   
2. **"A-更新流程文档" | "A-Update process documentation"**
   - 描述：将改进措施固化到标准流程 | Embed improvement measures into standard process
   - activeForm: "更新流程文档中" | "Updating process documentation"

#### PDCA循环完成 | PDCA Cycle Complete
询问用户 | Ask the user:
- "本轮PDCA完成，是否开始下一轮？（进入新的Plan阶段）" | "This PDCA cycle is complete. Start the next round? (Enter new Plan phase)"
- "还是需要调整策略？" | "Or need to adjust the strategy?"

---

## 框架2：SMART（目标设定）| Framework 2: SMART (Goal Setting)

### 适用场景 | Applicable Scenarios
- 设定KPI、OKR / Set KPIs, OKRs
- 制定项目目标 / Define project goals
- 需要可衡量的结果 / Need measurable results

### 执行流程 | Execution Flow

#### S - Specific（具体 | Specific）
询问并明确 | Ask and clarify:
- 目标是什么？（不能是"提高质量"这类模糊表述）/ What is the goal? (Cannot be vague like "improve quality")
- 涉及哪些人/部门？/ Which people/departments are involved?
- 边界在哪里？/ Where are the boundaries?

输出：具体的目标描述（1-2句话）| Output: Specific goal description (1-2 sentences)

#### M - Measurable（可衡量 | Measurable）
协助用户设定 | Help user set:
- 定量指标（数字、百分比、时间）/ Quantitative metrics (numbers, percentages, time)
- 验收标准（什么是"完成"？）/ Acceptance criteria (What is "done"?)
- 测量方式（怎么知道达成了？）/ Measurement method (How to know it's achieved?)

输出：指标清单 + 验收标准 | Output: Metrics list + Acceptance criteria

#### A - Achievable（可达成 | Achievable）
引导用户评估 | Guide user to evaluate:
- 现有资源是否足够？/ Are current resources sufficient?
- 技术/时间/人力是否可行？/ Are technical/time/staff feasible?
- 是否需要分阶段达成？/ Need phased achievement?

输出：资源清单 + 可行性评估 | Output: Resource list + Feasibility assessment

#### R - Relevant（相关性 | Relevant）
帮助用户确认 | Help user confirm:
- 这个目标对齐上级目标吗？/ Does this goal align with higher-level objectives?
- 对团队/公司有价值吗？/ Is it valuable to the team/company?
- 现在做这个合适吗？/ Is now the right time?

输出：对齐说明（1段话）| Output: Alignment explanation (1 paragraph)

#### T - Time-bound（时限性 | Time-bound）
协助设定 | Help set:
- 最终截止日期 / Final deadline
- 里程碑节点（milestones）/ Milestone nodes
- 检查点（checkpoints）/ Checkpoints

输出：时间表（甘特图或任务清单）| Output: Timeline (Gantt chart or task list)

#### SMART目标输出模板 | SMART Goal Output Template
```markdown
## SMART目标：[目标名称] | SMART Goal: [Goal Name]

**Specific（具体）**:
- 目标：... | Goal: ...
- 范围：... | Scope: ...

**Measurable（可衡量）**:
- 指标1：...（目标值 vs 当前值）| Metric 1: ... (Target vs Current)
- 指标2：...
- 验收标准：... | Acceptance criteria: ...

**Achievable（可达成）**:
- 可用资源：... | Available resources: ...
- 风险评估：... | Risk assessment: ...

**Relevant（相关性）**:
- 对齐目标：... | Aligned goal: ...
- 价值说明：... | Value description: ...

**Time-bound（时限性）**:
- 截止日期：YYYY-MM-DD | Deadline: YYYY-MM-DD
- 里程碑：... | Milestones: ...
```

---

## 框架3：SWOT（战略分析）| Framework 3: SWOT (Strategic Analysis)

### 适用场景 | Applicable Scenarios
- 竞品分析 / Competitor analysis
- 战略规划 / Strategic planning
- 项目启动前的环境分析 / Environment analysis before project launch

### 执行流程 | Execution Flow

#### S - Strengths（优势 | Strengths）
引导用户列出 | Guide user to list:
- 内部优势（技术、资源、团队、品牌...）/ Internal strengths (tech, resources, team, brand...)
- 与竞品对比的优势 / Advantages vs competitors

输出：优势清单（带优先级）| Output: Strengths list (with priority)

#### W - Weaknesses（劣势 | Weaknesses）
引导用户列出 | Guide user to list:
- 内部劣势（短板、缺陷、资源不足...）/ Internal weaknesses (shortcomings, defects, insufficient resources...)
- 与竞品对比的劣势 / Disadvantages vs competitors

输出：劣势清单（带优先级）| Output: Weaknesses list (with priority)

#### O - Opportunities（机会 | Opportunities）
引导用户列出 | Guide user to list:
- 外部机会（市场趋势、政策支持、技术突破...）/ External opportunities (market trends, policy support, tech breakthroughs...)
- 可以利用的时机 / Timings that can be leveraged

输出：机会清单（带优先级）| Output: Opportunities list (with priority)

#### T - Threats（威胁 | Threats）
引导用户列出 | Guide user to list:
- 外部威胁（竞争对手、政策风险、市场变化...）/ External threats (competitors, policy risks, market changes...)
- 需要防范的风险 / Risks to guard against

输出：威胁清单（带优先级）| Output: Threats list (with priority)

#### SWOT分析输出模板 | SWOT Analysis Output Template
```markdown
## SWOT分析：[分析对象] | SWOT Analysis: [Analysis Subject]

### 内部因素 | Internal Factors
| Strengths（优势） | Weaknesses（劣势） |
|------------------|---------------------|
| 1. ...           | 1. ...             |
| 2. ...           | 2. ...             |

### 外部因素 | External Factors
| Opportunities（机会） | Threats（威胁） |
|---------------------|----------------|
| 1. ...             | 1. ...        |
| 2. ...             | 2. ...        |

### 战略建议 | Strategic Recommendations
- **SO战略**（优势+机会）：... | **SO Strategy** (Strengths+Opportunities): ...
- **WO战略**（劣势+机会）：... | **WO Strategy** (Weaknesses+Opportunities): ...
- **ST战略**（优势+威胁）：... | **ST Strategy** (Strengths+Threats): ...
- **WT战略**（劣势+威胁）：... | **WT Strategy** (Weaknesses+Threats): ...
```

---

## 框架4：5W2H（问题拆解）| Framework 4: 5W2H (Problem Breakdown)

### 适用场景 | Applicable Scenarios
- 问题根因分析 / Problem root cause analysis
- 任务信息收集 / Task information gathering
- 需求澄清 / Requirements clarification

### 执行流程 | Execution Flow

#### W1 - What（是什么？| What is it?）
明确 | Clarify:
- 问题/任务是什么？/ What is the problem/task?
- 核心内容是什么？/ What is the core content?

输出：问题/任务描述（具体、无歧义）| Output: Problem/task description (specific, unambiguous)

#### W2 - Why（为什么？| Why?）
明确 | Clarify:
- 为什么要做这个？/ Why do this?
- 不做会有什么后果？/ What are the consequences of not doing it?

输出：目的说明 + 价值论证 | Output: Purpose statement + Value justification

#### W3 - Who（谁？| Who?）
明确 | Clarify:
- 谁负责？（Owner）/ Who is responsible? (Owner)
- 谁参与？（Stakeholders）/ Who participates? (Stakeholders)
- 谁受影响？（Beneficiaries）/ Who is affected? (Beneficiaries)

输出：角色清单 + 职责分配（RACI矩阵）| Output: Role list + Responsibility assignment (RACI matrix)

#### W4 - When（什么时候？| When?）
明确 | Clarify:
- 什么时候开始？/ When to start?
- 什么时候完成？/ When to finish?
- 关键节点是什么？/ What are the key milestones?

输出：时间表 + 里程碑 | Output: Timeline + Milestones

#### W5 - Where（在哪里？| Where?）
明确 | Clarify:
- 物理位置？（办公室、远程、多地）/ Physical location? (Office, remote, multi-location)
- 系统位置？（哪个平台、哪个模块）/ System location? (Which platform, which module)

输出：位置说明 | Output: Location description

#### H1 - How（怎么做？| How?）
明确 | Clarify:
- 技术方案是什么？/ What is the technical solution?
- 执行步骤是什么？/ What are the execution steps?

输出：执行方案（步骤清单）| Output: Execution plan (step list)

#### H2 - How much（多少成本？| How much cost?）
明确 | Clarify:
- 预算多少？/ What is the budget?
- 人力多少？/ How much staff?
- 时间多少？/ How much time?

输出：资源需求清单 + 成本估算 | Output: Resource requirements list + Cost estimation

#### 5W2H输出模板 | 5W2H Output Template
```markdown
## 5W2H分析：[问题/任务] | 5W2H Analysis: [Problem/Task]

**What（是什么）**:...

**Why（为什么）**:...

**Who（谁）**:
- Owner:...
- 参与者 | Participants:...
- 受影响者 | Affected:...

**When（什么时候）**:
- 开始 | Start:...
- 完成 | Finish:...
- 关键节点 | Key nodes:...

**Where（在哪里）**:...

**How（怎么做）**:
1. 步骤1 | Step 1:...
2. 步骤2 | Step 2:...

**How much（多少成本）**:
- 预算 | Budget:...
- 人力 | Staff:...
- 时间 | Time:...
```

---

## 组合框架示例 | Combined Framework Examples

### PDCA + SWOT（战略执行 | Strategic Execution）
1. **SWOT阶段 | SWOT Phase**: 先做SWOT分析，明确战略方向 | First do SWOT analysis, clarify strategic direction
2. **P阶段 | P Phase**: 基于SWOT结论，制定执行计划 | Based on SWOT conclusions, formulate execution plan
3. **D/C/A阶段 | D/C/A Phase**: 按PDCA循环执行 | Execute according to PDCA cycle

### SMART + 5W2H（目标拆解 | Goal Breakdown）
1. **SMART阶段 | SMART Phase**: 设定清晰的目标 | Set clear goals
2. **5W2H阶段 | 5W2H Phase**: 拆解目标为可执行的具体任务 | Break down goals into executable specific tasks

---

## 进化接口（预留）| Evolution Interface (Reserved)

### 如何添加新框架？| How to Add a New Framework?
当用户说"把XX框架加入选择器"时 | When user says "Add XX framework to selector":

1. 在本文档的"框架选择矩阵"表格中，新增一行 | Add a new row in the "Framework Selection Matrix" table
2. 新增"框架X：XXX（执行流程）"章节 | Add new "Framework X: XXX (Execution Flow)" section
3. 按照现有框架的结构，编写 | Following existing framework structure, write:
   - 适用场景 | Applicable scenarios
   - 执行流程（分步骤）| Execution flow (step by step)
   - 输出模板 | Output template
4. 更新本文档头部的 `version` 和 `updated` 字段 | Update `version` and `updated` fields in document header
5. 在 `_meta.json` 的 `changelog` 中记录本次更新 | Record this update in `_meta.json`'s `changelog`

### 如何修改现有框架？| How to Modify Existing Frameworks?
当用户反馈"PDCA的Check阶段不够用"时 | When user feedback "PDCA Check phase is not enough":

1. 修改对应框架的"执行流程"章节 | Modify the "Execution Flow" section of the corresponding framework
2. 保持向后兼容（不要删除字段，可以新增）| Maintain backward compatibility (don't delete fields, can add new ones)
3. 更新 `version`（如 1.0.0 → 1.1.0）| Update `version` (e.g. 1.0.0 → 1.1.0)
4. 记录到 `_meta.json` 的 `changelog` | Record in `_meta.json`'s `changelog`

### 如何删除框架？| How to Delete a Framework?
不推荐删除，建议 | Deletion not recommended, suggest:
1. 标记为"已弃用"（在框架标题后加 `~~已弃用~~`）| Mark as "deprecated" (add `~~deprecated~~` after framework title)
2. 保留内容（方便老用户参考）| Keep content (for old users' reference)
3. 在新任务中，不再推荐已弃用的框架 | In new tasks, no longer recommend deprecated frameworks

---

## 注意事项 | Notes

1. **按需加载 | Load on Demand**: 只在用户明确提到管理/规划/分析时加载此Skill，不要在每个任务中都加载 | Only load this skill when user explicitly mentions management/planning/analysis, don't load in every task
2. **用户确认 | User Confirmation**: 推荐框架后，必须等待用户确认，再执行详细流程 | After recommending framework, must wait for user confirmation before executing detailed flow
3. **灵活组合 | Flexible Combination**: 复杂任务可以组合多个框架，不要死板地只用一种 | Complex tasks can combine multiple frameworks, don't rigidly use only one
4. **持续进化 | Continuous Evolution**: 每次对话结束后，检查是否学到了新框架，主动询问用户是否要加入Skill | After each conversation, check if new frameworks were learned, proactively ask user if they want to add to Skill

---

**最后更新 | Last Updated**: 2026-05-14  
**版本 | Version**: 1.0.0  
**下次进化方向 | Next Evolution Direction**: 加入六顶思考帽、鱼骨图、OKR等框架（等待用户提供的学习资料）| Add Six Thinking Hats, Fishbone Diagram, OKR frameworks (waiting for user-provided learning materials)
