# 角色资产导航

本目录管理《第九条路》短剧阶段的角色视觉规格。后续生成人物设定图、角色照、场景图、关键帧、分镜和视频提示词时，必须先读取 `short-drama/AGENTS.md`。

## 文件说明

- `character-bible.md`：角色视觉总控，定义角色 ID、年龄版本、通用风格和禁忌。
- `xu-xing.md`：主角许行的幼年、青年、壮年三阶段规格。
- `episode-rosters/`：每集出场人物表，只引用角色 ID，不重新发明角色长相。
- `../assets/characters/_asset-index.md`：已规划和已生成角色视觉资产的索引。

## 使用顺序

```text
读 short-drama/AGENTS.md
-> 读 character-bible.md
-> 读具体角色规格
-> 读对应集数出场表
-> 查 _asset-index.md
-> 默认生成或复用人物设定图
-> 需要时再补充单张角色照
```
