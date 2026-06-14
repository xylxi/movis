# 角色视觉资产索引

本索引用于记录已规划、已生成和已批准的角色视觉资产。后续任何人物设定图或角色照生成前，必须先检查本文件。

默认优先资产类型为 `character_sheet`。单张 `portrait` 只能作为补充素材，不用于单独锁定人物完整形态。

## 状态说明

- `planned`：已规划，尚未生成。
- `generated`：已生成，待人工确认。
- `approved`：可作为后续一致性参考。
- `rejected`：废弃，不再引用。
- `superseded`：被新版本替代。

## 索引表

| asset_id | character_id | asset_type | episode | age_stage | file | status | note |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `xu-xing-child-sheet-v01` | `xu-xing-child` | `character_sheet` | `ep01` | `child` | `short-drama/assets/characters/xu-xing/child/xu-xing-child-sheet-v01.png` | `approved` | 用户确认采用；第一集许行幼年人物设定图，可作为后续一致性参考 |
| `xu-mingyuan-ep01-sheet-v01` | `xu-mingyuan-ep01` | `character_sheet` | `ep01` | `adult` | `short-drama/assets/characters/ep01-glass-crack/xu-mingyuan/xu-mingyuan-ep01-sheet-v01.png` | `rejected` | 用户反馈显老、疲惫，不符合阳光普通家庭调性 |
| `lin-an-ep01-sheet-v01` | `lin-an-ep01` | `character_sheet` | `ep01` | `adult` | `short-drama/assets/characters/ep01-glass-crack/lin-an/lin-an-ep01-sheet-v01.png` | `rejected` | 用户反馈显老、疲惫，且图中英文标签过多，不符合阳光普通家庭调性 |
| `xu-mingyuan-ep01-sheet-v02` | `xu-mingyuan-ep01` | `character_sheet` | `ep01` | `adult` | `short-drama/assets/characters/ep01-glass-crack/xu-mingyuan/xu-mingyuan-ep01-sheet-v02.png` | `superseded` | 用户反馈服装材质暗淡、整体偏保守，由 v03 迭代替代 |
| `lin-an-ep01-sheet-v02` | `lin-an-ep01` | `character_sheet` | `ep01` | `adult` | `short-drama/assets/characters/ep01-glass-crack/lin-an/lin-an-ep01-sheet-v02.png` | `superseded` | 用户反馈服装材质暗淡、整体偏保守，由 v03 迭代替代 |
| `xu-mingyuan-ep01-sheet-v03` | `xu-mingyuan-ep01` | `character_sheet` | `ep01` | `adult` | `short-drama/assets/characters/ep01-glass-crack/xu-mingyuan/xu-mingyuan-ep01-sheet-v03.png` | `approved` | 用户确认采用；父亲人物设定图 v03，可作为后续一致性参考 |
| `lin-an-ep01-sheet-v03` | `lin-an-ep01` | `character_sheet` | `ep01` | `adult` | `short-drama/assets/characters/ep01-glass-crack/lin-an/lin-an-ep01-sheet-v03.png` | `approved` | 用户确认采用；母亲人物设定图 v03，可作为后续一致性参考 |
| `teaching-director-ep01-sheet-v01` | `teaching-director-ep01` | `character_sheet` | `ep01` | `adult` | `short-drama/assets/characters/ep01-glass-crack/teaching-director/teaching-director-ep01-sheet-v01.png` | `approved` | 用户确认采用；第一集教导主任人物设定图，可作为后续一致性参考 |

## 更新规则

生成角色视觉资产后，必须将对应行从 `planned` 改为 `generated`，并确认 `file` 路径真实存在。

用户确认采用后，才能将 `status` 改为 `approved`。
