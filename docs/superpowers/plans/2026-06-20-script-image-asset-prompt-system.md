# Script Image Asset Prompt System Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Operationalize the script image asset prompt system for `projects/frozen-rebirth-revenge` without overwriting the existing generated asset records.

**Architecture:** Add project-local guidance and a v2 pilot layer that sits beside the current official asset files. The pilot layer contains upgraded briefs, a pilot index, v2 prompts, and a quality check, so the user can review the new system before any official `asset-briefs.md`, `image-generation-prompts.md`, or `_asset-index.md` content is merged.

**Tech Stack:** Markdown documentation, shell validation with `rg`, `test`, and `git diff --check`; no runtime dependencies.

## Global Constraints

- Work only inside `/Users/ruir/Documents/movies`.
- Current formal project is `projects/frozen-rebirth-revenge/PROJECT.md`.
- Project facts must come only from `projects/frozen-rebirth-revenge/`.
- Preserve existing user changes; do not revert or overwrite modified files.
- Do not modify `projects/frozen-rebirth-revenge/assets/asset-briefs.md`, `projects/frozen-rebirth-revenge/assets/image-generation-prompts.md`, or `projects/frozen-rebirth-revenge/assets/_asset-index.md` in this plan.
- Final images stay in `projects/frozen-rebirth-revenge/assets/`.
- `@素材名` must match `assets/素材名.png` when an asset becomes official.
- Single scene images must remain one space or one spatial function, with no arrows, marker lines, multi-panel layout, or explanatory text.
- Only approved assets may enter formal video handoff.
- Video-facing wording must land on subject, space, light, lens, action, and timeline rather than vague style stacking.
- This plan creates a pilot; it does not generate or overwrite PNG files.

---

## File Structure

- Create `projects/frozen-rebirth-revenge/assets/asset-prompt-guidelines.md`: project-local rules distilled from the approved spec, written for future asset authors.
- Create `projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md`: upgraded v2 briefs for eight pilot assets using `subtype`, `摄影语言`, `连续性约束`, and `质检重点`.
- Create `projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md`: pilot index matching the eight v2 briefs and their planned files.
- Create `projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md`: copyable v2 image prompts for the same eight pilot assets.
- Create `projects/frozen-rebirth-revenge/reviews/asset-prompt-system-quality-check.md`: validation checklist and command evidence for the pilot docs.

The official generated records remain untouched during the pilot:

- `projects/frozen-rebirth-revenge/assets/asset-briefs.md`
- `projects/frozen-rebirth-revenge/assets/image-generation-prompts.md`
- `projects/frozen-rebirth-revenge/assets/_asset-index.md`

---

### Task 1: Project-Local Asset Prompt Guidelines

**Files:**
- Create: `projects/frozen-rebirth-revenge/assets/asset-prompt-guidelines.md`

**Interfaces:**
- Consumes: `docs/superpowers/specs/2026-06-20-script-image-asset-prompt-system-design.md`
- Produces: A project-local guide referenced by later pilot files as the writing rule source.

- [ ] **Step 1: Run the failing presence check**

```bash
test -f projects/frozen-rebirth-revenge/assets/asset-prompt-guidelines.md
```

Expected: FAIL with exit code `1`, because the guide does not exist yet.

- [ ] **Step 2: Create the guide**

Use `apply_patch` to create `projects/frozen-rebirth-revenge/assets/asset-prompt-guidelines.md` with this exact content:

````markdown
# 素材提示词写作规范

适用项目：极寒重生复仇爽剧
适用阶段：素材 brief、生图提示词、素材质检、后续 Seedance 参考图筛选

## 核心顺序

素材提示词的优先级：

```text
剧情功能 > 连续性 > 可拍动作 > 摄影语言 > 单张图审美
```

不要只写“高级、好看、性感、电影感”。必须把它们翻译成可见事实：年龄、身份、动作、服装剪裁、空间结构、光源、镜头、景深、材质、天气结果和禁用元素。

## 标准字段

```text
@中文素材名
type：character / character-keyframe / scene / prop / crowd / atmosphere / ui-text / story-reference
subtype：character-sheet / character-keyframe / scene-base / evidence-prop / crowd-environment / weather-state
用途：
画面要求：
关键细节：
摄影语言：
连续性约束：
禁用元素：
file：assets/中文素材名.png
status：planned / generated / approved / rejected
质检重点：
```

兼容现有正式文件时，可以先把 v2 内容写入 `*-v2-pilot.md`，用户确认后再合并进正式 `asset-briefs.md`、`image-generation-prompts.md` 和 `_asset-index.md`。

## 通用提示词公式

```text
[素材用途和类型]，[主体是谁/是什么 + 动作/状态]，
[地点 + 时间 + 天气/环境压力]，
[现实主义短剧 / 电影剧照 / 抓拍摄影等 1 到 2 个主风格]，
[光线来源 + 光线方向 + 色温/反光结果]，
[镜头焦段 + 构图 + 景深 + 机位]，
[材质、服装、皮肤、道具、环境被天气影响后的结果]，
[背景只保留 2 到 3 个服务剧情的元素]，
[情绪或叙事状态]，
[连续性约束]，
[负面约束]
```

## 类型规则

人物设定图可以包含多姿态，但不要文字标签、箭头、角色属性表和复杂说明。它负责锁定长期连续性。

人物关键帧只生成一个可拍瞬间。它负责锁定具体动作、身体反应、道具关系和情绪转折。

场景基底图只对应一个空间或一个空间功能。不要人物、动线图、镜头框、箭头、红圈、说明文字和多格拼版。

道具图要说明剧情功能：录制、证明、交换、威胁、生存、藏匿或损坏。不要可读品牌、长文字和教程式箭头。

路人群体图要写人数范围、动作方向、密度、年龄层、服装季节和是否虚化。不要只写“很多路人”。

气候环境图必须写天气带来的结果：雪水脚印、结冰路面、雾化玻璃、衣服雨滴、湿润皮肤高光、路面反光、断电暗区。

UI 和画面文字只在剧情必须依赖短文字时使用。必须出现的文字加引号；长说明交给后期字幕或设计工具。

## 极寒项目负面约束

通用：

```text
不要低清晰度，不要水印，不要 logo，不要乱码文字，不要多格拼版，不要箭头，不要标记线，不要说明文字。
```

人物：

```text
不要未成年人感，不要畸形手指，不要多余手指，不要肢体扭曲，不要塑料皮肤，不要过度磨皮，不要无关人物。
```

成年吸睛女性：

```text
不要未成年人感，不要露点，不要透明服装，不要裸露性器官，不要性行为暗示，不要低质艳俗，不要偷拍感。
```

场景和极寒：

```text
不要末日废墟，不要怪物，不要夸张爆炸，不要科幻基地，不要不合现实的豪宅物资堆，不要不属于当前项目的时代和地点。
```

## 质检闸门

- `@素材名`、保存文件、索引名一致。
- 场景图是单空间，不含箭头、说明文字、拼版。
- 人物年龄、服装、发型、关键道具符合 `bible.md`。
- 道具无品牌和长文字。
- 气候影响真实落到地面、衣服、玻璃、光线。
- 素材能被镜头节拍引用。
- 未确认图片不得进入正式视频 handoff。
````

- [ ] **Step 3: Validate the guide**

```bash
rg -n "剧情功能 > 连续性 > 可拍动作 > 摄影语言 > 单张图审美" projects/frozen-rebirth-revenge/assets/asset-prompt-guidelines.md
rg -n "type：character / character-keyframe / scene / prop / crowd / atmosphere / ui-text / story-reference" projects/frozen-rebirth-revenge/assets/asset-prompt-guidelines.md
git diff --check -- projects/frozen-rebirth-revenge/assets/asset-prompt-guidelines.md
```

Expected: both `rg` commands print one matching line, and `git diff --check` exits `0`.

- [ ] **Step 4: Commit**

```bash
git add projects/frozen-rebirth-revenge/assets/asset-prompt-guidelines.md
git commit -m "docs: add asset prompt guidelines"
```

Expected: commit succeeds and includes only `asset-prompt-guidelines.md`.

---

### Task 2: V2 Pilot Briefs And Pilot Index

**Files:**
- Create: `projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md`
- Create: `projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md`

**Interfaces:**
- Consumes: Task 1 guide.
- Produces: Eight pilot asset definitions that Task 3 must match exactly by `@素材名` and file path.

- [ ] **Step 1: Run failing presence checks**

```bash
test -f projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md
test -f projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md
```

Expected: both commands FAIL with exit code `1`, because the pilot files do not exist yet.

- [ ] **Step 2: Create the v2 pilot brief file**

Use `apply_patch` to create `projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md` with this exact content:

````markdown
# 第一集素材 Brief v2 试点

说明：本文件是 `asset-prompt-guidelines.md` 的试点落地稿，不覆盖正式 `asset-briefs.md`。试点选择 8 个高价值素材：5 个已有素材的 v2 重写方向，3 个后续剧本和视频生成更需要的新素材。用户确认后，再决定是否合并进正式文件。

## 人物设定图

### @沈知夏设定图

type：character
subtype：character-sheet
用途：锁定女主长期外观、短发、冷静高智状态、深 V 吸睛但不裸露的主服装轮廓。
画面要求：29 岁中国成年女性，现代现实主义短剧人物设定图，包含正面全身、侧面半身、手持物资清单、冷静抬眼动作。
关键细节：短发，浅灰短款羽绒外套敞开，黑色深 V 修身内搭，腰线清楚，黑色高腰窄腿裤或皮裤，黑色长靴，皮手套，透明文件袋，手机。
摄影语言：干净浅灰背景，柔和棚拍光，50mm 自然人像视角，真实织物和皮肤质感，轮廓清楚。
连续性约束：后续场次保持短发、浅灰外套、黑色内搭、文件袋和手机；不要把她改成末世战甲或豪门女总裁造型。
禁用元素：不要未成年人感，不要露点，不要透明服装，不要裸露性器官，不要性行为暗示，不要低质网红妆，不要血污，不要文字标签。
file：`assets/沈知夏设定图.png`
status：planned
质检重点：人物必须成年；服装吸睛但不裸露；能作为后续关键帧的外观基准。

### @沈晚设定图

type：character
subtype：character-sheet
用途：锁定继妹甜美吸睛、装弱、直播卖惨和偷药功能。
画面要求：24 岁中国成年女性，现代现实主义短剧人物设定图，包含正面全身、侧面半身、举手机直播、抱小药箱遮挡动作。
关键细节：长卷发或高马尾，精致妆容，白色短款羽绒外套敞开，米白或浅粉深 V 修身内搭，腰线清楚，浅色修身短裙或浅色窄腿裤，白色长靴，手机补光灯，小药箱。
摄影语言：干净浅灰背景，柔和棚拍光，85mm 人像压缩感，皮肤和织物真实，眼神无辜但有算计。
连续性约束：后续直播、围门、抢药场次保持手机补光灯和小药箱；不要把她画成未成年、古装恶女或夸张哭花脸。
禁用元素：不要未成年人感，不要露点，不要透明服装，不要裸露性器官，不要性行为暗示，不要古早恶女妆，不要文字标签。
file：`assets/沈晚设定图.png`
status：planned
质检重点：甜美和算计同时成立；手机补光灯与药箱必须清楚。

## 场景和环境

### @暴雪楼道场景图

type：scene
subtype：scene-base
用途：上一世死亡、断电围门、撬门失败、递药关键帧的空间基准。
画面要求：单画面现代高层住宅楼道，竖屏 9:16，冬夜断电，防盗门在中景，楼梯间方向可见。
关键细节：防盗门、门缝微弱暖光、暗红应急灯、少量雪水脚印、门口地垫、门铃摄像头位置、楼梯间方向。
摄影语言：28mm 环境视角，中等景深，冷白门缝光和暗红应急灯形成色温冲突，地面反光体现湿冷。
连续性约束：必须能承接 `@公寓防盗门内侧场景图`；门铃摄像头位置要方便后续录制和围门镜头。
禁用元素：不要废土破楼，不要血迹，不要人物，不要箭头，不要标记线，不要文字说明，不要多格拼版。
file：`assets/暴雪楼道场景图.png`
status：planned
质检重点：空间普通真实；暴雪和停电通过光线、脚印、冷色体现，不靠灾难废墟。

### @公寓防盗门内侧场景图

type：scene
subtype：scene-base
用途：门挡、对讲、摄像头、门缝递药、拒绝仇人进门的室内空间基准。
画面要求：单画面公寓防盗门内侧，竖屏 9:16，门链、安全链、门挡、对讲屏、鞋柜、门边小桌清楚。
关键细节：门挡顶住，门缝有冷光，摄像头或对讲红点亮起，手机屏幕只是模糊光块，鞋柜和门边小桌普通真实。
摄影语言：35mm 室内环境中景，中等景深，门缝冷光和室内弱暖光对比，机位略低以强调门挡阻力。
连续性约束：必须与楼道侧防盗门对应；不要出现夸张机关、豪宅玄关或科幻安防。
禁用元素：不要可读监控文字，不要夸张机关，不要人物，不要箭头，不要标记线，不要多格拼版。
file：`assets/公寓防盗门内侧场景图.png`
status：planned
质检重点：门挡和安全链必须可见；空间要能支持递药动作。

### @停电楼道气候图

type：atmosphere
subtype：weather-state
用途：锁定场次 09 到 12 的断电、低温、围门压力和楼道环境结果。
画面要求：单画面现代住宅楼道气候状态，竖屏 9:16，断电后暗红应急灯，门缝冷暖光对比，空气里有轻微白气。
关键细节：地面雪水脚印、墙角结霜、几处湿冷反光、暗红应急灯、远处楼梯间黑暗、门口冷风从缝隙灌入的视觉结果。
摄影语言：35mm 环境中景，深景深，低照度，冷白和暗红混合光，画面噪点轻微但不低清。
连续性约束：必须服务 `@暴雪楼道场景图`，只加强气候状态，不改变楼道结构。
禁用元素：不要人物，不要废土破楼，不要怪物，不要爆炸，不要文字说明，不要箭头，不要多格拼版。
file：`assets/停电楼道气候图.png`
status：planned
质检重点：天气结果必须落在地面、墙角、空气和光线，而不是只写“冷”。

## 道具

### @门铃摄像头道具图

type：prop
subtype：evidence-prop
用途：锁定门铃摄像头、录制红点和手机模糊监控光块，服务改锁、围门、证据反制。
画面要求：单画面门铃摄像头道具参考图，竖屏 9:16，现代公寓门框上的小型门铃摄像头，红点亮起。
关键细节：摄像头安装在门框，防盗门局部清楚，旁边手机屏幕只是模糊光块，门框材质真实。
摄影语言：50mm 近景，浅景深，冷色走廊光，摄像头红点作为视觉焦点。
连续性约束：摄像头位置要能对应楼道和门内对讲镜头；不要出现品牌或可读界面。
禁用元素：不要可读聊天记录，不要品牌 logo，不要界面文字，不要多格拼版，不要教程箭头。
file：`assets/门铃摄像头道具图.png`
status：planned
质检重点：红点清楚；手机屏幕不可读；摄像头不是科幻设备。

## 关键帧和群体

### @门缝递药关键帧

type：character-keyframe
subtype：character-keyframe
用途：场次 11 的代价选择，女主只救真正求助的邻居母子，同时拒绝仇人进门。
画面要求：单画面短剧关键帧，沈知夏在防盗门内侧只打开安全链，把热水袋和退烧贴从门缝递给楼道里的年轻母亲。
关键细节：门链拉紧，门挡顶住，沈知夏戴皮手套，门外母亲抱着发烧孩子，孩子额头退烧贴，顾承泽只在背景边缘被老周挡住。
摄影语言：35mm 门缝视角，中等景深，室内弱暖光和楼道冷红应急灯混合，手和药品处于画面焦点。
连续性约束：沈知夏保持浅灰外套、黑色内搭和皮手套；邻居母子保持疲惫但克制；不要让仇人进入室内。
禁用元素：不要多格拼版，不要说明文字，不要血腥，不要病危夸张，不要让门完全打开，不要无关人物挤满画面。
file：`assets/门缝递药关键帧.png`
status：planned
质检重点：门只开安全链宽度；药品和热水袋必须可见；“救人但不放人进门”的动作成立。

### @暴雪围门群体图

type：crowd
subtype：crowd-environment
用途：场次 09 到 12 的门外群体压力，表现顾承泽、沈晚、陈兰和邻居围在门口，但不抢主角空间。
画面要求：单画面楼道群体环境参考，8 到 12 名成年人穿厚外套挤在现代住宅楼道，围在一扇防盗门外。
关键细节：顾承泽型男性拍门，甜美女性举低手机补光，成熟女性抱保温杯发抖，邻居围观但保持距离，地面有雪水脚印。
摄影语言：28mm 环境广角，中等景深，暗红应急灯和手机补光混合，前景门框压迫感，背景人群略虚化。
连续性约束：群体只服务围门压力；不要把楼道变成暴乱现场；不要出现警察、武器或血腥冲突。
禁用元素：不要明确可识别明星脸，不要夸张暴乱，不要血腥，不要水印，不要文字横幅，不要多格拼版。
file：`assets/暴雪围门群体图.png`
status：planned
质检重点：人数范围 8 到 12；所有人是成年人；人群压力强但仍是现实小区楼道。
````

- [ ] **Step 3: Create the v2 pilot index file**

Use `apply_patch` to create `projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md` with this exact content:

````markdown
# 第一集素材索引 v2 试点

说明：本索引只对应 v2 试点文件，不替代正式 `_asset-index.md`。用户确认后，再把选中的素材合并进正式索引。

| @素材名 | type | subtype | file | status | 用途 |
| --- | --- | --- | --- | --- | --- |
| @沈知夏设定图 | character | character-sheet | `assets/沈知夏设定图.png` | planned | 女主长期外观和吸睛服装连续性 |
| @沈晚设定图 | character | character-sheet | `assets/沈晚设定图.png` | planned | 继妹甜美吸睛、直播手机和药箱 |
| @暴雪楼道场景图 | scene | scene-base | `assets/暴雪楼道场景图.png` | planned | 楼道、防盗门、应急灯、门铃摄像头 |
| @公寓防盗门内侧场景图 | scene | scene-base | `assets/公寓防盗门内侧场景图.png` | planned | 门内对讲、门挡、安全链和递药空间 |
| @停电楼道气候图 | atmosphere | weather-state | `assets/停电楼道气候图.png` | planned | 断电楼道、低温白气、雪水脚印和暗红应急灯 |
| @门铃摄像头道具图 | prop | evidence-prop | `assets/门铃摄像头道具图.png` | planned | 门铃摄像头、录制红点和模糊监控光块 |
| @门缝递药关键帧 | character-keyframe | character-keyframe | `assets/门缝递药关键帧.png` | planned | 只开安全链递药，救邻居但拒绝仇人 |
| @暴雪围门群体图 | crowd | crowd-environment | `assets/暴雪围门群体图.png` | planned | 断电后门外 8 到 12 名成年人围门施压 |
````

- [ ] **Step 4: Validate pilot briefs and index**

```bash
test "$(rg -c '^### @' projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md)" -eq 8
test "$(awk -F'|' '$2 ~ /@/ && $2 !~ /@素材名/ {count++} END {print count+0}' projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md)" -eq 8
rg -n "摄影语言：" projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md
rg -n "连续性约束：" projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md
rg -n "质检重点：" projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md
git diff --check -- projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md
```

Expected: the two `test` commands exit `0`; each `rg` command prints eight matching lines; `git diff --check` exits `0`.

- [ ] **Step 5: Commit**

```bash
git add projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md
git commit -m "docs: add pilot v2 asset briefs"
```

Expected: commit succeeds and includes only the two v2 pilot brief/index files.

---

### Task 3: V2 Pilot Image Generation Prompts

**Files:**
- Create: `projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md`

**Interfaces:**
- Consumes: Task 2 `@素材名` and file paths.
- Produces: Eight copyable prompts that match the pilot briefs and index exactly.

- [ ] **Step 1: Run the failing presence check**

```bash
test -f projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md
```

Expected: FAIL with exit code `1`, because the v2 pilot prompts file does not exist yet.

- [ ] **Step 2: Create the v2 pilot prompts file**

Use `apply_patch` to create `projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md` with this exact content:

````markdown
# 第一集素材生图提示词 v2 试点

说明：本文件不覆盖正式 `image-generation-prompts.md`。每条提示词生成一张独立图片；生成前由用户确认是否覆盖同名文件或另存为临时图。

## 人物设定图

### @沈知夏设定图

保存文件：`assets/沈知夏设定图.png`

提示词：

```text
现代现实主义短剧人物设定图，29 岁中国成年女性沈知夏，城市规划公司项目经理，冷艳高智感，短发，眼神清醒克制但有强烈镜头吸引力。浅灰短款羽绒外套敞开，黑色深 V 修身内搭，腰线清楚，黑色高腰窄腿裤或皮裤，黑色长靴，皮手套，手边有透明文件袋和手机。画面包含正面全身、侧面半身、手持物资清单、冷静抬眼的动作参考，干净浅灰背景，柔和棚拍光，50mm 自然人像视角，真实织物和皮肤质感。后续所有场次保持短发、浅灰外套、黑色内搭、文件袋和手机。不要未成年人感，不要露点，不要透明服装，不要裸露性器官，不要性行为暗示，不要末世战甲，不要低质网红妆，不要血污，不要文字标签。
```

禁用元素：未成年人感、露点、透明服装、裸露性器官、性行为暗示、末世战甲、低质网红妆、血污、文字标签。

质检重点：人物成年；服装吸睛但不裸露；短发、浅灰外套、黑色内搭、文件袋和手机清楚。

### @沈晚设定图

保存文件：`assets/沈晚设定图.png`

提示词：

```text
现代现实主义短剧人物设定图，24 岁中国成年女性沈晚，甜美吸睛绿茶感，会利用外貌和镜头，表情无辜但眼神有算计。长卷发或高马尾，精致妆容，白色短款羽绒外套敞开，米白或浅粉深 V 修身内搭，腰线清楚，浅色修身短裙或浅色窄腿裤，白色长靴，手持手机补光灯和小药箱。画面包含正面全身、侧面半身、举手机直播、抱小药箱遮挡的动作参考，干净浅灰背景，柔和棚拍光，85mm 人像压缩感，真实皮肤和织物质感。后续直播、围门、抢药场次保持手机补光灯和小药箱。不要未成年人感，不要露点，不要透明服装，不要裸露性器官，不要性行为暗示，不要古早恶女妆，不要夸张哭花脸，不要文字标签。
```

禁用元素：未成年人感、露点、透明服装、裸露性器官、性行为暗示、古早恶女妆、夸张哭花脸、文字标签。

质检重点：甜美和算计同时成立；手机补光灯与小药箱必须清楚。

## 场景和环境

### @暴雪楼道场景图

保存文件：`assets/暴雪楼道场景图.png`

提示词：

```text
单画面现代高层住宅楼道场景参考，竖屏 9:16，冬夜断电，防盗门在中景，门缝透出微弱暖光，楼道应急灯暗红，地面有少量雪水脚印和湿冷反光，门口地垫，门铃摄像头在门框上，远处能看到楼梯间方向。28mm 环境视角，中等景深，冷白门缝光和暗红应急灯形成色温冲突，真实普通小区楼道，可承接围门、撬门和递药动作。不要废土破楼，不要血迹，不要人物，不要箭头，不要标记线，不要文字说明，不要多格拼版。
```

禁用元素：废土破楼、血迹、人物、箭头、标记线、文字说明、多格拼版。

质检重点：普通真实小区楼道；门铃摄像头位置清楚；暴雪和停电通过光线、脚印、地面反光体现。

### @公寓防盗门内侧场景图

保存文件：`assets/公寓防盗门内侧场景图.png`

提示词：

```text
单画面现代公寓防盗门内侧场景参考，竖屏 9:16，门链、安全链、门挡、门铃对讲屏、鞋柜和门边小桌清晰可见，门挡顶住，门缝有冷光，手机屏幕只是模糊光块，摄像头或对讲录制红点可见。35mm 室内环境中景，中等景深，门缝冷光和室内弱暖光对比，机位略低以强调门挡阻力，普通都市公寓入口，可支持门缝递药和拒绝开门动作。不要夸张机关，不要可读监控文字，不要人物，不要箭头，不要标记线，不要多格拼版。
```

禁用元素：夸张机关、可读监控文字、人物、箭头、标记线、多格拼版。

质检重点：门挡和安全链必须可见；空间能支持递药动作；不要豪宅玄关。

### @停电楼道气候图

保存文件：`assets/停电楼道气候图.png`

提示词：

```text
单画面现代住宅楼道气候状态参考，竖屏 9:16，暴雪夜断电后，暗红应急灯照着防盗门和楼梯间，门缝有微弱冷暖光对比，空气里有轻微白气。地面有雪水脚印、湿冷反光，墙角轻微结霜，远处楼梯间黑暗，门口像有冷风从缝隙灌入。35mm 环境中景，深景深，低照度，冷白和暗红混合光，画面噪点轻微但清晰真实。只加强 `暴雪楼道场景图` 的低温和断电状态，不改变楼道结构。不要人物，不要废土破楼，不要怪物，不要爆炸，不要文字说明，不要箭头，不要多格拼版。
```

禁用元素：人物、废土破楼、怪物、爆炸、文字说明、箭头、多格拼版。

质检重点：寒冷必须通过白气、脚印、结霜、地面反光和应急灯体现。

## 道具

### @门铃摄像头道具图

保存文件：`assets/门铃摄像头道具图.png`

提示词：

```text
单画面门铃摄像头道具参考图，竖屏 9:16，现代公寓门框上的小型门铃摄像头，红点亮起，门框和防盗门局部清楚，旁边手机屏幕只是模糊光块，用于表现录制和监控证据。50mm 近景，浅景深，冷色走廊光，摄像头红点作为视觉焦点，真实家用安防设备质感。不要可读聊天记录，不要品牌 logo，不要界面文字，不要多格拼版，不要教程箭头。
```

禁用元素：可读聊天记录、品牌 logo、界面文字、多格拼版、教程箭头。

质检重点：红点清楚；手机屏幕不可读；摄像头不是科幻设备。

## 关键帧和群体

### @门缝递药关键帧

保存文件：`assets/门缝递药关键帧.png`

提示词：

```text
单画面现代现实主义短剧关键帧，沈知夏在公寓防盗门内侧只打开安全链，把热水袋和退烧贴从门缝递给楼道里的年轻母亲。暴雪断电夜，门链拉紧，门挡顶住，沈知夏穿浅灰羽绒外套、黑色深 V 修身内搭和皮手套，手和药品处于画面焦点；门外母亲抱着发烧孩子，孩子额头有退烧贴，顾承泽只在背景边缘被老周挡住。35mm 门缝视角，中等景深，室内弱暖光和楼道暗红应急灯混合，画面表达“救人但不让仇人进门”。不要多格拼版，不要说明文字，不要血腥，不要病危夸张，不要让门完全打开，不要无关人物挤满画面。
```

禁用元素：多格拼版、说明文字、血腥、病危夸张、门完全打开、无关人物挤满画面。

质检重点：门只开安全链宽度；药品和热水袋可见；救邻居但拒绝仇人的动作成立。

### @暴雪围门群体图

保存文件：`assets/暴雪围门群体图.png`

提示词：

```text
单画面现代住宅楼道群体环境参考，暴雪断电夜，8 到 12 名成年人穿厚外套挤在防盗门外形成围门压力。顾承泽型都市男性拍门，甜美女性举低手机补光，成熟女性抱保温杯发抖，几名邻居围观但保持距离，地面有雪水脚印，楼道应急灯暗红。28mm 环境广角，中等景深，暗红应急灯和手机补光混合，前景门框形成压迫感，背景人群略虚化。现实小区楼道，不是暴乱现场。不要明确可识别明星脸，不要夸张暴乱，不要血腥，不要水印，不要文字横幅，不要多格拼版。
```

禁用元素：明星脸、夸张暴乱、血腥、水印、文字横幅、多格拼版。

质检重点：人数范围 8 到 12；所有人是成年人；人群压力强但仍是现实小区楼道。
````

- [ ] **Step 3: Validate prompt count and prompt consistency**

```bash
test "$(rg -c '^### @' projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md)" -eq 8
rg -n '保存文件：`assets/门缝递药关键帧.png`' projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md
rg -n "不要未成年人感" projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md
rg -n "质检重点：" projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md
git diff --check -- projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md
```

Expected: the `test` command exits `0`; each `rg` command prints at least one matching line; `git diff --check` exits `0`.

- [ ] **Step 4: Cross-check pilot prompt names against pilot index**

```bash
comm -3 \
  <(rg '^### @' projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md | sed 's/^### //' | sort) \
  <(awk -F'|' '$2 ~ /@/ && $2 !~ /@素材名/ {gsub(/^ +| +$/, "", $2); print $2}' projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md | sort)
```

Expected: no output.

- [ ] **Step 5: Commit**

```bash
git add projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md
git commit -m "docs: add pilot v2 image prompts"
```

Expected: commit succeeds and includes only the v2 pilot prompt file.

---

### Task 4: Pilot Quality Check

**Files:**
- Create: `projects/frozen-rebirth-revenge/reviews/asset-prompt-system-quality-check.md`

**Interfaces:**
- Consumes: Task 1 guide, Task 2 pilot briefs/index, Task 3 pilot prompts.
- Produces: A review artifact recording the checks needed before the pilot is merged into formal asset files.

- [ ] **Step 1: Run the failing presence check**

```bash
test -f projects/frozen-rebirth-revenge/reviews/asset-prompt-system-quality-check.md
```

Expected: FAIL with exit code `1`, because the quality check file does not exist yet.

- [ ] **Step 2: Create the quality check file**

Use `apply_patch` to create `projects/frozen-rebirth-revenge/reviews/asset-prompt-system-quality-check.md` with this exact content:

````markdown
# 素材提示词系统 v2 试点质检

范围：

- `assets/asset-prompt-guidelines.md`
- `assets/asset-briefs-v2-pilot.md`
- `assets/_asset-index-v2-pilot.md`
- `assets/image-generation-prompts-v2-pilot.md`

本质检只覆盖 v2 试点文档，不代表 8 张图片已经生成或 approved。

## 文档完整性

| 检查项 | 结果 | 证据 |
| --- | --- | --- |
| 项目内规范已存在 | 通过 | `assets/asset-prompt-guidelines.md` |
| v2 brief 试点共 8 个素材 | 通过 | `rg -c '^### @' assets/asset-briefs-v2-pilot.md` 返回 8 |
| v2 prompt 试点共 8 个素材 | 通过 | `rg -c '^### @' assets/image-generation-prompts-v2-pilot.md` 返回 8 |
| v2 索引共 8 个素材 | 通过 | `awk -F'|' '$2 ~ /@/ && $2 !~ /@素材名/ {count++} END {print count+0}' assets/_asset-index-v2-pilot.md` 返回 8 |
| prompt 名称与索引名称一致 | 通过 | `comm -3` 对比无输出 |

## 剧本素材闸门

| 检查项 | 结果 | 证据 |
| --- | --- | --- |
| 素材从场次动作推导 | 通过 | 门缝递药、围门群体、停电楼道气候均来自第一集场次 09 到 12 |
| 人物连续性字段存在 | 通过 | `摄影语言`、`连续性约束`、`质检重点` 已写入 v2 brief |
| 场景图保持单空间 | 通过 | 楼道、门内、气候图均禁止拼版、箭头、说明文字 |
| 道具避免品牌和可读界面 | 通过 | 门铃摄像头提示词禁止品牌、界面文字和可读聊天记录 |
| 成年吸睛女性安全约束存在 | 通过 | 沈知夏、沈晚均含成年、非裸露、非未成年人感约束 |
| 天气影响落到可见结果 | 通过 | 停电楼道气候图写明白气、脚印、结霜、反光和应急灯 |

## 合并前人工检查

- 用户确认是否保留 `@沈知夏设定图`、`@沈晚设定图`、`@暴雪楼道场景图`、`@公寓防盗门内侧场景图`、`@门铃摄像头道具图` 的同名覆盖生成策略。
- 用户确认新素材 `@停电楼道气候图`、`@门缝递药关键帧`、`@暴雪围门群体图` 是否进入正式 `_asset-index.md`。
- 用户目检生成图后，才能把素材状态从 `planned` 或 `generated` 改成 `approved`。

## 可复跑验证命令

```bash
test "$(rg -c '^### @' projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md)" -eq 8
test "$(rg -c '^### @' projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md)" -eq 8
test "$(awk -F'|' '$2 ~ /@/ && $2 !~ /@素材名/ {count++} END {print count+0}' projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md)" -eq 8
comm -3 \
  <(rg '^### @' projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md | sed 's/^### //' | sort) \
  <(awk -F'|' '$2 ~ /@/ && $2 !~ /@素材名/ {gsub(/^ +| +$/, "", $2); print $2}' projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md | sort)
git diff --check -- \
  projects/frozen-rebirth-revenge/assets/asset-prompt-guidelines.md \
  projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md \
  projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md \
  projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md \
  projects/frozen-rebirth-revenge/reviews/asset-prompt-system-quality-check.md
```
````

- [ ] **Step 3: Validate the quality check file**

```bash
rg -n "本质检只覆盖 v2 试点文档" projects/frozen-rebirth-revenge/reviews/asset-prompt-system-quality-check.md
rg -n "用户目检生成图后" projects/frozen-rebirth-revenge/reviews/asset-prompt-system-quality-check.md
git diff --check -- projects/frozen-rebirth-revenge/reviews/asset-prompt-system-quality-check.md
```

Expected: both `rg` commands print one matching line, and `git diff --check` exits `0`.

- [ ] **Step 4: Run whole-pilot validation**

```bash
test "$(rg -c '^### @' projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md)" -eq 8
test "$(rg -c '^### @' projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md)" -eq 8
test "$(awk -F'|' '$2 ~ /@/ && $2 !~ /@素材名/ {count++} END {print count+0}' projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md)" -eq 8
comm -3 \
  <(rg '^### @' projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md | sed 's/^### //' | sort) \
  <(awk -F'|' '$2 ~ /@/ && $2 !~ /@素材名/ {gsub(/^ +| +$/, "", $2); print $2}' projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md | sort)
git diff --check -- \
  projects/frozen-rebirth-revenge/assets/asset-prompt-guidelines.md \
  projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md \
  projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md \
  projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md \
  projects/frozen-rebirth-revenge/reviews/asset-prompt-system-quality-check.md
```

Expected: all three `test` commands exit `0`; `comm -3` prints no output; `git diff --check` exits `0`.

- [ ] **Step 5: Commit**

```bash
git add projects/frozen-rebirth-revenge/reviews/asset-prompt-system-quality-check.md
git commit -m "docs: add asset prompt pilot quality check"
```

Expected: commit succeeds and includes only the quality check file.

---

## Final Verification

Run these commands after all tasks complete:

```bash
git status --short
test -f projects/frozen-rebirth-revenge/assets/asset-prompt-guidelines.md
test -f projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md
test -f projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md
test -f projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md
test -f projects/frozen-rebirth-revenge/reviews/asset-prompt-system-quality-check.md
test "$(rg -c '^### @' projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md)" -eq 8
test "$(rg -c '^### @' projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md)" -eq 8
test "$(awk -F'|' '$2 ~ /@/ && $2 !~ /@素材名/ {count++} END {print count+0}' projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md)" -eq 8
comm -3 \
  <(rg '^### @' projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md | sed 's/^### //' | sort) \
  <(awk -F'|' '$2 ~ /@/ && $2 !~ /@素材名/ {gsub(/^ +| +$/, "", $2); print $2}' projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md | sort)
git diff --check -- \
  projects/frozen-rebirth-revenge/assets/asset-prompt-guidelines.md \
  projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md \
  projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md \
  projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md \
  projects/frozen-rebirth-revenge/reviews/asset-prompt-system-quality-check.md
```

Expected:

- `git status --short` may still show the pre-existing modified files `AGENTS.md`, `asset-briefs.md`, `image-generation-prompts.md`, and `_asset-index.md`; this plan does not require cleaning them.
- All `test -f` commands exit `0`.
- All count checks exit `0`.
- `comm -3` prints no output.
- `git diff --check` exits `0`.
