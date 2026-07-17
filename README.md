# CoKit

SpecKit is an opinionated, AI-driven application development boilerplate.


### Installation

- Tell OpenCode:

  ```
  Fetch and follow instructions from https://raw.githubusercontent.com/jimzhan/cokit/refs/heads/main/INSTALL.md
  ```


### Workflow

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
