# 第一集角色照生成规格卡：玻璃裂开的那一秒

## 边界

本文件只定义第一集角色标准照规格，不生成角色图、场景图、关键帧图、分镜表、视频提示词或 image2 prompt 成品。

后续进入 image2 / `image_gen` 生图前，必须再次读取：

1. `short-drama/AGENTS.md`
2. `short-drama/adaptation-control.md`
3. `short-drama/characters/character-bible.md`
4. `short-drama/characters/xu-xing.md`
5. `short-drama/characters/episode-rosters/01-glass-crack.md`
6. `short-drama/assets/characters/_asset-index.md`
7. `short-drama/scripts/01-glass-crack-script.md`
8. `short-drama/visual-handoff/01-glass-crack-entry-list.md`

## 统一生成风格

- 画面类型：现实主义短剧角色标准照。
- 构图：半身或中近景，人物正面或轻微三分之二侧身，背景干净朴素。
- 光线：自然光或朴素室内光，不做广告大片感。
- 质感：普通二线城市家庭和学校生活质感。
- 表情：克制，优先表现紧张、疲惫、稳定、担心和承担。
- 禁止：明星脸、网红脸、玄幻感、系统爽文感、精英霸总感、过度磨皮、夸张妆造。

## 生成批次

| asset_id | character_id | 角色 | 资产路径 | 状态 |
| --- | --- | --- | --- | --- |
| `xu-xing-child-v01` | `xu-xing-child` | 许行 | `short-drama/assets/characters/xu-xing/child/xu-xing-child-v01.png` | `planned` |
| `xu-mingyuan-ep01-v01` | `xu-mingyuan-ep01` | 许明远 | `short-drama/assets/characters/ep01-glass-crack/xu-mingyuan/xu-mingyuan-ep01-v01.png` | `planned` |
| `lin-an-ep01-v01` | `lin-an-ep01` | 林安 | `short-drama/assets/characters/ep01-glass-crack/lin-an/lin-an-ep01-v01.png` | `planned` |
| `teaching-director-ep01-v01` | `teaching-director-ep01` | 教导主任 | `short-drama/assets/characters/ep01-glass-crack/teaching-director/teaching-director-ep01-v01.png` | `planned` |

## 角色规格

### xu-xing-child

- 角色：许行，8 岁左右，小学阶段。
- 本集状态：刚踢碎三楼玻璃，在逃走、沉默和喊人承认之间选择。
- 外貌方向：普通小学男孩，脸部稚气明显，眼神容易受惊。
- 气质：内收、敏感、观察感强，紧张时会低头或抿嘴。
- 服装：普通小学运动校服或日常校服，干净但不昂贵，不潮牌化。
- 表情：紧张、害怕、犹豫，但没有戏剧化崩溃。
- 可见细节：手背可以有很轻的红痕；不需要夸张伤口。
- 背景建议：干净的学校墙面或浅色背景，不直接拍事故现场。
- 禁止：小天才感、童模广告感、超能力少年感、英雄化。
- 一致性备注：后续第二章如继续使用幼年许行，应以此版本为基础。

### xu-mingyuan-ep01

- 角色：许明远，第一集父亲。
- 本集状态：普通职场父亲，被工作消息牵扯，赶到学校后先确认伤害、承担检查责任，再带孩子复盘。
- 外貌方向：普通中年职场员工，疲惫但不颓废。
- 气质：压着焦虑，行动有顺序，不像人生导师。
- 服装：普通衬衫、夹克或通勤外套，符合小公司项目/运营岗位。
- 表情：担心、克制、疲惫，眼神先看事实再看孩子。
- 可见细节：可带黑色手机、普通工牌或磨损公文包；不要同时堆太多道具。
- 背景建议：学校办公室外或朴素室内背景。
- 禁止：成功人士感、伟岸父亲感、隐忍英雄感、精英管理者气质。
- 一致性备注：本角色照只锁第一集父亲状态，不自动代表后续所有年龄阶段。

### lin-an-ep01

- 角色：林安，第一集母亲。
- 本集状态：全职母亲，电话里先确认主任和孩子伤势，处理维修单和水费单。
- 外貌方向：普通家庭母亲，有生活操持感，但不是苦情形象。
- 气质：稳定、着急但能把问题拆开处理。
- 服装：简单家常外套、针织衫或围裙外搭，朴素、干净、可负担。
- 表情：担心、疲惫、克制，带一点生活被打断后的紧绷。
- 可见细节：可带帆布包或折起的纸单；不需要夸张家务道具。
- 背景建议：学校办公室边、家里饭桌边或干净朴素背景。
- 禁止：纯牺牲者、苦情母亲、鸡娃母亲、过度温柔圣母感。
- 一致性备注：本角色照服务第一集母亲状态，后续空巢或老年阶段需要另行规格。

### teaching-director-ep01

- 角色：教导主任，第一集学校角色。
- 本集状态：抱着作业本经过三楼窗下，被许行喊住后退，手背轻伤，接受道歉。
- 外貌方向：普通学校教导主任，年龄中年偏上，教师身份明确。
- 气质：严肃、被事故惊到，但不是反派。
- 服装：朴素衬衫、针织外套或教师通勤装。
- 表情：惊魂未定、严肃、克制。
- 可见细节：可抱作业本；手背可有小创可贴或轻微红痕。
- 背景建议：学校走廊或办公室背景。
- 禁止：反派化、夸张受伤、威压感过强、喜剧化。
- 一致性备注：本角色为第一集功能角色，不进入长期主角资产。

## 生图前确认清单

- [ ] `_asset-index.md` 中四个 asset 仍为 `planned`，没有可复用的 `approved` 图。
- [ ] 用户已确认本规格卡可以进入 image2 生图。
- [ ] 本批只生成角色标准照，不生成场景图、关键帧、分镜表、视频提示词或视频。
- [ ] 生成后图片必须保存到索引表中对应路径。
- [ ] 生成后将对应 asset 状态从 `planned` 改为 `generated`，等待用户确认后才能改为 `approved`。
