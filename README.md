# Movies 剧本工作区

这是剧本开发与视频化生产工作区。正式剧本项目统一放入 `projects/<project-slug>/`，每个项目独立维护 bible、剧本、素材、镜头节拍和视频生成交付。

## 项目入口

| 项目 | slug | 状态 | 入口 |
| --- | --- | --- | --- |
| 极寒重生复仇爽剧 | `frozen-rebirth-revenge` | 当前正式项目 | `projects/frozen-rebirth-revenge/PROJECT.md` |

## 文件导航

- `projects/README.md`：项目隔离规则和项目列表
- `projects/frozen-rebirth-revenge/PROJECT.md`：当前正式项目入口
- `projects/frozen-rebirth-revenge/bible.md`：项目设定总纲
- `projects/frozen-rebirth-revenge/episodes/episode-01-script.md`：第一集正典剧本
- `projects/frozen-rebirth-revenge/assets/`：第一集素材 brief、索引、生图提示词和最终图片素材
- `projects/frozen-rebirth-revenge/storyboards/episode-01-shot-beats.md`：服务 Seedance 2.0 的镜头节拍
- `projects/frozen-rebirth-revenge/video-generation/episode-01-handoff.md`：可直接用于视频生成的交付提示词
- `projects/frozen-rebirth-revenge/reviews/`：质量检查和素材总览

## 工作原则

- 新剧本必须创建独立 `projects/<project-slug>/`，不在仓库根目录堆放项目事实。
- 通用方法写入 skill；项目事实只写入项目目录。
- 素材引用使用中文可读 `@素材名`，并与 `assets/素材名.png` 文件名一致。
- 视频交付以 Seedance 2.0 可执行字段为准，不维护与生成无关的人读分镜副本。
