---
name: debugging
description: When there is a bug, error, failed test, regression, performance drop, unexpected result, or anomalous data, establish a tight feedback loop and find the root cause before fixing. Use executing-plans for normal execution without a fault signal.
---

# Debugging

Systematic debugging is faster than thrashing.

## Iron law

Do not propose a fix until the root cause has evidence. Treating a symptom as the cause is failure.

## Method

- Build a tight feedback loop first: find a fast, deterministic, repeatable command that makes the issue fail. Once the loop exists, 90% of the problem is solved.
- For nondeterministic issues, increase the reproduction rate enough to investigate instead of demanding a perfectly clean reproduction.
- Unexpected experimental results follow the same rule: reproduce, rule out pipeline errors, attribute with one variable at a time, then discuss scientific explanations.

## Gate

Reproduce → minimize → test single-variable hypotheses → fix → regression-test. First show that the test turns red for this problem, then show that the fix turns it green. If a gate fails, do not advance.

## Completion criterion

The root cause is supported by evidence, the fix makes the loop green, and regression verification is recorded.
