# SpecKit

**SpecKit** is a lightweight, opinionated, and AI-driven application development boilerplate. It provides out-of-the-box (OOTB) support for both Greenfield (new) and Brownfield (existing) projects. **What's included?**

- **[OpenCode](https://github.com/anomalyco/opencode)** - Model-agnostic agent orchestration.
- **[OpenSpec](https://github.com/Fission-AI/openspec)** - A spec-driven development framework with an opinionated workflow.
- **[Skills](https://github.com/mattpocock/skills)**
  - Real-world productivity skills powered by `mattpocock/skills` for `OpenSpec`.



### 1. Installation

#### 1.1 Instruct OpenCode to fetch and follow the setup instructions:

```text
Fetch and follow instructions from https://raw.githubusercontent.com/jimzhan/speckit/refs/heads/main/INSTALL.md
```

#### 1.2 Ensure at least one model provider is activated for `OpenCode`.

> 💡 **Tip:** It is recommended to start your test run with the free model provided by `OpenCode` (enabled by default if environment variable  `OPENCODE_API_KEY` is configured).





### 2. Workflow

```mermaid
---
config:
  look: handDrawn
  theme: forest
---
flowchart LR
    New["<b>/opsx:new</b> your-requirement<br/>(Start a new change)"]
    Grill["<b>grill-with-docs</b> skill used<br/>(Interview for <b><i>proposal.md</i></b>)"]
    Propose{"<b><i>proposal.md</i></b> LGTM?"}
    Review{"<b><i>design.md</i></b> & <b><i>tasks.md</i></b> LGTM?"}
    FF["<b>/opsx:ff</b><br/>(Write <b><i>design.md</i></b> & <b><i>tasks.md</i></b>)"]
    Continue["Review <b><i>proposal.md</i></b> then <b>/opsx:continue</b>"]
    Apply["<b>/opsx:apply</b><br/>(Implement tasks from the change)"]
    Archive["<b>/opsx:archive</b><br/>(Archive a completed change)"]

    New --> Grill
    Grill --> Propose
    Propose --> |Yes| FF
    Propose --> |No| Continue
    FF --> Review
    Continue --> Review
    Review --> Apply
    Apply --> Archive
```

#### 2.1 Use

- `/opsx-explore` - to think through ideas before committing to a change (`/opsx-new` comes next).
- `/opsx-verify` - to validate implementation matches artifacts.
- `/opsx-update` - to revise a change's planning artifacts and keep them coherent.
- `/opsx-sync` - to merge delta specs into main specs:
  - `openspec/<change-id>/**/spec.md` => `openspec/specs/<domain>/spec.md`





### Recommended Setup

- [`rtk`](https://github.com/rtk-ai/rtk) - High-performance CLI proxy that reduces LLM token consumption by 60-90% (`rtk init -g --opencode `).
