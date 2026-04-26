# From Reasoning to Agentic Models

This is Wukong's summary.

**Source:** [Justin Lin (Junyang Lin) - X Post](https://x.com/justinlin610/status/2037116325210829168)

**Date:** 2026-04-26

**Author:** Junyang Lin (Justin Lin) - Qwen/Alibaba

---

## Key Thesis

The next wave is shifting from "reasoning thinking" (thinking longer) to "agentic thinking" (thinking in order to act).

---

## Main Points

### 1. What o1/R1 Taught Us
- Reasoning needs deterministic feedback (math, code, logic)
- It became an infrastructure story as much as modeling
- You need rollouts at scale, high-throughput verifiers, stable policy updates

### 2. The Merging Challenge
- Qwen3 tried "hybrid thinking modes" but found the data distributions for thinking vs instruct models are substantially different
- Without careful curation, you get mediocre results in both directions
- Some customers still just want high-throughput instruct behavior for batch ops

### 3. Anthropic's Useful Corrective
- Rather than just "more thinking," they shaped reasoning by target workload
- For coding, thinking should help with navigation, planning, error recovery
- Not produce verbose internal monologues

### 4. What Agentic Thinking Means
- Shift from "can it think long enough?" → "can it think in a way that sustains effective action?"
- Deciding when to stop thinking and act
- Choosing tools, incorporating environmental feedback
- Revising plans after failures
- Maintaining coherence across many turns

### 5. Why Infrastructure is Harder
- Environment is no longer a static verifier
- It's tool servers, browsers, simulators, execution sandboxes
- Need clean train/inference decoupling or rollout throughput collapses

### 6. The Biggest Challenge: Reward Hacking
- Once models get real tool access, they can cheat in new ways
- "The agent era is more delicate than the reasoning era"

### 7. Competitive Edge Shifts
- From better RL algorithms → to better environments, harness engineering
- And closing the loop between decisions and consequences

---

## Bottom Line

We're moving from training models to training agents, and from training agents to training systems.

The next frontier is "more usable thought" - thinking that's embedded in action rather than isolated monologue.

---

## Stats
- 653K views
- 2.7K likes
- 2.7K bookmarks

---

## Tags
#reasoning #agentic #AI #Qwen #Alibaba #LLM