# 场景资产导航

本目录管理《第九条路》短剧阶段的场景视觉规格。后续生成场景设定图、关键帧、分镜和视频提示词时，必须先读取 `short-drama/AGENTS.md` 和 `short-drama/visual-asset-workflow.md`。

## 文件说明

- `scene-bible.md`：场景视觉总控，定义场景 ID、资产类型、版式和禁忌。
- `generation-briefs/`：每集场景设定图生成规格卡。
- `../assets/scenes/_asset-index.md`：已规划和已生成场景视觉资产的索引。
- 最终交接图片统一放在 `../assets/` 根目录，使用中文素材文件名。

## 使用顺序

```text
读 short-drama/AGENTS.md
-> 读 short-drama/visual-asset-workflow.md
-> 读 scene-bible.md
-> 读对应脚本
-> 读对应视觉入口清单
-> 读场景生成 brief
-> 查 assets/scenes/_asset-index.md
-> 默认生成或复用 scene_sheet
-> 保存/复制到 short-drama/assets/中文素材名.png
-> 需要时再补充单张 establishing shot 或 keyframe
```
