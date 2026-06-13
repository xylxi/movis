# short-drama/AGENTS.md

## 适用范围

本目录用于《第九条路》的短剧改编、角色照、场景图、关键帧、分镜、AI 视频提示词和后续投放素材管理。

凡是处理 `short-drama/` 下的角色、视觉资产或 image2 生图任务，必须遵守本文件。根目录 `AGENTS.md` 仍然是上级规则；若冲突，按根规则和小说正典账本优先。

## 生图前强制读取顺序

任何角色照、场景图、关键帧或视频提示词生成前，必须先读取：

1. `short-drama/adaptation-control.md`
2. `short-drama/characters/character-bible.md`
3. 对应角色规格文件
4. 对应集数 `short-drama/characters/episode-rosters/`
5. `short-drama/assets/characters/_asset-index.md`
6. 对应脚本和视觉入口清单

不得只凭聊天上下文、临时描述或单个脚本直接生成角色照。

## 角色 ID 规则

- 主角许行按年龄版本管理，不按集数重新定义：
  - `xu-xing-child`
  - `xu-xing-youth`
  - `xu-xing-adult`
- 每集配角按集管理，格式为 `<role-slug>-epXX`，例如：
  - `xu-mingyuan-ep01`
  - `lin-an-ep01`
  - `teaching-director-ep01`
- 角色照生成和引用必须使用角色 ID，不使用“爸爸”“妈妈”“主任”等临时称呼作为资产 ID。

## 角色照生成规则

- 生图默认使用 image2 / 内置 `image_gen`。
- 生图前必须检查 `_asset-index.md`。已有 `approved` 图时，不重复生成。
- 每次生成前必须先写或确认角色规格，不直接从一句话描述生成。
- 角色照应服务短剧一致性，避免明星脸、玄幻感、系统爽文感、过度精英化或夸张网感。
- 生成后必须保存到 `short-drama/assets/characters/` 下对应目录，并更新 `_asset-index.md`。
- 未经用户确认，不生成透明底；如需透明底，先使用 image2 纯色抠图背景，再本地去背景。

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
```

## 资产状态

`_asset-index.md` 中的 `status` 只能使用：

- `planned`：已规划，尚未生成。
- `generated`：已生成，待人工确认。
- `approved`：可作为后续一致性参考。
- `rejected`：废弃，不再引用。
- `superseded`：被新版本替代。

只有 `approved` 资产可以作为后续同角色一致性参考。

## 禁止事项

- 不跳过角色母表直接生图。
- 不用同一个角色 ID 表示不同年龄段许行。
- 不把第一集配角照片复用到明显不同年龄或阶段，除非规格表明确允许。
- 不在角色照阶段生成分镜表、视频提示词或 AI 视频。
- 不把未来分支视觉化为系统 UI、弹窗、任务奖励或命定特效。
