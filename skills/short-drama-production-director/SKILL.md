---
name: short-drama-production-director
description: "Use when developing short-drama projects from kickoff, source story adaptation, episode scripts, script review, visual asset planning, character and scene image generation, storyboards, or AI-video handoff."
---

# 短剧生产导演

## 核心原则

先把故事和生产链路拆清楚，再写剧本、做人物/场景资产、分镜和视频交接。不要从一句话 prompt 直接跳到生图或视频提示词。

本 skill 适用于通用短剧项目；项目专属事实只从当前工程的 bible、正典稿、脚本、资产索引和用户确认中读取。

## 阶段路由

| 任务 | 读取 |
| --- | --- |
| 项目开工、定位、目标观众、验证包 | `references/01-project-kickoff.md` |
| 从小说、故事梗概、真实案例或大纲拆成单集 | `references/02-story-to-episode.md` |
| 写单集剧本、场次、对白和动作 | `references/03-script-writing.md` |
| 审查剧本、改稿、判断能否进入视觉阶段 | `references/04-script-review.md` |
| 规划人物、场景、道具和视觉入口清单 | `references/05-visual-asset-briefs.md` |
| 生成人物设定图、场景图、资产包和索引 | `references/06-image-generation-assets.md` |
| 分镜表、导演节拍、参考素材引用 | `references/07-storyboard.md` |
| AI 视频生成交接、Seedance/Sora/其他模型提示词包 | `references/08-video-handoff.md`；Seedance 任务同时使用 `seedance2-video-director` |

## 固定流程

```text
开工定位
-> 故事母本/正典事实整理
-> 单集选择点和视觉钩子
-> 剧本
-> 剧本审查通过
-> 视觉入口清单
-> 人物/场景/道具 brief
-> 生图和素材包
-> 用户确认可用资产
-> 分镜表
-> 视频生成交接
```

## 硬闸门

- 未确定故事事实、主选择、人物关系和单集目标前，不写正式剧本。
- 剧本未审查通过前，不生成正式人物图、场景图、关键帧、分镜或视频提示词。
- 生图前必须有 brief；生成后必须有索引状态；用户确认前不得把素材当成最终参考。
- 图片素材统一进入项目的 `assets/` 根目录，不按人物、场景、集数分多层级目录保存最终交接图。
- 分镜和视频交接引用素材使用 `@中文素材名`；实际文件名必须去掉 `@` 后完全一致，例如 `@许行幼年设定图` -> `assets/许行幼年设定图.png`。
- 单张场景图只对应一个场景或一个空间功能；不要把多个场景、动线标记、分镜框、箭头和说明文字拼进给视频模型使用的参考图。
- 分镜里的“导演节拍”是一个视频段内部的时间线，不等于全部独立生成任务。
- 视频延长只在同一空间、同一动作链、同一镜头方向需要承接上一段末帧时使用；换时间、换空间、主观闪回或情绪断裂时独立生成。

## 交付最小字段

每个正式生产条目至少包含：

```text
段落/分镜编号：
目标时长：
引用素材：
画面目标：
动作节拍：
镜头与运动：
声音/对白：
视频提示词：
禁止项：
```

`引用素材` 必须逐项写清：

```text
@中文素材名，path: assets/中文素材名.png，role: reference_image，用途：...
```

## 常见错误

| 错误 | 修正 |
| --- | --- |
| 从故事一句话直接写视频提示词 | 先过单集结构、剧本、视觉 brief 和分镜 |
| 剧本阶段顺手生图 | 等剧本审查通过，再进视觉资产阶段 |
| `@素材名` 和文件名不一致 | 用中文可读名一一对应，交付前跑路径检查 |
| 把多格设定图直接喂给视频模型 | 另存单场景、无标记线的参考图 |
| 每个段落都写视频延长 | 只在真实画面连续时写延长 |
| 分镜表和视频任务混淆 | 分镜可细，正式生成任务要按可控段落合并 |
