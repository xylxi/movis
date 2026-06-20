# 短剧视觉资产工作流

## 目标

本文件统一管理《第九条路》短剧阶段的人物、场景、道具、关键帧、分镜和视频提示词的推进顺序。

核心原则：任何 image2 / `image_gen` 生图都不能只凭一句话 prompt 直接执行，必须先有规格、索引和状态闸门。

## 固定顺序

```text
脚本审查通过
-> 视觉入口清单
-> 资产规格 brief
-> 资产索引检查
-> image2 / image_gen 生图
-> 保存到 assets 根目录，使用中文素材文件名
-> 更新索引为 generated
-> 人工确认
-> 更新索引为 approved
-> 进入下一阶段
```

## 资产状态闸门

`planned`：只允许写 brief，不允许作为后续参考。  
`generated`：已生成，等待人工确认，不允许作为稳定一致性参考。  
`approved`：人工确认通过，可作为后续分镜、关键帧、视频提示词和同角色/同场景一致性参考。  
`rejected`：废弃，不再引用。  
`superseded`：被新版本替代，不再作为默认参考。

禁止把 `generated` 资产当作 `approved` 使用。

## 素材命名和目录

最终交接图片素材统一保存到 `short-drama/assets/` 根目录，不按人物、场景或集数拆多层目录。

分镜、视频交接和实际文件名必须一致：

```text
@中文素材名 -> short-drama/assets/中文素材名.png
```

示例：

- `@许行幼年设定图` -> `short-drama/assets/许行幼年设定图.png`
- `@学校办公室场景图` -> `short-drama/assets/学校办公室场景图.png`
- `@当晚饭桌场景图` -> `short-drama/assets/当晚饭桌场景图.png`

内部 `asset_id`、`character_id`、`scene_id` 和版本号写入索引，不进入交接文件名。

## 人物资产规则

默认主资产类型：`character_sheet`。

人物设定图必须尽量包含：

- 正面、侧面、背面三视图。
- 六种面部表情。
- 服装/道具拆解区。
- 配色条。
- 三个剪影姿势。
- 小型世界观缩略图。

单张 `portrait` 只能作为补充素材，不用于单独锁定人物完整形态，除非用户明确要求只生成照片。

## 场景资产规则

默认主资产类型：`scene_sheet`。

场景设定图必须尽量包含：

- 主视角 establishing view。
- 反向视角 reverse view。
- 平面关系或动线示意。
- 关键道具区。
- 光线/色调条。
- 三个可拍动作点。
- 安全边界或禁用元素说明。

场景图不能只是氛围图。它要能回答：人物站在哪里、从哪里进出、关键道具在哪里、镜头可以拍哪些动作。

## 生图 Prompt 合同

正式 prompt 必须包含：

```text
Use case:
Asset type:
Primary request:
Sheet layout:
Subject or scene details:
Style/medium:
Lighting/mood:
Color palette:
Constraints:
Avoid:
```

中文正典信息写在 brief 和索引里；图中可出现少量布局标签，但不得依赖图中文字传递关键正典。

## 禁止事项

- 不跳过 brief 和资产索引直接生图。
- 不用聊天上下文替代项目文件。
- 不把 `generated` 当成 `approved`。
- 不在人物或场景设定阶段顺手生成分镜表、视频提示词或 AI 视频。
- 不把未来分支画成系统 UI、弹窗、任务奖励、数值面板或玄幻命定视觉。
- 不为追求冲突感添加正典外狗血事件、夸张伤害或不符合家庭现实质感的元素。

## 每次生图前检查

- 已读取 `short-drama/AGENTS.md`。
- 已读取本文件。
- 已读取对应总控文件、脚本和视觉入口清单。
- 已读取对应资产索引。
- 没有可复用的 `approved` 资产。
- 已确认本次只生成当前阶段资产，不跨阶段生成。

## 每次生图后检查

- 图片已保存到工作区 `short-drama/assets/` 根目录，文件名与 `@中文素材名` 一致。
- 索引中的 `file` 路径真实存在。
- 索引状态已从 `planned` 更新为 `generated`。
- 未把资产状态直接改成 `approved`。
- 已目检确认资产类型正确，不是把场景图误生成人物照，或把人物设定图误生成单张头像。
