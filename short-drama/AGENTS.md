# short-drama/AGENTS.md

## 适用范围

本目录用于《第九条路》的短剧改编、人物设定图、角色照、场景设定图、场景图、关键帧、分镜、AI 视频提示词和后续投放素材管理。

凡是处理 `short-drama/` 下的角色、视觉资产或 image2 生图任务，必须遵守本文件。根目录 `AGENTS.md` 仍然是上级规则；若冲突，按根规则和小说正典账本优先。

## 生图前强制读取顺序

任何人物设定图、角色照、场景设定图、场景图、关键帧或视频提示词生成前，必须先读取：

1. `short-drama/visual-asset-workflow.md`
2. `short-drama/adaptation-control.md`
3. 对应资产总控：
   - 人物：`short-drama/characters/character-bible.md`
   - 场景：`short-drama/scenes/scene-bible.md`
4. 对应规格文件或生成 brief：
   - 人物：角色规格、集数出场表、`short-drama/characters/generation-briefs/`
   - 场景：`short-drama/scenes/generation-briefs/`
5. 对应资产索引：
   - 人物：`short-drama/assets/characters/_asset-index.md`
   - 场景：`short-drama/assets/scenes/_asset-index.md`
6. 对应脚本和视觉入口清单

不得只凭聊天上下文、临时描述或单个脚本直接生成人物设定图、角色照或场景设定图。

## 统一资产闸门

- 所有视觉资产必须先有 brief，再生图。
- 所有视觉资产必须先查 `_asset-index.md`，已有 `approved` 资产时不重复生成，除非用户明确要求重做或迭代。
- 生成后只能把状态更新为 `generated`，等待用户确认后才能改成 `approved`。
- `generated` 资产不能作为后续一致性参考；只有 `approved` 资产可以进入分镜、关键帧和视频提示词。
- 资产文件必须保存到 `short-drama/assets/` 下，不能只保留在默认生成目录。

## 角色 ID 规则

- 主角许行按年龄版本管理，不按集数重新定义：
  - `xu-xing-child`
  - `xu-xing-youth`
  - `xu-xing-adult`
- 每集配角按集管理，格式为 `<role-slug>-epXX`，例如：
  - `xu-mingyuan-ep01`
  - `lin-an-ep01`
  - `teaching-director-ep01`
- 人物设定图、角色照生成和引用必须使用角色 ID，不使用“爸爸”“妈妈”“主任”等临时称呼作为资产 ID。

## 人物设定图生成规则

- 生图默认使用 image2 / 内置 `image_gen`。
- 生图前必须检查 `short-drama/assets/characters/_asset-index.md`。已有 `approved` 图时，不重复生成。
- 每次生成前必须先写或确认角色规格，不直接从一句话描述生成。
- 角色视觉资产默认优先生成人物设定图，而不是单张半身照片。
- 人物设定图必须尽量包含：正面、侧面、背面三视图；六种面部表情；服装/道具拆解区；配色条；三个剪影姿势；一个小型世界观缩略图。
- 人物设定图应服务短剧一致性，避免明星脸、玄幻感、系统爽文感、过度精英化或夸张网感。
- 单张角色照只能作为补充素材，不作为锁定人物各形态的主资产，除非用户明确要求只生成照片。
- 设定图中不要依赖可读文字传递关键信息；标签和说明以 Markdown 资产索引和规格卡为准。
- 生成后必须保存到 `short-drama/assets/characters/` 下对应目录，并更新 `_asset-index.md`。
- 未经用户确认，不生成透明底；如需透明底，先使用 image2 纯色抠图背景，再本地去背景。

## 场景设定图生成规则

- 生图默认使用 image2 / 内置 `image_gen`。
- 生图前必须检查 `short-drama/assets/scenes/_asset-index.md`。已有 `approved` 图时，不重复生成。
- 每次生成前必须先写或确认场景规格，不直接从一句话描述生成。
- 场景视觉资产默认优先生场景设定图，而不是单张氛围图。
- 场景设定图必须尽量包含：主视角、反向视角、平面关系或动线示意、关键道具区、光线/色调条、三个可拍动作点、禁用元素说明。
- 场景设定图应服务短剧拍摄和后续分镜，必须能看清人物站位、出入口、危险点和道具位置。
- 单张场景氛围图只能作为补充素材，不作为锁定空间关系的主资产，除非用户明确要求只生成氛围图。
- 生成后必须保存到 `short-drama/assets/scenes/` 下对应目录，并更新 `_asset-index.md`。

## 目录约定

```text
short-drama/
  characters/
    character-bible.md
    xu-xing.md
    episode-rosters/
      01-glass-crack.md
  assets/
    characters/
      _asset-index.md
      xu-xing/
        child/
        youth/
        adult/
      ep01-glass-crack/
        xu-mingyuan/
        lin-an/
        teaching-director/
    scenes/
      _asset-index.md
      ep01-glass-crack/
  scenes/
    scene-bible.md
    generation-briefs/
      01-glass-crack-scene-sheets.md
```

## 资产状态

人物和场景 `_asset-index.md` 中的 `status` 只能使用：

- `planned`：已规划，尚未生成。
- `generated`：已生成，待人工确认。
- `approved`：可作为后续一致性参考。
- `rejected`：废弃，不再引用。
- `superseded`：被新版本替代。

只有 `approved` 资产可以作为后续同角色或同场景一致性参考。

## 禁止事项

- 不跳过角色母表直接生图。
- 不用同一个角色 ID 表示不同年龄段许行。
- 不把第一集配角设定图复用到明显不同年龄或阶段，除非规格表明确允许。
- 不用“学校”“家里”这类模糊场景 ID 直接生图。
- 不把单张场景氛围图当作空间设定图。
- 不在人物设定图阶段生成分镜表、视频提示词或 AI 视频。
- 不把未来分支视觉化为系统 UI、弹窗、任务奖励或命定特效。
