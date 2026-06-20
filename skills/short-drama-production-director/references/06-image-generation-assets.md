# 生图与素材包

## 固定流程

```text
brief
-> 检查索引是否已有可用资产
-> 生图
-> 保存到 assets/
-> 更新索引为 generated
-> 人工确认
-> 更新为 approved / final
-> 进入镜头节拍和视频交接
```

## 文件命名

- 最终图片素材统一放在 `assets/` 根目录。
- 文件名使用中文可读名，必须与镜头节拍和交接里的 `@中文素材名` 一致。
- `@中文素材名` 去掉 `@` 后就是文件 stem。

示例：

```text
@暴雪楼道场景图 -> assets/暴雪楼道场景图.png
@沈知夏设定图 -> assets/沈知夏设定图.png
@极寒生存物资图 -> assets/极寒生存物资图.png
```

## 索引字段

```text
asset_id：
@素材名：
type：
file：
status：
source：
note：
```

## 状态

- `planned`：有计划，未生成。
- `generated`：已生成，待确认。
- `approved`：可进入镜头节拍和视频提示词。
- `rejected`：废弃。
- `superseded`：被新版本替代。

旧版本不要混入正式交接包。最终交接只引用 `approved` 或明确标记为最终采用的素材。
