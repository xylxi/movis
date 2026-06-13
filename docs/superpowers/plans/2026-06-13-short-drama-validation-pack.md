# Short Drama Validation Pack Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the first short-drama validation pack for 《第九条路》 without changing the canonical novel drafts.

**Architecture:** This is a Markdown-only content workflow. Update project workflow docs first, then add a bounded `short-drama/` workspace with adaptation rules, test-chapter selection, the first sample script, and a next-stage visual handoff list. Keep visual generation, storyboard tables, video prompts, and image2 prompts out of this stage.

**Tech Stack:** Markdown, shell verification with `rg`/`find`/`git`, canonical novel ledgers and drafts, DeepSeek `deepseek-v4-pro` for formal creative writing when an available project integration exists, image2 / built-in `image_gen` only in the later visual asset stage.

---

## File Structure

- Modify `workflow/todo.md`: reflect that the novel mother-text is complete and the current phase is the short-drama validation pack.
- Modify `workflow/production-pipeline.md`: update the phase gate and keep the downstream pipeline order.
- Create `short-drama/adaptation-control.md`: single source of truth for short-drama adaptation constraints.
- Create `short-drama/test-chapter-selection.md`: first-round test chapter selection and rationale.
- Create `short-drama/scripts/01-glass-crack-script.md`: 1-3 minute sample script for Chapter 1.
- Create `short-drama/visual-handoff/01-glass-crack-entry-list.md`: next-stage entry list only, not storyboard, prompts, or generated assets.

Do not modify any file under `novel/drafts/`.

### Task 1: Workflow Phase Sync

**Files:**
- Modify: `workflow/todo.md`
- Modify: `workflow/production-pipeline.md`
- Read: `docs/superpowers/specs/2026-06-13-short-drama-validation-pack-design.md`
- Read: `novel/chapter-ledger.md`

- [ ] **Step 1: Read the approved spec and current workflow docs**

Run:

```bash
sed -n '1,260p' docs/superpowers/specs/2026-06-13-short-drama-validation-pack-design.md
sed -n '1,260p' workflow/todo.md
sed -n '1,260p' workflow/production-pipeline.md
sed -n '1,120p' novel/chapter-ledger.md
```

Expected: the spec says this phase delivers a short-drama validation pack; the chapter ledger marks 1-9 as canonical.

- [ ] **Step 2: Update `workflow/todo.md`**

Use `apply_patch`. The updated file should contain these sections:

```markdown
## 当前阶段：短剧验证包

### 小说母本锁稿

- [x] 小说母本九章正典草稿完成
- [x] 建立小说风格规范
- [x] 更新人物连续性、章节和伏笔账本

### 短剧验证包

- [ ] 同步短剧改编总控
- [ ] 从小说章节中选出 3 个最适合短剧验证的高钩子章节
- [ ] 将第一章改编为 1-3 分钟短剧样片脚本
- [ ] 建立第一章视觉资产入口清单
- [ ] 脚本定版后再进入角色图、场景图、分镜和视频提示词
```

Keep the later “投流验证” section, but make clear it has not started.

- [ ] **Step 3: Update `workflow/production-pipeline.md`**

Use `apply_patch`. Replace the old gate with:

```markdown
当前闸门：小说母本九章正典草稿已完成，当前允许进入短剧验证包。短剧验证包先完成脚本和交接清单，脚本定版后再进入角色图、场景图、分镜、AI 视频提示词和投流执行。
```

Add a short “当前短剧验证包” subsection listing the current deliverables:

```markdown
## 当前短剧验证包

本阶段只做：

- 短剧改编总控
- 三个测试章节选择
- 第一章 1-3 分钟短剧样片脚本
- 第一章视觉资产入口清单

本阶段不生成角色图、场景图、分镜表、AI 视频提示词或 image2 prompt 成品。
```

- [ ] **Step 4: Verify workflow sync**

Run:

```bash
rg -n "当前阶段：短剧验证包|小说母本九章正典草稿已完成|短剧验证包|本阶段不生成角色图" workflow/todo.md workflow/production-pipeline.md
git diff --check
```

Expected: matches in both workflow files; `git diff --check` exits `0`.

- [ ] **Step 5: Commit workflow sync**

Run:

```bash
git add workflow/todo.md workflow/production-pipeline.md
git commit -m "docs: sync short drama validation workflow"
```

Expected: commit succeeds.

### Task 2: Adaptation Control

**Files:**
- Create: `short-drama/adaptation-control.md`
- Read: `docs/superpowers/specs/2026-06-13-short-drama-validation-pack-design.md`
- Read: `novel/series-bible.md`
- Read: `novel/family-dossier.md`
- Read: `novel/story-control-checklist.md`
- Read: `novel/foreshadowing-ledger.md`

- [ ] **Step 1: Create the short-drama directories**

Run:

```bash
mkdir -p short-drama/scripts short-drama/visual-handoff
```

Expected: directories exist.

- [ ] **Step 2: Read source constraints**

Run:

```bash
sed -n '1,260p' docs/superpowers/specs/2026-06-13-short-drama-validation-pack-design.md
sed -n '1,220p' novel/series-bible.md
sed -n '1,220p' novel/family-dossier.md
sed -n '1,240p' novel/story-control-checklist.md
sed -n '1,260p' novel/foreshadowing-ledger.md
```

Expected: source rules confirm family-growth light sci-fi positioning, no system UI, and image2 use in the later visual stage.

- [ ] **Step 3: Write `short-drama/adaptation-control.md`**

Use `apply_patch`. The file must include these sections:

```markdown
# 短剧改编总控

## 当前阶段

## 正典来源

## 改编禁忌

## 单集短剧模板

| 组件 | 要求 | 检查点 |
| --- | --- | --- |
| 选择点 | 每集只能围绕一个主选择 | 选择必须来自正典章节 |
| 可视化道具 | 每集至少一个 | 道具不能强行掉出或变成解释工具 |
| 家庭日常场景 | 每集至少一个 | 家庭压力必须有数字或动作 |
| 未来分支 | 两到三个短画面 | 只呈现代价，不给答案 |
| 父母行动示范 | 先确认伤害，再承担责任，再复盘 | 少说金句 |
| 真实代价和钩子 | 选择后必须付代价 | 结尾用未完成动作收束 |

## 未来分支表现规则

## 父母行动规则

## image2 生图阶段规则

## 脚本审查清单
```

The “正典来源” section must list all 9 canonical draft paths from `novel/chapter-ledger.md`.

The “image2 生图阶段规则” section must say image2 / built-in `image_gen` is used after script approval, not before.

- [ ] **Step 4: Verify adaptation control**

Run:

```bash
rg -n "正典来源|改编禁忌|单集短剧模板|未来分支表现规则|父母行动规则|image2|image_gen|脚本审查清单" short-drama/adaptation-control.md
rg -n "novel/drafts/0[1-9]-" short-drama/adaptation-control.md
git diff --check
```

Expected: all required sections are present; all 9 canonical draft paths appear; `git diff --check` exits `0`.

- [ ] **Step 5: Commit adaptation control**

Run:

```bash
git add short-drama/adaptation-control.md
git commit -m "docs: add short drama adaptation control"
```

Expected: commit succeeds.

### Task 3: Test Chapter Selection

**Files:**
- Create: `short-drama/test-chapter-selection.md`
- Read: `short-drama/adaptation-control.md`
- Read: `novel/chapter-ledger.md`
- Read: `novel/foreshadowing-ledger.md`
- Read: `workflow/production-pipeline.md`

- [ ] **Step 1: Read selection inputs**

Run:

```bash
sed -n '1,260p' short-drama/adaptation-control.md
sed -n '1,180p' novel/chapter-ledger.md
sed -n '1,260p' novel/foreshadowing-ledger.md
sed -n '1,220p' workflow/production-pipeline.md
```

Expected: Chapter 1, Chapter 6, Chapter 9 are already recommended in the approved spec; Chapter 3 is listed as a backup.

- [ ] **Step 2: Write `short-drama/test-chapter-selection.md`**

Use `apply_patch`. The file must include:

```markdown
# 第一轮短剧测试章节选择

## 选择结论

主测试章节：

1. 第 1 章《玻璃裂开的那一秒》
2. 第 6 章《捷径》
3. 第 9 章《第九条路》

备选章节：

- 第 3 章《不合群的人》

## 评分维度

| 维度 | 检查重点 |
| --- | --- |
| 开场钩子 | 前 5 秒是否能形成危险或异常 |
| 视觉道具 | 是否有清晰可拍的物件 |
| 选择强度 | 主角是否必须在几种代价间选择 |
| 家庭现实 | 是否有数字、账单、动作进入冲突 |
| 情绪记忆点 | 结尾是否能留下动作或关系变化 |

## 章节评估表

## 推荐动作

## 依据证据

## 解决的问题

## 预期收益

## 潜在风险

## 置信度

## 是否允许自动执行

## 替换条件
```

The “章节评估表” must include rows for chapters 1, 3, 6, and 9. Use evidence from `novel/chapter-ledger.md` and `novel/foreshadowing-ledger.md`.

- [ ] **Step 3: Verify selection file**

Run:

```bash
rg -n "第 1 章|第 6 章|第 9 章|第 3 章|玻璃裂开的那一秒|捷径|第九条路|不合群的人|推荐动作|依据证据|替换条件" short-drama/test-chapter-selection.md
git diff --check
```

Expected: all required chapters and recommendation fields are present; `git diff --check` exits `0`.

- [ ] **Step 4: Commit test chapter selection**

Run:

```bash
git add short-drama/test-chapter-selection.md
git commit -m "docs: select short drama test chapters"
```

Expected: commit succeeds.

### Task 4: Chapter 1 Sample Script

**Files:**
- Create: `short-drama/scripts/01-glass-crack-script.md`
- Read: `short-drama/adaptation-control.md`
- Read: `short-drama/test-chapter-selection.md`
- Read: `novel/drafts/01-glass-crack.md`
- Read: `novel/chapter-cards/01-glass-crack.md`
- Read: `novel/chapter-ledger.md`
- Read: `novel/writing-style-guide.md`
- Read: `novel/story-control-checklist.md`

- [ ] **Step 1: Read source packet**

Run:

```bash
sed -n '1,260p' short-drama/adaptation-control.md
sed -n '1,220p' short-drama/test-chapter-selection.md
sed -n '1,360p' novel/drafts/01-glass-crack.md
sed -n '1,220p' novel/chapter-cards/01-glass-crack.md
sed -n '1,140p' novel/chapter-ledger.md
sed -n '1,240p' novel/writing-style-guide.md
sed -n '1,220p' novel/story-control-checklist.md
```

Expected: the full canonical Chapter 1 draft is visible, including the blue work notebook completion beat, water-fee ending, and final unfinished action. The script can inherit only canonical Chapter 1 facts: shattered glass, the third-floor window, teaching director risk, `280 元` repair cost, parents' action order, the blue work notebook, and the final unfinished action.

- [ ] **Step 2: Draft the script**

Use `apply_patch` to create `short-drama/scripts/01-glass-crack-script.md`.

The file must start with:

```markdown
# 第一章短剧样片脚本：玻璃裂开的那一秒

## 基本信息

- 来源正典：`novel/drafts/01-glass-crack.md`
- 目标时长：1-3 分钟
- 核心选择：逃走、沉默，还是喊住教导主任并承认
- 主数字锚点：维修费 `280 元`
- 主视觉道具：碎玻璃、三楼窗户、维修单、蓝色工作记录本
- 能力表现：只用感官断裂和短画面，不使用系统界面
```

Then include a table with this exact header:

```markdown
| 场次 | 时间 | 场景 | 画面/动作 | 台词 | 声音/转场 | 道具或数字锚点 | 改编备注 |
| --- | --- | --- | --- | --- | --- | --- | --- |
```

The script must contain 6-8 scenes covering:

1. 0-5 seconds: physical reaction and falling glass danger.
2. 5-25 seconds: real-world choice pressure.
3. 25-55 seconds: two or three future branch flashes.
4. 55-95 seconds: Xu Xing returns to reality, shouts, and admits the kick.
5. 95-140 seconds: parents arrive and follow the action order.
6. 140-180 seconds: `280 元`, blue work notebook, and unfinished ending.

Add a final section:

```markdown
## 脚本自检

- [x] 一个明确选择点
- [x] 一个可视化道具
- [x] 一个家庭日常场景
- [x] 两到三个未来分支画面
- [x] 一个父母行动示范
- [x] 一个选择后的真实代价和章尾钩子
- [x] 未生成角色图、场景图、分镜表、视频提示词或 image2 prompt
```

For formal creative drafting, use `deepseek-v4-pro` non-thinking mode if a configured project integration is available. If no DeepSeek integration is available in this environment, write the script directly from the canonical draft and note in the self-check that external model drafting was not run.

- [ ] **Step 3: Verify script format and guardrails**

Run:

```bash
rg -n "来源正典|目标时长|核心选择|维修费 `280 元`|蓝色工作记录本|场次|声音/转场|道具或数字锚点|脚本自检" short-drama/scripts/01-glass-crack-script.md
rg -n "不使用系统界面|未生成角色图、场景图、分镜表、视频提示词或 image2 prompt" short-drama/scripts/01-glass-crack-script.md
rg -n "系统弹窗|彩票|股票|龙脉|龙鳞" short-drama/scripts/01-glass-crack-script.md
git diff --check
```

Expected: first command finds required structure; second command confirms guardrail lines are present; third command has no matches; `git diff --check` exits `0`.

- [ ] **Step 4: Commit Chapter 1 script**

Run:

```bash
git add short-drama/scripts/01-glass-crack-script.md
git commit -m "docs: draft chapter one short drama script"
```

Expected: commit succeeds.

### Task 5: Visual Handoff Entry List

**Files:**
- Create: `short-drama/visual-handoff/01-glass-crack-entry-list.md`
- Read: `short-drama/scripts/01-glass-crack-script.md`
- Read: `docs/superpowers/specs/2026-06-13-short-drama-validation-pack-design.md`

- [ ] **Step 1: Read script and visual-stage boundary**

Run:

```bash
sed -n '1,260p' short-drama/scripts/01-glass-crack-script.md
sed -n '120,180p' docs/superpowers/specs/2026-06-13-short-drama-validation-pack-design.md
```

Expected: the handoff must only list next-stage entry points and must not become a storyboard, video prompt set, image prompt set, or generated asset list.

- [ ] **Step 2: Write `short-drama/visual-handoff/01-glass-crack-entry-list.md`**

Use `apply_patch`. The file must include:

```markdown
# 第一章视觉资产入口清单

## 边界

本文件只记录下一阶段入口，不生成角色图、场景图、关键帧图、分镜表、视频提示词或 image2 prompt 成品。

## 入口表

| 来源场次 | 入口类型 | 需要确认的信息 | 脚本依赖 | 下一阶段动作 |
| --- | --- | --- | --- | --- |
```

Allowed `入口类型` values:

- 角色
- 场景
- 道具
- 情绪关键帧
- 声音/转场

The table should include entries for 8 岁许行、许明远、林安、教导主任、操场、三楼窗户、学校办公室、饭桌、碎玻璃、维修单、蓝色工作记录本, and the three future-branch visual moments if present in the script.

Do not include lens numbers, shot durations, camera movement, composition instructions, finished prompts, model parameters, filenames for generated images, or generated image paths.

- [ ] **Step 3: Verify visual handoff boundary**

Run:

```bash
rg -n "边界|入口表|来源场次|入口类型|需要确认的信息|脚本依赖|下一阶段动作|角色|场景|道具|情绪关键帧|声音/转场" short-drama/visual-handoff/01-glass-crack-entry-list.md
rg -n "镜头编号|镜头时长|镜头运动|构图|Prompt:|prompt:|提示词：|image2 prompt|生成路径|\\.png|\\.jpg|\\.webp|\\.mp4" short-drama/visual-handoff/01-glass-crack-entry-list.md
git diff --check
```

Expected: first command finds required structure; second command has no matches except the boundary sentence if it mentions forbidden artifact names; `git diff --check` exits `0`.

- [ ] **Step 4: Commit visual handoff list**

Run:

```bash
git add short-drama/visual-handoff/01-glass-crack-entry-list.md
git commit -m "docs: add chapter one visual handoff list"
```

Expected: commit succeeds.

### Task 6: Final Verification

**Files:**
- Read: `workflow/todo.md`
- Read: `workflow/production-pipeline.md`
- Read: `short-drama/adaptation-control.md`
- Read: `short-drama/test-chapter-selection.md`
- Read: `short-drama/scripts/01-glass-crack-script.md`
- Read: `short-drama/visual-handoff/01-glass-crack-entry-list.md`

- [ ] **Step 1: Verify deliverable set**

Run:

```bash
find short-drama -type f | sort
```

Expected:

```text
short-drama/adaptation-control.md
short-drama/scripts/01-glass-crack-script.md
short-drama/test-chapter-selection.md
short-drama/visual-handoff/01-glass-crack-entry-list.md
```

- [ ] **Step 2: Verify no novel drafts were changed**

Run:

```bash
git status --short novel/drafts novel/chapter-ledger.md novel/character-continuity.md novel/foreshadowing-ledger.md
```

Expected: no output.

- [ ] **Step 3: Verify no generated visual or video assets exist**

Run:

```bash
find short-drama -type f \( -name '*.png' -o -name '*.jpg' -o -name '*.jpeg' -o -name '*.webp' -o -name '*.mp4' -o -name '*.mov' \)
```

Expected: no output.

- [ ] **Step 4: Verify forbidden drift**

Run:

```bash
rg -n "彩票|股票|龙脉|龙鳞|玄幻命定|系统弹窗" short-drama workflow
```

Expected: no matches except explicit prohibition lines in `short-drama/adaptation-control.md` if they exist.

- [ ] **Step 5: Verify markdown whitespace and final status**

Run:

```bash
git diff --check
git status --short workflow short-drama novel/drafts novel/chapter-ledger.md novel/character-continuity.md novel/foreshadowing-ledger.md
```

Expected: `git diff --check` exits `0`; scoped `git status --short` has no unstaged/uncommitted files after all task commits. Ignore unrelated dirty files outside this plan's write scope, if any exist.

- [ ] **Step 6: Summarize outcome**

Report:

- files created and modified
- commit hashes for each task
- verification commands run
- whether DeepSeek was available for formal script drafting
- that image2 / `image_gen` was not invoked in this stage
