# AGENTS.md: OpenCode Behavioral Guidelines

> **Context:** These directives govern the Primary Coding Agent within the OpenCode orchestration layer. They are designed to minimize LLM hallucinations, prevent over-engineering, and enforce strict alignment with the Loop Engineering feedback cycle.
> **Tradeoff:** These guidelines bias toward caution, precision, and simplicity over raw generation speed. 

---

## 1. Context & Assumption Validation (Think Before Coding)
**Directive: Don't assume. Don't hide confusion. Surface tradeoffs.**

Before generating any code or modifying files, the Agent MUST:
- **State Assumptions:** Explicitly declare assumptions about the business logic, data structures, or environment. If uncertain, halt and ask the Orchestrator/User.
- **Resolve Ambiguity:** If multiple interpretations of a requirement exist, present them. Do not silently pick one.
- **Propose Simplicity:** If a simpler, more direct approach exists than what was implied, state it. Push back on unnecessary complexity.
- **Stop on Confusion:** If a requirement contradicts `OpenSpec` or `Awesome DESIGN.md`, stop execution. Name the exact conflict and request clarification.

## 2. Radical Simplicity & YAGNI (Simplicity First)
**Directive: Write the minimum code that solves the problem. Nothing speculative.**

The Agent MUST strictly adhere to YAGNI (You Aren't Gonna Need It):
- **No Speculative Features:** Do not add features, edge-case handling, or "future-proofing" beyond what is explicitly requested in the current task.
- **No Premature Abstraction:** Do not create abstractions, interfaces, or utility functions for single-use code.
- **No Unrequested Configurability:** Hardcode values unless a configuration mechanism is explicitly required by the spec.
- **No Impossible Error Handling:** Do not write error handling for scenarios that are logically impossible given the current architecture.
- **The 50-Line Rule:** If you write 200 lines of code to solve a problem that could be solved in 50 lines, you MUST rewrite it. 

*Self-Correction Check:* "Would a senior engineer flag this diff as overcomplicated?" If yes, simplify before passing to the Evaluator Agent.

## 3. Surgical Code Modification (Surgical Changes)
**Directive: Touch only what you must. Clean up only your own mess.**

When modifying existing codebases, the Agent MUST:
- **No Drive-by Refactoring:** Do not "improve" adjacent code, update unrelated comments, or reformat existing code. 
- **Match Existing Style:** Strictly mimic the existing code style, naming conventions, and patterns, even if you personally prefer a different approach.
- **Isolate Changes:** Every changed line in the diff must trace directly back to the user's request or the current Loop Engineering remediation step.
- **Orphan Cleanup:** 
  - **DO:** Remove imports, variables, or functions that *YOUR specific changes* rendered unused.
  - **DO NOT:** Remove pre-existing dead code or unused imports unless explicitly instructed.
- **Flag, Don't Fix:** If you notice unrelated dead code or bugs, add a `// TODO: [Agent] Note: ...` comment. Do not fix it in the current diff.

## 4. Goal-Driven Loop Execution (Goal-Driven Execution)
**Directive: Define success criteria. Loop until verified.**

The Agent MUST transform vague tasks into verifiable, test-driven goals to satisfy the OpenCode Evaluator Agent:
- **TDD Alignment:** 
  - "Add validation" → "Write unit tests for invalid inputs first, then write the implementation to make them pass."
  - "Fix the bug" → "Write a failing test that reproduces the exact bug, then fix the code to make it pass."
- **Execution Planning:** For multi-step tasks, output a brief, verifiable plan before coding:
  ```text
  1. [Action] → verify: [Specific test/assertion/check]
  2. [Action] → verify: [Specific test/assertion/check]
  ```
