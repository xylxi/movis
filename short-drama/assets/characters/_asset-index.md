# 角色照资产索引

本索引用于记录已规划、已生成和已批准的角色照。后续任何角色照生成前，必须先检查本文件。

## 状态说明

- `planned`：已规划，尚未生成。
- `generated`：已生成，待人工确认。
- `approved`：可作为后续一致性参考。
- `rejected`：废弃，不再引用。
- `superseded`：被新版本替代。

## 索引表

| asset_id | character_id | episode | age_stage | file | status | note |
| --- | --- | --- | --- | --- | --- | --- |
| `xu-xing-child-v01` | `xu-xing-child` | `ep01` | `child` | `short-drama/assets/characters/xu-xing/child/xu-xing-child-v01.png` | `planned` | 第一章主角幼年标准照 |
| `xu-mingyuan-ep01-v01` | `xu-mingyuan-ep01` | `ep01` | `adult` | `short-drama/assets/characters/ep01-glass-crack/xu-mingyuan/xu-mingyuan-ep01-v01.png` | `planned` | 第一章父亲标准照 |
| `lin-an-ep01-v01` | `lin-an-ep01` | `ep01` | `adult` | `short-drama/assets/characters/ep01-glass-crack/lin-an/lin-an-ep01-v01.png` | `planned` | 第一章母亲标准照 |
| `teaching-director-ep01-v01` | `teaching-director-ep01` | `ep01` | `adult` | `short-drama/assets/characters/ep01-glass-crack/teaching-director/teaching-director-ep01-v01.png` | `planned` | 第一章教导主任标准照 |

## 更新规则

生成角色照后，必须将对应行从 `planned` 改为 `generated`，并确认 `file` 路径真实存在。

用户确认采用后，才能将 `status` 改为 `approved`。
