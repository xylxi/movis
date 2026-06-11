# Ninth Road Complete Novel Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Complete the remaining novel mother-text chapters 3-9 of 《第九条路》 as canonical drafts, then update continuity ledgers.

**Architecture:** Work chapter by chapter from the existing chapter cards, canonical drafts, and continuity ledgers. Each chapter gets a navigator, a canonical no-version draft, DeepSeek review evidence, and ledger updates before moving to the next chapter.

**Tech Stack:** Markdown novel files, project continuity ledgers, `deepseek-v4-pro` for formal writing and review, local shell verification.

---

### Task 1: Preflight Context And Safety

**Files:**
- Read: `AGENTS.md`
- Read: `novel/drafts/01-glass-crack.md`
- Read: `novel/drafts/02-first-lie.md`
- Read: `novel/chapter-ledger.md`
- Read: `novel/character-continuity.md`
- Read: `novel/foreshadowing-ledger.md`
- Read: `novel/writing-style-guide.md`

- [x] **Step 1: Confirm deliverable**

User selected option 1: complete the novel mother-text, not short-drama adaptation.

- [x] **Step 2: Confirm canonical sources**

Use only no-version canonical drafts listed in `novel/chapter-ledger.md`.

- [x] **Step 3: Verify no chapter-version drafts remain**

Run: `find novel/drafts -maxdepth 1 -type f -name '*version*'`

Expected: no output.

### Task 2: Chapter Navigators For 3-9

**Files:**
- Create: `novel/chapter-navigators/03-wrong-friends-navigator.md`
- Create: `novel/chapter-navigators/04-grade-pressure-navigator.md`
- Create: `novel/chapter-navigators/05-major-choice-navigator.md`
- Create: `novel/chapter-navigators/06-shortcut-navigator.md`
- Create: `novel/chapter-navigators/07-relationship-navigator.md`
- Create: `novel/chapter-navigators/08-marriage-navigator.md`
- Create: `novel/chapter-navigators/09-ninth-road-navigator.md`

- [x] **Step 1: Generate each navigator**

For each chapter, include information sufficiency, source evidence, main recommendation, writing controls, DeepSeek review plan, and post-draft ledger updates.

- [x] **Step 2: Verify required fields**

Run: `rg "信息充足|推荐动作|依据证据|本章写作控制|定稿后反写" novel/chapter-navigators`

Expected: every new navigator includes these fields.

### Task 3: Canonical Drafts For 3-9

**Files:**
- Create: `novel/drafts/03-wrong-friends.md`
- Create: `novel/drafts/04-grade-pressure.md`
- Create: `novel/drafts/05-major-choice.md`
- Create: `novel/drafts/06-shortcut.md`
- Create: `novel/drafts/07-relationship.md`
- Create: `novel/drafts/08-marriage.md`
- Create: `novel/drafts/09-ninth-road.md`

- [x] **Step 1: Draft chapters using `deepseek-v4-pro` non-thinking mode**

Each chapter must follow its chapter card, navigator, canonical ledgers, and style guide.

- [x] **Step 2: Keep chapter scope stable**

Each chapter must contain one concrete real event, one key choice, one future-branch sequence, one family pressure number/action, parent action mirrors, a real cost, and an unfinished ending.

- [x] **Step 3: Avoid forbidden drift**

Do not introduce systems, destiny, specific-profit predictions, controlling parents, or adult-gold-line summaries.

### Task 4: Review And Revision

**Files:**
- Create: `research/deepseek-v4pro-03-wrong-friends-review-log.md`
- Create: `research/deepseek-v4pro-04-grade-pressure-review-log.md`
- Create: `research/deepseek-v4pro-05-major-choice-review-log.md`
- Create: `research/deepseek-v4pro-06-shortcut-review-log.md`
- Create: `research/deepseek-v4pro-07-relationship-review-log.md`
- Create: `research/deepseek-v4pro-08-marriage-review-log.md`
- Create: `research/deepseek-v4pro-09-ninth-road-review-log.md`

- [x] **Step 1: Run DeepSeek structural review**

Use `deepseek-v4-pro`, thinking mode, `reasoning_effort=high`, with the story-control score weights.

- [x] **Step 2: Apply only necessary revisions**

Apply must-fix issues and low-risk high-impact changes. Stop when remaining issues are low-gain polish or would damage continuity.

- [x] **Step 3: Record review result**

Each log records score, must-fix issues, applied fixes, and stop reason.

### Task 5: Ledger Updates

**Files:**
- Modify: `novel/chapter-ledger.md`
- Modify: `novel/character-continuity.md`
- Modify: `novel/foreshadowing-ledger.md`
- Modify only if reusable rule emerges: `novel/writing-style-guide.md`

- [x] **Step 1: Update chapter ledger**

Add canonical rows for chapters 3-9 and a status section for each chapter.

- [x] **Step 2: Update character continuity**

Record actual state changes only, not candidate ideas.

- [x] **Step 3: Update foreshadowing ledger**

Mark each chapter's object, ability, and relationship threads as opened, advanced, recovered, or paused.

### Task 6: Final Verification

**Files:**
- Read all created and modified Markdown files.

- [x] **Step 1: Check canonical draft set**

Run: `find novel/drafts -maxdepth 1 -type f | sort`

Expected: `01` through `09` no-version draft files, no temporary version files.

- [x] **Step 2: Check forbidden text and wrong names**

Run: `rg -n "系统|龙脉|龙鳞|彩票|股票|林秀|胡秀兰|02-first-lie-version|version-" novel/drafts novel/chapter-ledger.md novel/character-continuity.md novel/foreshadowing-ledger.md`

Expected: no matches except allowed generic rule text in control docs.

- [x] **Step 3: Check markdown whitespace**

Run: `git diff --check`

Expected: exit code `0`.

- [x] **Step 4: Check no secret leakage**

Run: `rg -n "deepseek[_-]?api[_-]?key=|Bearer[[:space:]]+[A-Za-z0-9_.-]+" novel research docs AGENTS.md README.md`

Expected: no matches.
