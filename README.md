# 短剧剪映成片 Skill

把每集已生成的镜头剪成可发布、可续接的短剧成片。**复用制作流程，每部剧独立确认剧情、风格、水印和封面。**

这是给 Codex 使用的工作流 Skill，不是独立视频软件或“一键无人值守”应用。实际制作依赖可用的剪映、媒体工具与电脑控制能力。

## 第一件事：先问清楚，再开剪

新剧先确认正式剧名、集数、水印平台和完整文案、位置与划线范围、风格及交付要求；收到用户确认的本集全部镜头后才开始。水印可选番茄小说、QQ阅读、其它平台或不加，不能自动沿用上一部剧。

- 按实际剧情精剪，保留因果与人物反应，删除重复和无效等待。
- 按动作、声音、时空和情绪逐切点做过渡，避免生硬拼接，也不机械堆转场。
- 原对白优先；按需处理配音、配乐、环境/动作音、小号双语字幕及人物介绍。
- 每集默认生成实际封面JPG、发布标题、副标题与#话题，保存到本集交付/发布物料/，不用再次索要。每部剧独立设计系列母版，同剧后续通常只改集数。
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
    assets/发布文案.md
    references/bgm-sfx-library.md
    references/craft-and-acceptance.md
    references/jianying-runtime.md
    references/publishing-delivery.md
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

## 每集同时交付发布物料

视频之外，每集自动附可上传的系列封面、一条推荐标题、一条简短副标题及通常3–5个相关#话题。文案基于本集最终成片，不把未发生的结果写成已经完成；副标题单列，不强制烧入视频。封面固定本剧人物、片名与版式，不同剧不套同一风格。

本集交付/发布物料/中保存封面JPG、发布文案.md和封面设计说明.md。交付前查看实际图片、核对文案，并在回复给文件路径；不能只给封面提示词或把“MP4已导出”当整套交付齐全。用户明确取消的项目可跳过，工具受阻项单独列明。需要合集时另做去集数的合集封面与合集名、简介，不每集重复生成。

## 制作环境与边界

- Windows 上安装可运行的剪映专业版，并具有可用的登录/会员状态（仅在所选功能需要时）。
- 可用的 ffmpeg / ffprobe、Python 剪辑环境，以及支持当前剪映版本的工程构建/界面操作方式。
- 优先复用已安装的 [jianying-editor](https://github.com/isYangs/jianying-editor-skill)；short-drama-edit 是可复用的剪辑辅助 Skill。它们未随本仓库捆绑，工具缺失时先检查并说明补齐方式，不声称安装本流程就已连接剪映。
- 运行细节、转场素材注册顺序和安全续接见 [剪映运行说明](skills/drama-jianying-pipeline/references/jianying-runtime.md)。示例按已安装版本核对，不保证所有剪映或第三方工具版本兼容。
- 本仓库不包含第三方工具代码、剧集、音乐、字体、账号、凭据或付费服务。付费配音、新云服务上传和对外发布按实际需要取得用户授权。

Skill 格式与项目级发现路径依据 [OpenAI 官方技能文档](https://learn.chatgpt.com/docs/build-skills)。

## 开源许可

本仓库的工作流说明和模板使用 [MIT License](LICENSE)。外部工具及用户素材遵循各自许可。

## 版本

当前版本：**v1.1.0**（见 [CHANGELOG](CHANGELOG.md)）。
- v1.1.0：新增 [BGM与音效库](skills/drama-jianying-pipeline/references/bgm-sfx-library.md)（热门短剧BGM按题材与情绪关键词分类、音效三层架构、0.2秒重音规则、版权来源规则），并加入水印/人物介绍/字卡的精品包装规范；每集必须有BGM和音效。

