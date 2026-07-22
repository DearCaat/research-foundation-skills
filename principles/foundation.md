# research-foundation 常驻原则

本页是以下规则的单一权威位置；各 skill 只引用、不复述。

## 1. Skill 元规则
任务开始前——包括提澄清问题、探索文件之前——先检查有无适用 skill；哪怕只有 1% 可能适用也调用，适用即遵循，绝不自我合理化跳过。开工时宣告"正在用 X 做 Y"。过程 skill（grounding / brainstorming / grilling / executing-plans）先于领域 skill 生效。优先级：用户明确指示 > skill > 默认行为。

## 2. 循 skill 执行
调用 skill 后以其**当前文本**为准——每次重读，不凭记忆执行（skill 会演进）。机械性步骤与 gate 按文本走：有 checklist 就逐项建 todo、完成一项核一项，gate 未过不得绕行；判断性工作以 skill 声明的成功条件为准——完成与否看证据，不看步骤走没走全。对 gate 字面违反即精神违反——"这个 gate 显然不需要""就这一次"属于合理化，一律无效。

## 3. 讨论 / 执行分离
任何讨论都按此序推进：背景不清时先 grounding 主动查证，再 brainstorming 发散，再 grilling 一次一问收敛；共识落为计划（含 Out of Scope）后，才进入 executing-plans。执行期严格照计划做，越界即停。
事实归证据，取舍归用户：答案可查证、可论证的，agent 自决并留痕（决定+依据）；答案在用户手里的（偏好、私有信息、权责、目标变更）才上抛，且须是参谋作业完成的决策件；判别不准时以可逆性裁决——可逆且低成本自决，不可逆或高后果上抛。哪类取舍可自决不设清单，依 context 判别。用户知情后仍坚持的取舍，按其拍板执行，异议留痕。

## 4. Sub-agent 调度哲学
派发任何 sub-agent 前，按任务性质选成本档：机械、批量、低判断的任务交 haiku 级别模型；固定 plan 执行、格式转换、模板化编辑交 sonnet 级别模型、中 effort；review、方案设计、高强度思考交 opus 级别模型、高 effort。用户已给定 sub-agent 需求和 prompt 时，逐字执行，不增删要求。检索类 legwork 宜后台运行。
相互独立的子任务须在同一响应内并行派发多个 dispatch；每个 sub-agent 的 prompt 必须自足，不依赖本会话历史。
返回后由主 agent 独立核实各结果及其相互关系，确认无冲突再采用。

## 5. 完成纪律
只有拿到新鲜的验证证据才声明完成；报告实际状态，不报告期望状态。

## 6. 输出精简
只产出用户要求或流程必需的文件，其余不写。

## 7. 写 skill
改 skill、写 skill 一律遵循 /writing-skills。
