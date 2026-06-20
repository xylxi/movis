# Seedance 2.0 Video Director Workflow Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: You must use superpowers:subagent-driven-development to implement this plan task-by-task. Only fall back to superpowers:executing-plans if superpowers:subagent-driven-development is unavailable. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build and commit a reusable Chinese Codex skill for high-quality Seedance 2.0 video prompt direction, then use subagents to research popular Douyin/Hongguo AI short-drama topics and iteratively improve 15-second storyboard prompts with DeepSeek scoring until a score reaches 9/10 or more than 10 rounds have run.

**Architecture:** The skill lives as repo-tracked source under `workflow/skills/seedance2-video-director/`, with a symlink into `/Users/ruir/.codex/skills/` for local use. The research and prompt iteration artifacts live under `research/` so every scoring round can be committed and audited.

**Tech Stack:** Markdown Codex skills, local shell validation, subagent review, web research, DeepSeek API via `.env` variable `deepseek_api_key`, git commits.

## Global Constraints

- Do not modify or revert existing unrelated `short-drama/` changes.
- Skill body and references use Chinese; skill name remains `seedance2-video-director`.
- Do not create content-type playbook files for short drama, product ads, science explainers, dynamic posters, character showcases, or scenery videos in the first version.
- Keep Seedance platform capability guidance separate from the 10-layer director system.
- The 10-layer director system must be split into 10 independent Markdown files.
- Seedance 2.0 constraints must include: images <= 9, videos <= 3, audio <= 3, mixed files <= 12, generation duration 4-15 seconds, `@素材名` purpose binding, video extension phrasing, identifiable realistic face upload limitation, and reliable text-generation risk.
- Every DeepSeek improvement round must be committed separately after changes are written.
- Stop the scoring loop only when any candidate reaches 9/10 or when the completed round count is greater than 10.

---

## File Structure

Skill files:

- Create or modify: `workflow/skills/seedance2-video-director/SKILL.md`
- Create or modify: `workflow/skills/seedance2-video-director/agents/openai.yaml`
- Create or modify: `workflow/skills/seedance2-video-director/references/seedance2-platform-guide.md`
- Create or modify: `workflow/skills/seedance2-video-director/references/seedance2-quality-checks.md`
- Create or modify: `workflow/skills/seedance2-video-director/references/director-system/01-intent.md`
- Create or modify: `workflow/skills/seedance2-video-director/references/director-system/02-visual-skeleton.md`
- Create or modify: `workflow/skills/seedance2-video-director/references/director-system/03-light-material.md`
- Create or modify: `workflow/skills/seedance2-video-director/references/director-system/04-camera-distance.md`
- Create or modify: `workflow/skills/seedance2-video-director/references/director-system/05-camera-movement.md`
- Create or modify: `workflow/skills/seedance2-video-director/references/director-system/06-action-causality.md`
- Create or modify: `workflow/skills/seedance2-video-director/references/director-system/07-multi-subject-locking.md`
- Create or modify: `workflow/skills/seedance2-video-director/references/director-system/08-product-believability.md`
- Create or modify: `workflow/skills/seedance2-video-director/references/director-system/09-prompt-compilation.md`
- Create or modify: `workflow/skills/seedance2-video-director/references/director-system/10-workflow-review.md`
- Create or modify: `docs/superpowers/plans/2026-06-20-seedance2-video-director-workflow.md`

Research and iteration files:

- Create: `research/seedance2-ai-short-drama-topic-research.md`
- Create: `research/seedance2-ai-short-drama-prompt-iterations.md`
- Optional create: `workflow/tools/deepseek_score_seedance_prompts.py` if direct DeepSeek API calling needs a repeatable local helper.

Local install target:

- Create or update symlink outside git: `/Users/ruir/.codex/skills/seedance2-video-director -> /Users/ruir/Documents/movies/workflow/skills/seedance2-video-director`

---

### Task 1: Finalize The Seedance Skill Source

**Files:**
- Modify: `workflow/skills/seedance2-video-director/SKILL.md`
- Modify: `workflow/skills/seedance2-video-director/agents/openai.yaml`
- Modify: `workflow/skills/seedance2-video-director/references/seedance2-platform-guide.md`
- Modify: `workflow/skills/seedance2-video-director/references/seedance2-quality-checks.md`
- Modify: `workflow/skills/seedance2-video-director/references/director-system/*.md`

**Interfaces:**
- Produces: A valid Codex skill directory with `SKILL.md`, `agents/openai.yaml`, platform guide, quality checks, and 10 director-system references.
- Consumes: Seedance 2.0 platform facts, 10-layer video director methodology, and local skill-creator validation rules.

- [ ] **Step 1: Confirm required files exist**

Run:

```bash
find workflow/skills/seedance2-video-director -maxdepth 4 -type f | sort
```

Expected: exactly the skill entry file, `agents/openai.yaml`, two top-level reference files, and 10 files under `references/director-system/`.

- [ ] **Step 2: Fix SKILL.md navigation**

Ensure `SKILL.md` points to `references/director-system/*.md`, not `director-system/*.md`, and does not require runtime access to GitHub examples.

Run:

```bash
rg -n "director-system/|GitHub|seedance2-skill" workflow/skills/seedance2-video-director/SKILL.md
```

Expected: all director paths include `references/director-system/`; any GitHub mention is framed as optional external background rather than a runtime dependency.

- [ ] **Step 3: Strengthen 10-layer reference cards**

Each `references/director-system/*.md` must contain these sections:

```markdown
## 解决的问题
## 写作检查
## Seedance 编译要点
## 常见坏写法
## 失败修正
## 最小示例
```

Each file must explain how the layer compiles into Seedance prompt material use, time segments, camera, action, sound, or negative constraints.

- [ ] **Step 4: Run skill validation**

Run:

```bash
python /Users/ruir/.codex/skills/.system/skill-creator/scripts/quick_validate.py workflow/skills/seedance2-video-director
```

Expected: validation reports the skill is valid.

- [ ] **Step 5: Run whitespace validation**

Run:

```bash
git diff --check -- workflow/skills/seedance2-video-director docs/superpowers/plans/2026-06-20-seedance2-video-director-workflow.md
```

Expected: no whitespace errors.

---

### Task 2: Review, Install, And Commit The Skill

**Files:**
- Stage: `workflow/skills/seedance2-video-director/**`
- Stage: `docs/superpowers/plans/2026-06-20-seedance2-video-director-workflow.md`
- Do not stage: `short-drama/**`

**Interfaces:**
- Consumes: Validated skill source from Task 1.
- Produces: One git commit containing the plan and skill source, plus a local symlink for Codex skill discovery.

- [ ] **Step 1: Review staged scope before staging**

Run:

```bash
git status --short
```

Expected: unrelated `short-drama/` changes may exist but are not part of this task.

- [ ] **Step 2: Create or refresh local skill symlink**

Run:

```bash
ln -sfn /Users/ruir/Documents/movies/workflow/skills/seedance2-video-director /Users/ruir/.codex/skills/seedance2-video-director
test -L /Users/ruir/.codex/skills/seedance2-video-director
```

Expected: `test` exits 0.

- [ ] **Step 3: Stage only plan and skill source**

Run:

```bash
git add docs/superpowers/plans/2026-06-20-seedance2-video-director-workflow.md workflow/skills/seedance2-video-director
git diff --cached --stat
```

Expected: only the plan and `workflow/skills/seedance2-video-director/` files are staged.

- [ ] **Step 4: Commit the skill**

Run:

```bash
git commit -m "feat: add seedance2 video director skill"
```

Expected: commit succeeds.

---

### Task 3: Research Douyin And Hongguo AI Short-Drama Topics

**Files:**
- Create: `research/seedance2-ai-short-drama-topic-research.md`

**Interfaces:**
- Consumes: Web research results and project constraints.
- Produces: A topic research memo with source links, observed topic patterns, visual feasibility notes for 15-second Seedance segments, and recommended prompt directions.

- [ ] **Step 1: Dispatch research subagent**

Ask a subagent to research recent Douyin and Hongguo popular short-drama and AI short-drama topics, using current web sources with links. Require it to separate evidence from inference.

- [ ] **Step 2: Write research memo**

Create `research/seedance2-ai-short-drama-topic-research.md` with:

```markdown
# Seedance 2.0 AI 短剧题材调研

## 结论
## 抖音热门短剧题材
## 红果热门短剧题材
## AI 视频适配判断
## 不建议进入的拥挤题材
## 推荐测试方向
## 来源
```

- [ ] **Step 3: Commit the research memo**

Run:

```bash
git add research/seedance2-ai-short-drama-topic-research.md
git commit -m "research: summarize ai short drama topics"
```

Expected: commit succeeds.

---

### Task 4: Generate Initial 15-Second Storyboard Prompt Candidates

**Files:**
- Create or modify: `research/seedance2-ai-short-drama-prompt-iterations.md`

**Interfaces:**
- Consumes: `research/seedance2-ai-short-drama-topic-research.md`, `workflow/skills/seedance2-video-director/`, Seedance 15-second generation limit.
- Produces: Multiple candidate 15-second storyboard prompts ready for DeepSeek scoring.

- [ ] **Step 1: Select 3 to 5 candidate premises**

Use the research memo to select premises that can be expressed in 4-15 second segments and benefit from AI visuals.

- [ ] **Step 2: Write initial candidates**

For each candidate, write:

```markdown
### Candidate N

**题材钩子：**
**15 秒分镜提示词：**
**Seedance 入口：**
**素材假设：**
**风险：**
```

- [ ] **Step 3: Commit initial candidates**

Run:

```bash
git add research/seedance2-ai-short-drama-prompt-iterations.md
git commit -m "draft: add seedance short drama prompt candidates"
```

Expected: commit succeeds.

---

### Task 5: Run DeepSeek Scoring And Improvement Loop

**Files:**
- Modify: `research/seedance2-ai-short-drama-prompt-iterations.md`
- Optional create or modify: `workflow/tools/deepseek_score_seedance_prompts.py`

**Interfaces:**
- Consumes: DeepSeek API key from `.env` variable `deepseek_api_key`.
- Produces: Per-round score table, improvement notes, revised prompts, and one commit after every round.

- [ ] **Step 1: Confirm DeepSeek credential variable exists without printing the key**

Run:

```bash
sed -n 's/=.*//p' .env | rg '^deepseek_api_key$'
```

Expected: prints `deepseek_api_key`.

- [ ] **Step 2: Score round 1**

Use DeepSeek to score each candidate from 0 to 10 on:

```text
Seedance 可执行性 2 分
15 秒节奏可控性 2 分
题材钩子强度 2 分
画面/运镜/动作指令质量 2 分
差异化与投流潜力 2 分
```

- [ ] **Step 3: Record score and improvements**

Append a round section to `research/seedance2-ai-short-drama-prompt-iterations.md`:

```markdown
## Round N

| Candidate | Score | Main issue | Revision action |
| --- | ---: | --- | --- |

### Revised Prompts
```

- [ ] **Step 4: Commit each round**

Run after every round:

```bash
git add research/seedance2-ai-short-drama-prompt-iterations.md
if [ -f workflow/tools/deepseek_score_seedance_prompts.py ]; then git add workflow/tools/deepseek_score_seedance_prompts.py; fi
git commit -m "iterate: improve seedance prompts round N"
```

Expected: commit succeeds when tracked files changed. If no helper script exists, only the research iteration file is staged.

- [ ] **Step 5: Stop check**

After each round, stop only if any score is at least 9/10 or if the completed round count is greater than 10. Otherwise repeat Steps 2-4.

---

## Self-Review

- Spec coverage: The plan covers skill creation, subagent implementation, validation, commit, local install, research, prompt candidates, DeepSeek scoring, per-round commits, and stop conditions.
- Placeholder scan: No `TBD`, `TODO`, or undefined implementation step remains.
- Scope check: Skill development and prompt iteration are sequential deliverables under one requested goal; each produces a separate commit and can be reviewed independently.
