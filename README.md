# Harness-Bounded Self-Improvement in Language Agents  
## Context as a Missing Optimization Variable

This repository contains the paper **"Harness-Bounded Self-Improvement in Language Agents: Context as a Missing Optimization Variable"**.

## Abstract

Recent work on self-improving language agents has largely focused on improving the **harness** surrounding a base model: prompts, tool-use policies, reflection loops, execution strategies, and orchestration logic. This paper argues that such a view is structurally incomplete.

We formalize a third optimization layer - the **context layer** - which captures the retrieved, remembered, accumulated, and dynamically assembled information on which agent behavior depends at inference time. We show that when context is stochastic, partially observed, and non-stationary, harness-centric self-improvement faces a fundamental limitation: it optimizes only a conditional slice of the overall agentic system while leaving a major source of error unmodeled.

The paper develops a formal framework for decomposing agent performance into **model**, **harness**, and **context** components, and derives four key results:

1. **Harness incompleteness under context variability**  
   A single globally optimized harness is generally suboptimal relative to a context-aware policy when different contexts require different harness behavior.

2. **Bias in harness self-improvement under context-corrupted feedback**  
   If feedback used for self-improvement is generated under latent context corruption or harness-dependent context shifts, the harness update objective becomes biased.

3. **Non-stationarity of the optimal harness under context drift**  
   As retrieval distributions, memory state, and other context processes evolve over time, the optimal harness itself becomes non-stationary.

4. **A residual harness boundedness gap**  
   Even if harness-only self-improvement converges perfectly, it can still converge to the wrong optimum: the best harness conditioned on a fixed context process rather than the best overall agent system.

## Core Thesis

Most current recursive self-improvement systems optimize the wrong variable, or at least an incomplete set of variables.

They improve the **harness**:
- prompts
- decomposition strategies
- reflection loops
- tool routing
- orchestration logic

But they often treat **context** as fixed, implicit, or exogenous.

This paper argues that in open-world agent systems, that assumption breaks.  
Failures are not only caused by weak prompts or poor orchestration. They are also caused by unreliable context:
- missing evidence
- stale memory
- irrelevant retrievals
- conflicting tool outputs
- incomplete histories
- poorly assembled execution state

In that setting, harness-only recursive self-improvement is structurally bounded in the reliability it can achieve.

## Main Formal Objects

The paper models an agent as a **model-harness-context system**:

- **Model layer** `θ`  
  The underlying model parameters.

- **Harness layer** `h`  
  Prompts, tool-use policies, decomposition strategies, reflection logic, routing, and orchestration.

- **Context layer** `π`  
  Retrieval, memory selection, tool outputs, conversation history, and dynamically assembled information supplied to the agent at inference time.

The expected system risk is written as:

\[
R(\theta,h,\pi)=\mathbb{E}_{x}\left[\mathbb{E}_{c\sim \pi(\cdot|x)}[L(\theta,h,c,x)]\right]
\]

where:
- `x` is the input
- `c` is the context supplied to the agent
- `h` is the harness configuration
- `π(c|x)` is the context-generation policy

## Key Concept: Harness-Bounded Self-Improvement

The paper defines **harness-bounded self-improvement** as any self-improvement process that can update the harness `h` but not the context policy `π`.

That includes many modern self-improving agent patterns such as:
- prompt optimization
- reflection-based prompt revision
- tool-routing refinement
- execution scaffold improvement
- orchestration-level self-improvement loops

The core claim of the paper is that **harness-bounded self-improvement is structurally incomplete** whenever context is a major source of uncertainty and failure.

## Repository Contents

- `paper.pdf` – final compiled paper
- `main.tex` – LaTeX source
- `neurips_2023.sty` – NeurIPS style file used for formatting
- `README.md` – repository overview

## Why this matters

There is growing excitement around self-improving agents and recursive self-improvement as a path toward increasingly autonomous systems. But improving the harness is not the same as improving the full system.

This paper shows that if context remains stochastic, drifting, and partially unreliable, then self-improvement at the harness layer alone cannot fully close the reliability gap.

In other words:

> A system can get better at reasoning over a context without getting better at receiving the right context.

That distinction matters for how we think about:
- recursive self-improvement
- agent reliability
- evaluation-driven optimization
- retrieval and memory systems
- open-world deployment of language agents

## Citation

If you want to reference this work, please cite the repository or the paper directly once a canonical paper link is available.

## Author

**Debraj Bandyopadhyay**  
Litmus AI

**Sanjay Srivastava**  
Litmus AI
