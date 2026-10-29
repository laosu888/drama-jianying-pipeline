# 短剧剪映成片 Skill

把每集已生成的镜头剪成可发布、可续接的短剧成片。**复用制作流程，每部剧独立确认剧情、风格、水印和封面。**

这是给 Codex 使用的工作流 Skill，不是独立视频软件或“一键无人值守”应用。实际制作依赖可用的剪映、媒体工具与电脑控制能力。

## 第一件事：先问清楚，再开剪

新剧先确认正式剧名、集数、水印平台和完整文案、位置与划线范围、风格及交付要求；收到用户确认的本集全部镜头后才开始。水印可选番茄小说、QQ阅读、其它平台或不加，不能自动沿用上一部剧。

- 按实际剧情精剪，保留因果与人物反应，删除重复和无效等待。
- 按动作、声音、时空和情绪逐切点做过渡，避免生硬拼接，也不机械堆转场。
- 原对白优先；按需处理配音、配乐、环境/动作音、小号双语字幕及人物介绍。
- 每部剧一套系列封面母版和真实剧情标题，后续通常只改集数。
- 按确认规格用剪映导出；用户选择4K＋一键超清后，不因排队慢擅自取消或降级。
- 验收实际 MP4、动态衔接、字幕、水印及声音，留下剪辑单和可续接工程。

## 装入项目

下载本仓库 ZIP 并解压，或：

```powershell
git clone https://github.com/laosu888/drama-jianying-pipeline.git
```

将 `skills/drama-jianying-pipeline` 整个文件夹复制到目标项目的 `.agents/skills/` 下，再把根目录的 `短剧剪辑使用说明.md` 复制到目标项目根目录：

```text
目标项目/
  短剧剪辑使用说明.md
  .agents/skills/drama-jianying-pipeline/
    SKILL.md
    LICENSE
    agents/openai.yaml
    assets/项目剪辑设定.md
    references/craft-and-acceptance.md
    references/jianying-runtime.md
```

保留目标项目现有 AGENTS.md 和素材。已有同名 Skill 时先对比，再决定更新，不盲目覆盖。项目级与用户级同名副本不合并，测试时明确读取目标项目内的版本。

## 开始使用

在 Codex 打开目标项目，发送：

```text
阅读本项目《短剧剪辑使用说明.md》，使用本项目的 $drama-jianying-pipeline。
这是新剧，先向我确认正式剧名、水印、风格和交付要求。
等我提供并确认本集全部镜头后再开始剪辑。
```

后续集确认沿用设定，提供本集全部镜头 ZIP 或目录即可。完整资料单、交付与目录说明见 [短剧剪辑使用说明](短剧剪辑使用说明.md)。

## 制作环境与边界

- Windows 上安装可运行的剪映专业版，并具有可用的登录/会员状态（仅在所选功能需要时）。
- 可用的 ffmpeg / ffprobe、Python 剪辑环境，以及支持当前剪映版本的工程构建/界面操作方式。
- 优先复用已安装的 [jianying-editor](https://github.com/isYangs/jianying-editor-skill)；short-drama-edit 是可复用的剪辑辅助 Skill。它们未随本仓库捆绑，工具缺失时先检查并说明补齐方式，不声称安装本流程就已连接剪映。
- 运行细节、转场素材注册顺序和安全续接见 [剪映运行说明](skills/drama-jianying-pipeline/references/jianying-runtime.md)。示例按已安装版本核对，不保证所有剪映或第三方工具版本兼容。
- 本仓库不包含第三方工具代码、剧集、音乐、字体、账号、凭据或付费服务。付费配音、新云服务上传和对外发布按实际需要取得用户授权。

Skill 格式与项目级发现路径依据 [OpenAI 官方技能文档](https://learn.chatgpt.com/docs/build-skills)。

## 开源许可

本仓库的工作流说明和模板使用 [MIT License](LICENSE)。外部工具及用户素材遵循各自许可。
