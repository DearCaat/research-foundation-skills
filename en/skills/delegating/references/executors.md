# Choosing an executor

A piece of work can go to four kinds of executor: a script, a decision model, a direct LLM API call, or a harness. For the entry points available in the runtime environment, and their prices and rate limits, consult that environment’s calling documentation.

## Script

Whether to use one follows §4 of the standing principles. To derive here means to explain why the rule meets the task definition for every input in scope, given its premises; a short, checkable rationale normally suffices, and “it was right on the samples seen” is not one. When the task is defined as counting distinct patient IDs, deduplicating on that field holds for IDs never seen before; a code that is in the code table is classified by the table even on its first appearance, and a code outside the table is reported as unknown as agreed. What cannot be derived is not decided by a script: when reading free text, a keyword or regular-expression match can serve as evidence; where the conclusion still depends on context, a model judges from the material; where the decision criterion itself is not yet settled, follow §3 of the standing principles.

Once the derivation holds, still verify that the implementation follows the rule, and check the critical premises of the current input. For a premise whose failure would still yield a result that looks valid, check it whenever the input allows; when the check fails, identify the affected records or tasks and do not adopt the corresponding results. For a critical premise that the input cannot settle, such as what a field means, consult the source or specification first; mark it unresolved if it still cannot be confirmed.

## Decision model

Judges among fixed options and returns only a label, a score, or a probability; it generates no text.

- Each item is usually faster and cheaper than a generative call, which suits large batches of classification, first-pass screening, and reference signals.
- It gives no reasons, so a single wrong judgment cannot be diagnosed from the output, and accuracy varies by task. Validate a new use on representative labeled samples first; support a critical judgment with other evidence.
- Set the threshold by the task’s goal and revalidate after changing the model; when downstream work will read the output as a probability, also check its calibration.

## Direct LLM API call

Suited to work whose material can be assembled in advance and that needs one judgment or one generation; the conclusion can carry reasons a person can review.

- There is no harness system prompt or tool loop, so the input is the task itself: low overhead and more controllable behavior.
- The caller assembles the material and sets the parameters that matter to the task. A successful call does not mean a usable result: the response may carry an empty answer, one truncated by a limit, a requested parameter that did not take effect, or a model different from the requested one, and still look like a normal result. So check every final answer for completeness and usability, and check the finish reason, model identifier, and usage that the response exposes against the interface documentation; mark any requested configuration that the response cannot confirm as unverified. Set empty and truncated results aside, and merge them into the result set only after they are handled.
- When the interface supports prefix caching, put fixed content (instructions, criteria, shared material) before per-item content; check cache hits against the statistics the interface reports.

## Harness

The model gathers its own material, calls tools, and works over multiple turns; suited to work that must keep gathering material or acting on intermediate results. A sub-agent is this kind of executor inside the current harness.

- Choose by the abilities the task will use: tools, isolation, session reuse, context compaction. Every tool-call turn and every compaction adds latency and a chance of failure; when the material is ready, one judgment or generation suffices, and the task has no host-specific requirement such as isolation, prefer a direct call.
- Once you have decided on a harness, prefer the current host’s native sub-agent when it meets the required model, effort, workspace, permissions, and isolation, which saves a layer of cross-host parameter passing. Use an external harness only when those requirements cannot be met, the user named another combination, or the work must run in parallel outside the host.

## Reading images

Before reading images through a new model or calling path, run a trial with an image whose answer you know and that tests the detail the task needs. This applies to direct calls and harnesses alike: some paths convert an image to text or shrink it, and the model still answers without an error.

## Comparing two paths

Total token count is not cost: cache reads, uncached input, and output differ in unit price and latency. To compare two available paths, use the same set of representative tasks and the same quality standard; record uncached input, cache reads and writes, output, total latency, and invalid results for each, and compare them at each path’s actual pricing. Measure latency with the dependent turns and the concurrency actually used. Savings count only when quality is comparable. When a comparable free path exists, run the trial directly (§3 of the standing principles).

## Batches

Start with a small representative batch and check answer quality, the share of empty and truncated answers, and latency; then set batch size and concurrency.
