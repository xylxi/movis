---
name: ninth-road-project
description: "Use when working inside /Users/ruir/Documents/movies on 第九条路 novel canon, short-drama adaptation, visual assets, storyboards, Seedance prompts, AI video generation, Douyin validation, or project workflow decisions."
---

# 第九条路项目工作流

## 核心原则

本 skill 是《第九条路》项目的工作流入口。不要把聊天上下文当作正典；先读项目文件，再写小说、改短剧、做视觉资产、分镜或视频提示词。

项目根目录固定为 `/Users/ruir/Documents/movies`。所有文件路径在交付文档里优先使用项目相对路径，方便用户定位和复查。

## 任务分流

| 用户任务 | 必读文件 |
| --- | --- |
| 小说开章、改稿、润色 | `AGENTS.md`、`README.md`、`novel/series-bible.md`、`novel/family-dossier.md`、`novel/writing-style-guide.md`、`novel/character-continuity.md`、`novel/chapter-ledger.md`、`novel/foreshadowing-ledger.md`、`novel/story-control-checklist.md`、对应章节卡和导航图 |
| 短剧改编、脚本、审稿 | `AGENTS.md`、`short-drama/AGENTS.md`、`short-drama/adaptation-control.md`、`novel/chapter-ledger.md`、对应正典草稿、对应短剧脚本或入口清单 |
| 人物设定图、角色照 | `short-drama/AGENTS.md`、`short-drama/visual-asset-workflow.md`、`short-drama/adaptation-control.md`、`short-drama/characters/character-bible.md`、对应角色规格或 brief、`short-drama/assets/characters/_asset-index.md`、对应脚本和视觉入口清单 |
| 场景设定图、场景图 | `short-drama/AGENTS.md`、`short-drama/visual-asset-workflow.md`、`short-drama/adaptation-control.md`、`short-drama/scenes/scene-bible.md`、对应场景 brief、`short-drama/assets/scenes/_asset-index.md`、对应脚本和视觉入口清单 |
| 分镜、关键帧、Seedance 提示词 | `short-drama/AGENTS.md`、`short-drama/visual-asset-workflow.md`、`short-drama/adaptation-control.md`、对应脚本、storyboard、video-generation handoff、角色/场景资产索引；同时使用 `seedance2-video-director` |
| 抖音发布、数据复盘 | `workflow/production-pipeline.md`、已有研究记录、发布数据记录；复盘结论必须能回写到短剧策略或小说改编策略 |

## 小说正典规则

- 后续创作只以 `novel/chapter-ledger.md` 标记的正典草稿路径为事实来源。
- 旧稿、导航图、审稿意见和临时想法只能作为参考，不能自动继承为事实。
- 新章或大改前，先确认章节功能、现实事件、主选择、代价、家庭压力数字、父母行动和章尾动作。
- 推荐新方向或补信息时，使用项目规定字段：`推荐动作`、`依据证据`、`解决的问题`、`预期收益`、`潜在风险`、`置信度`、`是否允许自动执行`。
- 大改不要直接覆盖已有正文；优先新建临时迭代稿，除非用户明确要求覆盖。
- 定稿后按 `novel/story-control-checklist.md` 反写人物连续性账本、章节账本和伏笔账本。

## 短剧改编规则

- 短剧验证目标是测试“现实亲情 + 轻科幻人生分支”，不是系统爽文、鸡娃对抗或家庭伦理强冲突。
- 每集围绕一个主选择；未来分支只呈现代价，不给答案，不提供考试、彩票、股票、绩效等具体利益信息。
- 父母行动顺序是：确认伤害、承担责任、复盘问题。少写教育金句，多写动作和处理顺序。
- 进入 image2、关键帧、分镜或视频提示词前，脚本中的场次、人物状态、道具、数字锚点和家庭场景必须相对稳定。
- 不提前铺开全九集脚本；当前短剧验证包以第一章、第六章、第九章为主，第三章保留为备选。

## 视觉资产闸门

- 任何人物、角色照、场景、关键帧或视频提示词生成前，先查对应 `_asset-index.md`。
- 已有 `approved` 资产时不得重复生成同一对象同一版本，除非用户明确要求重做或迭代。
- 新生成资产只能登记为 `generated`，等待用户确认后才能改成 `approved`。
- `generated` 不能作为后续一致性参考；只有 `approved` 能进入分镜、关键帧和视频提示词。
- 人物默认优先生成人物设定图 `character_sheet`，不是单张头像。
- 场景默认优先生成功能明确的 `scene_sheet`，不是单张氛围图。
- 未来分支不能视觉化为系统 UI、弹窗、任务面板、奖励结算、玄幻命定或爽文特效。

## Seedance 交接规则

- 编写 Seedance 相关提示词时，必须使用个人通用 skill：`seedance2-video-director`。本项目 skill 只补充《第九条路》的正典、资产和交接规则。
- Handoff 中每个素材必须有 `@素材名`、项目相对路径、用途和角色。正式上传给即梦的材料文件名应与 `@素材名` 的可见名称一致，例如 `@许行幼年设定图` 对应 `short-drama/assets/许行幼年设定图.png`。
- 如果素材有内部索引路径和交接副本，交接文档必须能追溯到 `approved` 源资产；不要让用户只看到无法定位的临时文件名。
- 单张场景图只服务一个场景或一个空间功能。不要把多个场景拼进一张图，也不要把标记线、分镜框、编号箭头或解释文字放进给 Seedance 参考的场景图。
- 视频延长只在真实需要承接上一段视频最后画面、动作或镜头时使用。若只是同一集的下一个独立分镜，不写延长。
- 使用视频延长时，提示词必须写清“将 @上一段视频 继续延长”，并说明承接的是上一段的哪个末帧、动作、人物位置或镜头方向。
- 分镜正式生成清单是给即梦生产视频的条目；段内导演节拍只用于理解该段内部时间线，不能把所有节拍都当成独立视频生成任务。
- 每段提示词检查：素材引用是否准确、时长是否合理、动作因果是否可执行、是否误用延长、是否只有 `approved` 资产进入参考。

## 输出检查

交付前执行这些检查：

- 是否读取了本任务对应的必读文件，而不是只凭聊天上下文。
- 是否使用项目相对路径指向材料、脚本、分镜和资产。
- 是否保留用户已有改动，没有回滚无关文件。
- 是否把正典事实、候选想法、资产状态和视频生产任务分清。
- 是否把 DeepSeek 审稿意见、Seedance 能力说明和项目正典规则分层处理。

## 常见错误

| 错误 | 修正 |
| --- | --- |
| 把项目规则复制到多个地方 | 只在 skill 写入口和读档顺序，具体规则回到项目文件 |
| 直接从聊天描述写正文或生图 | 先读正典、brief 和索引 |
| 把 `generated` 当作稳定参考 | 等用户确认后改为 `approved` |
| 看到连续分镜就全部写视频延长 | 只有画面真实承接才写延长 |
| `@素材名` 和文件名不一致 | 交接文件名与 `@素材名` 可见名称保持一致 |
| 把多场景拼成一张参考图 | 一张场景图只服务一个场景或空间功能 |
