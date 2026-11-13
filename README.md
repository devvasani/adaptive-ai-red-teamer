# Adaptive AI Red Teamer

A feedback-driven framework for automated red teaming of language models, exploring how adversarial strategies can be iteratively refined using target responses and evaluation feedback.

**Status:** V1 implemented | V2 under development

## Overview

V1 implements an adaptive attacker–target–auditor architecture for evaluating hidden-instruction leakage in a sandbox LLM.

- **Attacker:** Generates adversarial prompts and refines its strategy based on previous attempts.
- **Target:** A configurable chatbot with hidden system instructions.
- **Auditor:** Evaluates target responses for instruction leakage and provides feedback to the attacker.

The system runs a multi-round evaluation loop, using previous outcomes to guide subsequent attacks rather than relying on a fixed set of prompts.

A Streamlit interface provides visibility into attack attempts, target responses, and evaluation results.

# Adaptive AI Red Teamer

An experimental framework for adaptive security evaluation of language models, exploring how an LLM-based attacker can iteratively refine adversarial prompts using feedback from a target model and an independent evaluator.

The project investigates automated red teaming as a feedback-driven process rather than a collection of static, predefined attacks.

**Status:** V1 implemented · V2 under development

## Overview

Traditional prompt-based security testing often evaluates a model against a fixed set of adversarial inputs. This project explores an alternative approach in which an attacker model generates new attempts based on the outcomes of previous interactions.

The initial implementation focuses on a specific security objective: **testing whether a sandbox chatbot can be induced to reveal its hidden instructions**.

The system consists of three components:

- **Attacker:** Generates adversarial prompts and adapts its strategies using previous attempts and evaluator feedback.
- **Target:** A configurable sandbox chatbot with visible role instructions and hidden system instructions.
- **Auditor:** Evaluates the target's responses for instruction leakage, assigns scores, and provides feedback for subsequent attempts.

Each round follows the same process:

1. The attacker generates an adversarial prompt based on its current strategy and previous feedback.
2. The target chatbot responds to the generated prompt.
3. The auditor evaluates the response for hidden-instruction leakage.
4. The evaluation result and feedback are added to the attack history.
5. The attacker uses this information to guide its next attempt.

The loop continues for a configurable number of rounds, or stops early when the auditor identifies a full instruction leak.

### Architecture

```text
            ┌───────────────────┐
            │    LLM Attacker   │
            └─────────┬─────────┘
                      │ Attack prompt
                      ▼
            ┌───────────────────┐
            │  Sandbox Target   │
            └─────────┬─────────┘
                      │ Target response
                      ▼
            ┌───────────────────┐
            │    LLM Auditor    │
            └─────────┬─────────┘
                      │ Evaluation + feedback
                      ▼
            ┌───────────────────┐
            │  Attack History   │
            └─────────┬─────────┘
                      │
                      └──────► Next attack round
```

## Current Development

V2 is extending the framework toward **tool-using AI agents**, investigating security risks involving tool access, permissions, and multi-step agent workflows.

V2 is currently under development and is not included in this repository.
