# 多剧本项目目录

本目录用于隔离不同剧本项目。正式剧本必须放入 `projects/<project-slug>/`，不要把多个故事混在仓库根目录或公共目录中。

## 项目列表

| 项目 | slug | 状态 | 入口 |
| --- | --- | --- | --- |
| 极寒重生复仇爽剧 | `frozen-rebirth-revenge` | 当前正式项目，按通用剧本规范推进 | `projects/frozen-rebirth-revenge/PROJECT.md` |

## 新项目结构

```text
projects/<project-slug>/          # 单个剧本项目目录，slug 使用小写英文、数字和连字符
├── PROJECT.md                    # 项目入口：定位、状态、正典文件和交付入口
├── bible.md                      # 项目设定总纲：世界观、人物关系、冲突和连续性规则
├── episodes/                     # 单集剧本目录，保存 episode-xx-script.md
├── assets/                       # 素材目录，保存素材 brief、索引、生图提示词和最终图片
├── storyboards/                  # 镜头节拍目录，服务 Seedance 的段内时间线和画面动作
├── video-generation/             # 视频生成交付目录，保存可直接输入模型的 handoff
├── reviews/                      # 审查和复盘目录，保存质量检查、素材总览和问题记录
└── research/                     # 可选研究目录，保存题材、竞品、平台和资料调研
```

## 隔离规则

- 每个剧本只读自己的 `PROJECT.md` 和目录内正典文件。
- 新项目不得引用其他剧本的角色图、场景图、视频片段或素材索引。
- 通用方法写入 skill；项目事实写入项目目录。
- 视频交付文件只保留可供模型执行的字段，不维护并行的人读分镜稿。
