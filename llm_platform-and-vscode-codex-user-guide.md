# LLM Platform and VS Code Codex User Guide

> Human2AI | @NullCodeLabs | 2026  
> English edition

## 1. The system in one minute

The Human2AI system uses two separate master prompts.

- `llm-platform-master-prompt.txt` — the general, platform-level Human2AI operating layer.
- `codex-vscode-master-prompt.txt` — the development operating layer optimized for VS Code and Codex.

They are not duplicate files and they are not loaded in the same place.

The LLM platform prompt belongs in the global instruction layer of the AI service.

The Codex prompt belongs in Codex's own local instruction stack.

Canonical sources:

- https://github.com/NullCodeLabs/Human2ai-intent-codec/blob/main/llm-platform-master-prompt.txt
- https://github.com/NullCodeLabs/Human2ai-intent-codec/blob/main/codex-vscode-master-prompt.txt

This guide does not duplicate the full prompts. The canonical `.txt` file remains the source of truth.

---

## 2. What the two layers mean

### LLM Platform Master Prompt

The general LLM platform prompt controls the model's operating behavior across normal conversations:

- Contract
- Supervisor Body
- AllGAP
- Precedence / Precedent
- TCO
- OHYL / Investigator
- DIE
- canonical state
- context discipline
- zero-noise output

It is not designed for one chat or one project. Its purpose is platform-level behavior.

### Codex VS Code Master Prompt

The Codex version translates the same Human2AI operating logic into software-development work.

Primary concerns include:

- repository state
- working tree
- dependencies
- tests
- Git
- build
- migrations
- security
- minimal patching
- canonical code
- debugging
- context control

### Important

ChatGPT Custom Instructions do not automatically flow into Codex inside VS Code.

Codex builds its own instruction stack.

---

## 3. Where to use the LLM platform prompt

The goal is not to paste the prompt as the first message of every new conversation.

When a service provides an account-level or global instruction field, use that field.

Where no global field exists, use project instructions or an API system/developer message.

| Platform | Recommended location |
|---|---|
| ChatGPT | Settings → Personalization → Custom Instructions |
| Claude | Settings → Instructions for Claude |
| Gemini | Settings & help → Personal Intelligence → Instructions for Gemini |
| Perplexity | Profile / Personalization + Project Instructions |
| Kimi | Project Instructions; Kimi Code may use a separate global instruction file |
| DeepSeek | Web: chat/project level; API: system message |
| Qwen | Consumer UI varies; API / Model Studio: system message |

### Rule

Put the general OS in the global layer.

Put only project-specific delta in project instructions, unless that platform does not carry the global layer into projects.

---

## 4. ChatGPT

### Global setup

1. Open `Settings`.
2. Select `Personalization`.
3. Open `Custom Instructions`.
4. Paste the canonical `llm-platform-master-prompt.txt` content.
5. Save.
6. Verify behavior in a new chat.

### Projects

A project may provide its own instruction layer.

Project instructions should contain only project-specific information such as:

- objective
- stack
- file rules
- domain constraints
- acceptance criteria

Do not maintain a manual copy of the general OS unless the platform's instruction behavior makes that necessary.

---

## 5. Claude

Claude's account-wide `Instructions for Claude` is the appropriate place for the general platform OS.

Steps:

1. Open your profile / initials.
2. Open `Settings`.
3. Open `Instructions for Claude`.
4. Paste the `llm-platform-master-prompt.txt` content.
5. For a Project, place only the project-specific delta in `Set project instructions`.

Project knowledge is content.

Global instructions are operating rules.

Do not treat them as the same thing.

---

## 6. Gemini

### Normal Gemini

1. Open Gemini.
2. Open `Settings and help`.
3. Open `Personal Intelligence`.
4. Open `Instructions for Gemini`.
5. Select `Add`.
6. Paste the platform prompt.
7. Save.

### Gems

A Gem has its own `Instructions` field.

Gem instructions are separate from the global `Instructions for Gemini`.

---

## 7. Perplexity

Perplexity separates personal profile behavior from Project Instructions.

Recommended layout:

- general Human2AI preferences → Profile / Personalization
- specific research or development project → Project Instructions
- project files → reference material

Do not use a prompt file as both knowledge material and operating instructions when the platform provides separate mechanisms.

---

## 8. Kimi, DeepSeek, Qwen

### Kimi

A normal Kimi Project can apply Project Instructions across project chats.

Kimi Code uses a separate development instruction mechanism.

### DeepSeek

If the consumer web interface does not provide a reliable account-wide instruction field:

- use chat or project scope
- use a system message through the API

### Qwen

Consumer features may vary.

For API / Model Studio workflows, a system message is the stable model-independent pattern.

### Rule

If a platform does not provide a real global instruction layer, do not force one.

Keep the canonical prompt unchanged. Change only the loading adapter.

---

## 9. VS Code + Codex: the correct architecture

Codex does not operate from ChatGPT Custom Instructions.

It builds its own instruction stack.

That is why `codex-vscode-master-prompt.txt` is a separate Codex source.

Practical order:

```text
Native Codex system / sandbox / permissions
        ↓
config.toml developer_instructions [if used]
        ↓
$CODEX_HOME/AGENTS.override.md or AGENTS.md
        ↓
from project root to cwd: AGENTS.* or configured fallback filenames
        ↓
current user request + local environment
```

---

## 10. Windows setup: Codex master prompt

Target state:

```text
C:\Users\<WINDOWS_USER>\.codex\codex-vscode-master-prompt.txt
C:\Users\<WINDOWS_USER>\.codex\AGENTS.md
C:\Users\<WINDOWS_USER>\.codex\sync-codex-prompt.ps1
C:\Users\<WINDOWS_USER>\.codex\config.toml
```

The canonical source is the `.txt` file only.

`AGENTS.md` is a Codex-compatible mirror.

Do not edit it manually.

Steps:

1. Create `C:\Users\<WINDOWS_USER>\.codex\` if it does not already exist.
2. Put the canonical `codex-vscode-master-prompt.txt` there.
3. Create the `sync-codex-prompt.ps1` sync script.
4. Run the sync.
5. Start a new Codex session.

---

## 11. One-way TXT → AGENTS.md sync

```powershell
$src = "$env:USERPROFILE\.codex\codex-vscode-master-prompt.txt"
$dst = "$env:USERPROFILE\.codex\AGENTS.md"

Copy-Item $src $dst -Force
Write-Host "Synced: $src -> $dst"
```

Save as:

```text
C:\Users\<WINDOWS_USER>\.codex\sync-codex-prompt.ps1
```

Run manually:

```powershell
powershell -ExecutionPolicy Bypass -File "$env:USERPROFILE\.codex\sync-codex-prompt.ps1"
```

### Canonical rule

`AGENTS.md` is a generated compatibility file.

Never edit it manually.

All changes are made in `codex-vscode-master-prompt.txt`, then synchronized again.

---

## 12. config.toml: what it is and is not

`project_doc_fallback_filenames` does not automatically turn the global `.txt` file under `$CODEX_HOME` into a global instruction source.

The documented global layer is the `$CODEX_HOME` file:

- `AGENTS.md`
- `AGENTS.override.md`

Recommended minimum:

```toml
# C:\Users\<WINDOWS_USER>\.codex\config.toml

# The global Human2AI layer is loaded through the AGENTS.md mirror.
# Keep config.toml for other Codex settings only when they are actually needed.
```

For project fallback filenames:

```toml
project_doc_fallback_filenames = ["codex-vscode-master-prompt.txt"]
```

Use this only when you explicitly want Codex to recognize a repository-local `.txt` instruction file as project instructions.

---

## 13. Global prompt vs. project delta

### Global Codex prompt

Contains:

- Human2AI Contract
- Supervisor Body
- AllGAP
- Precedence
- Precedent
- TCO
- OHYL
- DIE
- repository-first behavior
- canonical code
- minimal patch
- testing
- Git discipline
- dependency discipline
- security baseline

### Project AGENTS.md

Contains:

- repository purpose
- tech stack
- build commands
- test commands
- directory structure
- conventions
- project-specific invariants
- deployment and migration rules

### Do not duplicate

A project `AGENTS.md` should not repeat the global Human2AI OS.

It should contain only the project-specific delta.

---

## 14. Daily workflow

1. Open VS Code in the correct repository.
2. Make sure the latest global TXT has been synchronized to `AGENTS.md`.
3. Start a new Codex session if the global prompt changed.
4. Describe the task as an outcome.
5. State what must not break.
6. State what counts as acceptance.
7. Do not prescribe the technical method unless it is a hard constraint.
8. Allow or request relevant tests after code changes.
9. Commit / push / deploy only within the intended scope.

Example:

```text
GOAL: login should provide feedback within 2 seconds.
MUST NOT BREAK: current Google login, Firestore schema, mobile UI.
ACCEPTANCE: existing tests + new regression test pass.
METHOD: your call; choose the shortest reliable path.
```

---

## 15. Correct prompt update workflow

The canonical filename does not change.

Do not create:

- final2
- revised
- v7-copy
- new-final
- revised-final

Track versions with Git commits, tags, or an internal header.

Steps:

1. Edit `codex-vscode-master-prompt.txt` in place.
2. Review the delta.
3. Run `sync-codex-prompt.ps1`.
4. Verify that `AGENTS.md` matches the TXT content.
5. Commit the canonical TXT update.
6. Start a new Codex session.

Quick verification:

```powershell
$a = Get-FileHash "$env:USERPROFILE\.codex\codex-vscode-master-prompt.txt"
$b = Get-FileHash "$env:USERPROFILE\.codex\AGENTS.md"
$a.Hash -eq $b.Hash
```

Expected result:

```text
True
```

---

## 16. How to test whether it is actually active

Do not ask:

```text
Did you load the prompt?
```

Test behavior.

### Shortest Path test

```text
Do not give me two technical routes.
Choose one recommended route using total cost of ownership,
maintenance burden, and reversibility.
```

### Precedent test

```text
Before adding a new module, check whether the same function
already exists in the repository, standard library, or framework.
```

### Canonical Code test

```text
Do not create a new helper file if the current canonical
implementation can be fixed directly.
```

### AllGAP test

```text
The bug appears in the frontend.
Check whether backend, auth, schema, config, or deployment boundaries
may actually be the cause.
```

---

## 17. Troubleshooting

### Codex behaves as if it cannot see the global prompt

Check whether:

- `$env:USERPROFILE\.codex\AGENTS.md` exists
- its content matches the canonical TXT
- the sync script ran successfully
- a new Codex session was started
- an `AGENTS.override.md` exists
- a more specific project `AGENTS.md` is changing behavior

### Platform prompt works in normal chats but not in a project

Check the platform's project instruction precedence rules.

If the project layer is stronger, preserve the required global invariants in the project delta.

### Output is too long or too AI-like

Do not repeat the same style rule in every chat.

Fix the global prompt.

---

## 18. Trust, security, and distribution

The canonical prompt uses `.txt` intentionally.

A user does not need to trust an executable binary, installer, macro, or unknown script merely to read or paste the prompt.

A `.txt` file is not a security shield.

The real trust boundary includes:

- files you execute
- repositories you open
- shell commands you authorize
- project instructions you inherit
- dependencies you install

The prompt file is still a good distribution format because it is:

- passive
- auditable
- diffable
- versionable
- platform-independent

### Codex-specific warning

An unfamiliar repository's `AGENTS.md` or equivalent project instruction file can influence agent behavior.

Review instruction files before trusting an unfamiliar repository.

---

## 19. Short FAQ

### Does the Codex prompt override the ChatGPT platform prompt?

No.

They are loaded in different systems.

Their shared Human2AI behavior comes from semantic alignment between the two canonical prompts.

### Do I paste the Codex TXT into VS Code Settings?

No.

Recommended Windows flow:

```text
canonical TXT under .codex
↓
automatic AGENTS.md mirror
↓
Codex
```

### Why do I need AGENTS.md if TXT is canonical?

Because `AGENTS.md` is Codex's documented global user instruction source.

In this architecture it is only a compatibility mirror, not a second source of truth.

### Does project_doc_fallback_filenames replace this?

Not globally.

Fallback filenames extend project-level instruction discovery.

### When should I start a new Codex session?

After changing global instructions, starting a new session is the safest way to ensure the new state is loaded.

---

## 20. Canonical links

### Human2AI prompts

- https://github.com/NullCodeLabs/Human2ai-intent-codec/blob/main/llm-platform-master-prompt.txt
- https://github.com/NullCodeLabs/Human2ai-intent-codec/blob/main/codex-vscode-master-prompt.txt

### Platform documentation

- OpenAI Custom Instructions: https://help.openai.com/en/articles/8096356
- OpenAI Codex agent instruction stack: https://openai.com/index/unrolling-the-codex-agent-loop/
- Claude Personalization: https://support.claude.com/en/articles/10185728-understanding-claude-s-personalization-features
- Claude Projects: https://support.claude.com/en/articles/9519177-how-can-i-create-and-manage-projects
- Google Instructions for Gemini: https://support.google.com/gemini/answer/16598625?hl=en
- Google Custom Gems: https://support.google.com/gemini/answer/15235603?hl=en
- Perplexity Projects: https://www.perplexity.ai/help-center/en/articles/10352961-what-are-spaces
- Kimi Projects: https://www.kimi.com/en/help/features/project
- Kimi Code Customization: https://www.kimi.com/en/help/kimi-code/cli-customization

---

@NullCodeLabs | Human2AI Intent Codec | 2026
