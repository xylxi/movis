# 场景视觉资产索引

本索引用于记录已规划、已生成和已批准的场景视觉资产。后续任何场景设定图、场景图或关键帧生成前，必须先检查本文件。

默认优先资产类型为 `scene_sheet`。单张 `establishing_shot` 或 `keyframe` 只能作为补充素材，不用于单独锁定场景完整空间关系。

## 状态说明

- `planned`：已规划，尚未生成。
- `generated`：已生成，待人工确认。
- `approved`：可作为后续一致性参考。
- `rejected`：废弃，不再引用。
- `superseded`：被新版本替代。

## 索引表

| asset_id | scene_id | asset_type | episode | file | status | note |
| --- | --- | --- | --- | --- | --- | --- |
| `ep01-school-playground-building-sheet-v01` | `ep01-school-playground-building` | `scene_sheet` | `ep01` | `short-drama/assets/操场教学楼场景图.png` | `approved` | 用户确认采用；操场、教学楼、公告栏和学生围观距离设定图；分镜/交接素材名 `@操场教学楼场景图` |
| `ep01-broken-window-risk-sheet-v01` | `ep01-broken-window-risk` | `scene_sheet` | `ep01` | `short-drama/assets/三楼破窗场景图.png` | `generated` | 基于场景规格重新生成的单画面参考图；替代原多格破窗设定拼版直接上传；需用户目检确认后再改为 `approved` |
| `ep01-school-office-clinic-sheet-v01` | `ep01-school-office-clinic` | `scene_sheet` | `ep01` | `short-drama/assets/学校办公室场景图.png` | `approved` | 用户确认采用；学校办公室、门边座位和医务处理空间；分镜/交接素材名 `@学校办公室场景图` |
| `ep01-family-dining-review-sheet-v01` | `ep01-family-dining-review` | `scene_sheet` | `ep01` | `short-drama/assets/当晚饭桌场景图.png` | `approved` | 用户确认采用；当晚饭桌复盘、维修单和蓝色记录本；分镜/交接素材名 `@当晚饭桌场景图` |
| `ep01-next-morning-bill-sheet-v01` | `ep01-next-morning-bill` | `scene_sheet` | `ep01` | `short-drama/assets/次日水费单场景图.png` | `approved` | 用户确认采用；次日早饭、水费单、粥碗和文具盒动作；分镜/交接素材名 `@次日水费单场景图` |

## 更新规则

生成场景视觉资产后，必须将对应行从 `planned` 改为 `generated`，并确认 `file` 路径真实存在。

用户确认采用后，才能将 `status` 改为 `approved`。

正式交接场景图统一为单画面参考图，不使用多格拼版、动线标记、色卡、红叉示例、黄虚线或圈选标记。
