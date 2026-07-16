# Cokit: AI-Driven Project Scaffolding Guide

> **AI Execution Directive**: Follow these instructions strictly when a user asks you to scaffold or integrate a new project with `OpenCode` and `OpenSpec`. Your primary mandate is **non-destructive integration**: never delete, overwrite, or alter existing product code, tests, or package files without explicit, confirmed user consent.

## 1. Prerequisites
Before proceeding, verify or instruct the user to ensure the following are installed on their local machine:
- **Git**: `v2.30+` (Required for cloning and version control checks).
- **Node.js**: `v22+` LTS (Required for cross-platform, non-destructive merge logic and script execution).
- **OpenCode CLI**: Latest version (Installed globally or via project package manager).
- **OpenSpec**: Latest version (Install globally via `npm`).

## 2. Goal
Intelligently inject the Cokit spec-driven governance layer (`OpenSpec` + `OpenCode` configurations) into the user's current working directory while preserving 100% of their existing project conventions, code, and documentation.

## 3. Source Template Acquisition
Clone a fresh, isolated copy of the template repository into the system's temporary directory (e.g., `/tmp` on macOS/Linux or `%TEMP%` on Windows) to prevent any accidental pollution of the user's workspace.

```bash
# Execute in system temp directory
git clone --depth 1 https://github.com/jimzhan/cokit.git cokit 
```

## 4. Target Directory Review (AI Checklist)
Before copying any files, inspect the user's current working directory (`process.cwd()`). Check for the existence of:
- [ ] `README.md`
- [ ] `AGENTS.md`
- [ ] `opencode.json`
- [ ] `skills-lock.json`
- [ ] `openspec/` directory
- [ ] `.opencode/` directory
- [ ] `.agents/` directory

**Rule**: Identify any existing OpenSpec, OpenCode, agent, or skill settings. You must preserve user-specific instructions and project conventions.

## 5. Files To Install & Merge Strategy

### A. Copy (Only if they do NOT exist)
Safely copy the following template files and directories into the target project root:
- `openspec/`
- `.opencode/`
- `.agents/`
- `skills-lock.json`
- `opencode.json`

### B. Merge (If they already exist)
- **`AGENTS.md`**: **Append** the OpenSpec git-discipline instruction block to the end of the file. **Do not** remove, truncate, or alter any existing user instructions.
- **`README.md`**: Do **not** modify unless the user explicitly requests project documentation updates.

## 6. Step-by-Step Installation Execution

1. **Acquire**: Clone or locate the source template repository in a temporary, isolated directory.
2. **Inspect**: Scan the target project for existing configuration and documentation files (refer to Section 4).
3. **Copy**: Transfer missing template directories and files from the temp directory to the target project.
4. **Merge**: Safely append the OpenSpec git-discipline block to `AGENTS.md` if it exists.
5. **Conflict Resolution**: If `opencode.json`, `skills-lock.json`, `openspec/`, `.opencode/`, or `.agents/` already exist, **pause execution**. Compare the template version/structure with the target version. Present the differences to the user and **ask for explicit approval** before replacing, merging, or restructuring anything.
6. **Preservation Guarantee**: Ensure the target project's product code (`src/`, `lib/`, etc.), package files (`package.json`, `requirements.txt`), application docs, and existing tests remain 100% unchanged.
7. **Summarize**: Verify the resulting file tree and output a clear, bulleted summary of exactly what was added or modified.

## 7. Post-Installation Validation

After installation, run the safest, read-only checks available for the target project to ensure no breakage occurred:

```bash
# 1. Verify only intended files were touched
git status --short

# 2. Validate OpenSpec schema (if the CLI is available in the environment)
openspec schema validate spec-driven

# 3. (Optional) Verify OpenCode providers
opencode providers list
```

**Fallback Rule**: If `openspec` or `opencode` commands are unavailable in the user's environment, clearly report this limitation to the user, but leave the installed files in place so the user can verify them manually later.

## 8. Cleanup (OPTIONAL)
Once the user confirms the installation is successful, delete the temporary cloned repository (`cokit`) to maintain a clean environment.
