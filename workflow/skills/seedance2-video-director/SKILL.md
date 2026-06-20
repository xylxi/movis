---
name: seedance2-video-director
description: "为即梦 Seedance 2.0 创建、改写、审查和排查高质量视频提示词。适用于文生视频、图片参考、视频参考、视频延长、视频编辑、视频融合、音频参考、音乐卡点、一镜到底和多素材参考等 Seedance 2.0 工作流。"
---

# Seedance 2.0 视频导演

## 使用场景

当用户需要为即梦 Seedance 2.0 生成、改写、压缩、扩展、审查或排查视频提示词时使用本 skill。目标不是套用内容模板，而是把需求转成可执行的导演约束：素材用途、时间线、镜头、动作因果、声音节奏和禁止项。

## 信息来源优先级

1. 平台硬限制和入口规则优先，以 `references/seedance2-platform-guide.md` 为准。
2. 质量检查和失败定位优先，以 `references/seedance2-quality-checks.md` 为准。
3. 导演方法论按需读取 `references/director-system/` 中对应层级。
4. 外部示例只作为能力用法背景，不作为运行时依赖；本 skill 以本地 `references/` 为准。

## 硬规则摘要

- 图片最多 9 个，视频最多 3 个，音频最多 3 个，混合文件最多 12 个。
- 生成时长为 4-15 秒；视频延长时，时长写新增部分，不写原视频总时长。
- 引用素材必须用 `@素材名` 指定用途，例如首帧、尾帧、主体、风格、动作参考、声音参考。
- 视频延长必须写清楚“将 @视频名 继续延长”。
- 不支持上传写实可识别人脸素材；不要设计依赖真实可识别人脸素材的流程。
- 不依赖模型生成可靠可读文字；字幕、海报字、包装字和屏幕字必须视为高风险。

## 执行流程

1. 先确认任务类型：新生成、改写、审查、排查，或视频延长。
2. 读取 `references/seedance2-platform-guide.md`，确认素材数量、时长、入口和 @素材名 规则。
3. 如用户要求审查、排查或最终交付，读取 `references/seedance2-quality-checks.md`。
4. 按需求只读取必要的导演层级文件，不一次性加载全部参考。
5. 将提示词编译为 Seedance 可执行文本：明确素材、时间段、镜头、动作、声音和禁止项。
6. 输出前检查是否违反平台硬限制，是否有不可验证的形容词堆叠，是否缺少动作因果。

## 10 层按需读取规则

- 需求不清或目标摇摆：读取 `references/director-system/01-intent.md`。
- 画面主体、空间关系或时间线混乱：读取 `references/director-system/02-visual-skeleton.md`。
- 光线、材质、质感或可信度不足：读取 `references/director-system/03-light-material.md`。
- 景别、镜头距离或构图需要锁定：读取 `references/director-system/04-camera-distance.md`。
- 运镜、节奏、一镜到底或运动真实感需要设计：读取 `references/director-system/05-camera-movement.md`。
- 动作像随机表演、缺少触发和结果：读取 `references/director-system/06-action-causality.md`。
- 多人物、多物件或多素材容易串位：读取 `references/director-system/07-multi-subject-locking.md`。
- 只有产品或商业展示任务才读取 `references/director-system/08-product-believability.md`。
- 需要把分析稿整理成最终提示词：读取 `references/director-system/09-prompt-compilation.md`。
- 需要复盘失败、改版或形成下一轮参数：读取 `references/director-system/10-workflow-review.md`。

## 输出格式

默认输出以下结构，除非用户指定其他格式：

```text
Seedance 入口：
素材清单：
生成时长：
提示词：
禁止项：
检查结果：
```

审查或排查任务使用：

```text
问题分层：
证据：
修改方向：
改写后提示词：
复检清单：
```

## 读取文件规则

- 每次正式写 Seedance 提示词前读取平台指南。
- 每次交付最终版、审查他人提示词或排查失败结果前读取质量检查。
- 导演系统文件按问题读取；不要把 10 层全部当固定模板输出。
- 产品可信层只服务产品、商业展示和品牌资产任务；非产品视频跳过。
