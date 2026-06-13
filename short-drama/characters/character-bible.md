# 角色视觉总控

## 总原则

角色视觉必须服务《第九条路》的现实亲情和轻科幻人生分支气质。人物应像普通二线城市家庭和学校、职场中真实存在的人，不做明星化、玄幻化或爽文主角化。

## 角色 ID 总表

| character_id | 角色 | 年龄/阶段 | 管理方式 | 规格文件 |
| --- | --- | --- | --- | --- |
| `xu-xing-child` | 许行 | 幼年，小学阶段 | 主角年龄版本 | `short-drama/characters/xu-xing.md` |
| `xu-xing-youth` | 许行 | 青年，高中到初入职场 | 主角年龄版本 | `short-drama/characters/xu-xing.md` |
| `xu-xing-adult` | 许行 | 壮年，结婚到成为父亲 | 主角年龄版本 | `short-drama/characters/xu-xing.md` |
| `xu-mingyuan-ep01` | 许明远 | 第一集，父亲 | 每集配角 | `short-drama/characters/episode-rosters/01-glass-crack.md` |
| `lin-an-ep01` | 林安 | 第一集，母亲 | 每集配角 | `short-drama/characters/episode-rosters/01-glass-crack.md` |
| `teaching-director-ep01` | 教导主任 | 第一集，学校角色 | 每集配角 | `short-drama/characters/episode-rosters/01-glass-crack.md` |

## 通用视觉风格

- 现实主义短剧角色照，接近日常生活质感。
- 自然光或朴素室内光，不做广告大片感。
- 表情克制，优先表现压力、犹豫、疲惫、稳定和承担。
- 服装普通、可负担、符合年龄和生活场景。
- 背景可干净简化，但不能变成纯概念海报或玄幻背景。

## 通用禁忌

- 不做明星脸、网红脸、精英霸总脸。
- 不做玄幻、赛博、系统爽文、命定感视觉。
- 不用夸张妆造或过度精修皮肤。
- 不让父母显得完美、伟岸或牺牲感过强。
- 不让许行看起来像天才、救世主或超能力者。

## 生图前检查

生成任何角色照前，必须确认：

1. `character_id` 已存在。
2. 年龄版本或集数版本已明确。
3. 对应规格文件已读取。
4. `_asset-index.md` 中没有可复用的 `approved` 资产。
5. 本次生成不是分镜、视频提示词或关键帧生成。
