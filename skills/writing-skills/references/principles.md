# Skill Writing and Structure Principles

本文件是所有写作与结构规则的唯一权威位置。review_gates.md 只提检查问句，规则本体在此。

## 1. 可预测性总纲

skill 的意义是从随机系统中拧出可预测性，但两类工作的抓手不同。机械性工作求**过程确定**：能抽取的确定性子任务（格式校验、字段扫描、路径检查、批量替换）尽量脚本化，不是什么都让模型生成。判断性工作求**结果可证伪**：不变量是成功条件，不是路径——对有能力的模型规定判断类路径，只会把"做对"降维成"走完形状"。

## 2. 表达方式分层

分界线是可检验性，不是 skill 的层级：机械可判的写死——下沉脚本、schema、受控值表，细度不设上限；判断性的给可证伪目标 + 规格，方法让路。编号步骤只在顺序本身是约束（先确认后动手、先 dry-run 后 write）或实际观察到抢跑时保留。
规格是判别器，不是生成器：细到独立裁判凭规格+产物能裁决对错，粗到不能机械照抄出产物——能照抄即已滑回 SOP；判断类判据不得逐项穷举成伪机械条款。
内容归属：无条件成立的裁决规则进 foundation 常驻；有外部结构信号触发的活动做 model-invoked skill；触发判断本身会被腐蚀的行为，挂既有结构信号或做 user-invoked；只在写 skill 时用的教义进本 references。

## 3. 命名哲学

skill 名用哲学级活动名（英文 kebab-case 动名词），名字本身即 leading word（领头词，调动模型预训练先验），不绑具体业务对象。

## 4. Invocation 二分

model-invoked：保留 description，agent 可自主触发，代价是 description 常驻上下文（context load，上下文占用）。user-invoked：`disable-model-invocation: true`，只能人手动触发，代价是人要记住它（cognitive load，记忆负担）。只有 agent 必须自主触发才选 model-invoked。双 harness 成对同步：`disable-model-invocation` ↔ openai.yaml 的 `policy.allow_implicit_invocation: false`。

## 5. description 写法

model-invoked 的 description 承担触发职责：领头词前置、一个使用场景配一个触发词、同义改写即冗余；同时写明排除场景。

## 6. Leading words

用模型预训练里已有的紧凑概念（如 grilling、tracer bullet）锚定一片行为，替代长句复述。太弱、压不过默认行为的词（如“认真”）等于没写，换更强的词。

## 7. 完成判据

每个工作单元以判据收尾。判据必须可检查（能分辨 done/not-done）、可穷尽（“每条都核对”而非“给个清单”），且可证伪——敷衍与诚实的产出必须不同形：确认式判据（“确认无误 ✓”）不合格；合格形态是缺陷式——列出发现的偏差及证据，未发现的交出自带查证链的 null 报告（查了哪里、拿什么实际值对过哪条不变量），可被抽查。根规则：伪造合格产出的成本 ≥ 诚实完成的成本，且伪造可被廉价抽查戳穿。模糊判据招致 premature completion（抢跑，提前收工）。

## 8. Negation 反噬

禁止式表述把被禁行为带进上下文，反而更易触发。优先正向陈述目标行为；只有无法正向表述的硬红线才用禁止，且必须同时给出替代动作。

## 9. 分层与 progressive disclosure

progressive disclosure（渐进披露）：SKILL.md 入口只放职责、流程、边界、必读引用、输出约定；稳定、可复用、较长的内容下沉 references/，一个 reference 只承载一个职责。分支测试——所有分支都需要的内联，只有部分分支到达的下沉。

## 10. 脚本双向边界

脚本不越界：只做结构、格式、路径、显式字段等机械检查，输出 risk_flags / issues / evidence 类结果，不对职责、语言质量、事实正确性下最终 verdict；语义结论由模型/人基于 evidence 给出（硬门槛）。模型不包揽：见第 1 条脚本化原则。

## 11. 精简版基础规则

- front matter 必须有唯一 kebab-case `name` 与含触发+排除场景的 `description`。
- 正文中文；规则一条一个动作、可执行可检查；不为覆盖自然语言变体写穷举列表。
- 结构模式速查：
  - 单体工具型：SKILL.md + references/ + scripts/，说明工具目的、输入输出、运行边界。
  - 固定 workflow controller：顶层只管阶段顺序、转交边界、停止条件，细则在阶段子 skill。
  - route controller：顶层路由表 + 默认行为，细则在 route 子 skill。
  - audit/update 型：先限定范围，默认 dry-run，只改目标块，输出可审阅变更。

## 12. 输入与产物的必要性

判据是必要性而非数量：质量所需的读取、查证、验证与必要中间产物，不因省 token 而省；对任务无贡献的读取与产物即浪费。
- skill 要求的输入先定位再读、只读所需片段；大范围探索交 sub-agent 隔离承担，主上下文回收结论与指针，不回收原始材料。
- 每个产物——含中间产物——须说得出用途与服务对象，保持完成任务所需的最简形态；必须落盘的说明数量、路径、用途；说不出用途的不设。
