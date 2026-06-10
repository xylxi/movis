# Writing Recommendation System Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a documentation-backed writing recommendation system for 《第九条路》 so agents can recommend chapter direction, revision actions, and continuity updates from evidence.

**Architecture:** Add focused Markdown ledgers for character continuity, chapter history, foreshadowing, story control, and chapter navigators. Update `AGENTS.md` so future agents must read these files before writing or reviewing chapters.

**Tech Stack:** Markdown documentation, existing novel project structure, DeepSeek model policy already documented in `AGENTS.md`.

---

### Task 1: Design And Plan Documents

**Files:**
- Create: `docs/superpowers/specs/2026-06-11-writing-recommendation-system-design.md`
- Create: `docs/superpowers/plans/2026-06-11-writing-recommendation-system.md`

- [ ] **Step 1: Create the design specification**

Document the recommendation contract, the four recommendation flows, confidence thresholds, and manual-confirmation gates.

- [ ] **Step 2: Create the implementation plan**

Use checkbox steps and reference the exact files that will be created or modified.

- [ ] **Step 3: Verify documents exist**

Run: `test -f docs/superpowers/specs/2026-06-11-writing-recommendation-system-design.md && test -f docs/superpowers/plans/2026-06-11-writing-recommendation-system.md`

Expected: exit code `0`.

### Task 2: Core Continuity Ledgers

**Files:**
- Create: `novel/character-continuity.md`
- Create: `novel/chapter-ledger.md`
- Create: `novel/foreshadowing-ledger.md`

- [ ] **Step 1: Create the character continuity ledger**

Include immutable traits, current state, change variables, behavior evidence, and recommendation rules for 许行、许明远、林安.

- [ ] **Step 2: Create the chapter ledger**

Seed it with chapter 1 facts from `novel/drafts/01-glass-crack.md`.

- [ ] **Step 3: Create the foreshadowing ledger**

Seed it with chapter 1 objects and open threads: blue work notebook, water bill, shoe mark, father work message, and sensory future branches.

- [ ] **Step 4: Verify required terms**

Run: `rg "不可违背|已发生事实|状态变化|回收状态|下一章债务" novel/character-continuity.md novel/chapter-ledger.md novel/foreshadowing-ledger.md`

Expected: every ledger returns relevant matches.

### Task 3: Recommendation Checklist And Chapter Navigator

**Files:**
- Create: `novel/story-control-checklist.md`
- Create: `novel/chapter-navigators/README.md`
- Create: `novel/chapter-navigators/template.md`

- [ ] **Step 1: Create the story control checklist**

Include information sufficiency checks, recommendation output format, scoring weights, modification priority, ledger update rules, and manual-confirmation gates.

- [ ] **Step 2: Create the navigator README**

Explain when to create a navigator, what to read first, and when writing is blocked.

- [ ] **Step 3: Create the navigator template**

Include sections for source evidence, information sufficiency, candidate directions, main recommendation, DeepSeek review plan, and post-chapter ledger updates.

- [ ] **Step 4: Verify recommendation fields**

Run: `rg "推荐动作|依据证据|置信度|是否允许自动执行|信息充足" novel/story-control-checklist.md novel/chapter-navigators`

Expected: checklist and template both include these fields.

### Task 4: Agent Workflow Update

**Files:**
- Modify: `AGENTS.md`

- [ ] **Step 1: Add new key files**

Add the continuity ledger, chapter ledger, foreshadowing ledger, story control checklist, and chapter navigators to the key file list.

- [ ] **Step 2: Update the writing workflow**

Require agents to read ledgers before writing, create a chapter navigator before drafting, and update ledgers after finalization.

- [ ] **Step 3: Add auto-recommendation rules**

Record the recommendation contract and confidence thresholds.

- [ ] **Step 4: Verify references**

Run: `rg "character-continuity|chapter-ledger|foreshadowing-ledger|story-control-checklist|chapter-navigators|推荐动作" AGENTS.md`

Expected: all new files and the recommendation contract are referenced.

### Task 5: Final Verification

**Files:**
- Read-only verification across created and modified files.

- [ ] **Step 1: Check file list**

Run: `test -f novel/character-continuity.md && test -f novel/chapter-ledger.md && test -f novel/foreshadowing-ledger.md && test -f novel/story-control-checklist.md && test -f novel/chapter-navigators/README.md && test -f novel/chapter-navigators/template.md`

Expected: exit code `0`.

- [ ] **Step 2: Check no secret leakage**

Run: `rg -n "api[_-]?key|deepseek_api_key|Bearer" AGENTS.md docs/superpowers novel`

Expected: no API key value appears. Generic model-policy references are acceptable if they do not include secrets.

- [ ] **Step 3: Review git status**

Run: `git status --short`

Expected: only intended new or modified files are relevant; `.env` remains untouched and unstaged.
