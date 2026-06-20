# 素材提示词系统 v2 试点质检

范围：

- `assets/asset-prompt-guidelines.md`
- `assets/asset-briefs-v2-pilot.md`
- `assets/_asset-index-v2-pilot.md`
- `assets/image-generation-prompts-v2-pilot.md`

本质检只覆盖 v2 试点文档，不代表 8 张图片已经生成或 approved。

## 文档完整性

| 检查项 | 结果 | 证据 |
| --- | --- | --- |
| 项目内规范已存在 | 通过 | `assets/asset-prompt-guidelines.md` |
| v2 brief 试点共 8 个素材 | 通过 | `rg -c '^### @' assets/asset-briefs-v2-pilot.md` 返回 8 |
| v2 prompt 试点共 8 个素材 | 通过 | `rg -c '^### @' assets/image-generation-prompts-v2-pilot.md` 返回 8 |
| v2 索引共 8 个素材 | 通过 | `awk -F'|' '$2 ~ /@/ && $2 !~ /@素材名/ {count++} END {print count+0}' assets/_asset-index-v2-pilot.md` 返回 8 |
| prompt 名称与索引名称一致 | 通过 | `comm -3` 对比无输出 |

## 剧本素材闸门

| 检查项 | 结果 | 证据 |
| --- | --- | --- |
| 素材从场次动作推导 | 通过 | 门缝递药、围门群体、停电楼道气候均来自第一集场次 09 到 12 |
| 人物连续性字段存在 | 通过 | `摄影语言`、`连续性约束`、`质检重点` 已写入 v2 brief |
| 场景图保持单空间 | 通过 | 楼道、门内、气候图均禁止拼版、箭头、说明文字 |
| 道具避免品牌和可读界面 | 通过 | 门铃摄像头提示词禁止品牌、界面文字和可读聊天记录 |
| 成年吸睛女性安全约束存在 | 通过 | 沈知夏、沈晚均含成年、非裸露、非未成年人感约束 |
| 天气影响落到可见结果 | 通过 | 停电楼道气候图写明白气、脚印、结霜、反光和应急灯 |

## 合并前人工检查

- 用户确认是否保留 `@沈知夏设定图`、`@沈晚设定图`、`@暴雪楼道场景图`、`@公寓防盗门内侧场景图`、`@门铃摄像头道具图` 的同名覆盖生成策略。
- 用户确认新素材 `@停电楼道气候图`、`@门缝递药关键帧`、`@暴雪围门群体图` 是否进入正式 `_asset-index.md`。
- 用户目检生成图后，才能把素材状态从 `planned` 或 `generated` 改成 `approved`。

## 可复跑验证命令

```bash
test "$(rg -c '^### @' projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md)" -eq 8
test "$(rg -c '^### @' projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md)" -eq 8
test "$(awk -F'|' '$2 ~ /@/ && $2 !~ /@素材名/ {count++} END {print count+0}' projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md)" -eq 8
comm -3 \
  <(rg '^### @' projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md | sed 's/^### //' | sort) \
  <(awk -F'|' '$2 ~ /@/ && $2 !~ /@素材名/ {gsub(/^ +| +$/, "", $2); print $2}' projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md | sort)
git diff --check -- \
  projects/frozen-rebirth-revenge/assets/asset-prompt-guidelines.md \
  projects/frozen-rebirth-revenge/assets/asset-briefs-v2-pilot.md \
  projects/frozen-rebirth-revenge/assets/_asset-index-v2-pilot.md \
  projects/frozen-rebirth-revenge/assets/image-generation-prompts-v2-pilot.md \
  projects/frozen-rebirth-revenge/reviews/asset-prompt-system-quality-check.md
```
