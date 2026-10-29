# 剪映运行与跨项目复用

实际制作本集时才读取；收集资料阶段不触碰剪映或正在运行的导出。复用现有工具，不改业务仓库依赖或剪映全局配置。

## 定位本机入口

- 从当前可用技能清单定位 jianying-editor 与 short-drama-edit，读取各自 SKILL.md 的安装约定。不硬编码作者电脑的盘符或用户名。
- 优先使用剪辑工具已有的独立 Python 环境；确认解释器及依赖可用，不往业务项目或全局 Python 中直接装依赖。
- ffmpeg / ffprobe：从当前 PATH 或已配置工具路径定位。
- 本流程：用户级 .agents/skills/drama-jianying-pipeline，或本项目同名 Skill。
- 将实际工具路径、剪映版本和草稿目录记录在本项目制作记录中，不回写进可分享的 Skill。

缺工具时说明缺项和影响，经用户同意后补齐；不要自动下载、修改全局配置或假装已连接。继续已授权的素材清单和剪辑准备。

进程内设置 JY_SKILL_ROOT，将其 scripts 加入 sys.path，再从 jy_wrapper 导入 JyProject 和 draft。在已验证的 jianying-editor 安装中，pyJianYingDraft 是其 vendor 模块，不先导入 wrapper 就直接 import 会找不到。按工具库 rules/setup.md 和实际接口初始化。

最低预检：Python与wrapper可用；ffmpeg/ffprobe可用；素材可读、输出可写；真实草稿目录、剪映版本/窗口、当前增强/导出状态可确定。从剪映当前设置发现真实草稿目录，不把示例路径当作当前路径。

## 工程安全

新草稿名含剧名、集数、版本，先检查不存在再创建。JyProject 的 overwrite=False 不保证安全：已验证的 wrapper 版本在加载失败时仍可能强制重建。只对新目录或明确工作副本调用构造器，保留原工程和引用素材。

正常路线是生成可复现时间线，导入/打开剪映，实际确认轨道和转场。新版不接受第三方明文稿时，不反复写坏文件或修改 cipher/账号/授权元数据；走当前可用的官方界面导入素材、字幕并构建新副本。仅有兼容草稿而尚未打开时明确记录，不声称完成原生工程验收。

使用电脑控制前读 computer-use 技能及当前工具文档，不复用旧窗口/坐标，不通过底层注入绕过权限。用户 Esc/停止后遵守工具停止要求；保存草稿或排队不构成恢复控制的授权。

## 转场接口示例（按已安装版本核对）

读 jianying-editor 的 rules/effects.md 及实际源码；用现有枚举或 asset_search，不猜 ID。2026-10-30 验证的 vendor 方法是：
~~~
VideoSegment.add_transition(transition_type, *, duration=None)
~~~
转场挂在前一段，整数时长单位为微秒，也接受 "0.20s"；已有转场不能重复添加。该版本含 draft.TransitionType.叠化；先核对当前安装接口，再套用示例。

**先给 VideoSegment 加转场，再将该段加入 ScriptFile。** 该版本 ScriptFile.add_segment 只在加入轨道时收集关联素材；通过 add_media_safe 入轨后才加转场，会有片段引用却没有 materials.transitions 条目，保存成功也不会证明效果完整。需要转场的段按下面顺序构造，不套用先 add_media_safe 再改段的顺序：
~~~python
# source_path、target_range、source_range 和 main_track 来自本集真实剪辑单。
previous_segment = draft.VideoSegment(
    source_path, target_range, source_timerange=source_range
)
previous_segment.add_transition(draft.TransitionType.叠化, duration="0.20s")
assert previous_segment.transition is not None
project.script.add_segment(previous_segment, main_track)
~~~
后续镜头另按剪辑单加入同轨；最后一段不挂向后转场。保存后核对 materials.transitions 中的实际条目、时长和前一段 extra_material_refs 中的对应引用，不能只检查内存对象非空。这仍不证明实际可见、余量和同步，须检查剪映时间线与导出。

验证时该 wrapper 的 add_transition_simple 先构造 Transition 对象后传给上述方法，与 vendor 所需类型不一致；本流程避免此快捷方法，直接用已核对的段级接口。升级后重新核对，不推广成所有版本故障。失败不能静默跳过或只留下勾选记录。

## 导出与恢复

- 自动导出入口按实际版本验证；不凭 export_video/auto_exporter 返回成功就交付。
- 用户选4K＋一键超清时，在剪映界面核对组合及补分辨率/补帧状态；普通4K编码或 ffmpeg 放大不是该功能。
- 登录、会员、额外付费额度由用户处理受影响项；保留设置，继续独立工作，不自动购买或关闭增强。
- 增强/导出运行中先观察真实状态，不反复点击导出、按Esc取消、强制退出、关闭增强、杀进程或重启来提速。真实失败先保留证据，再处理具体失败项；重跑前确认同一任务未在执行。
- CURRENT_TASK.md 写明：等待资料／剪辑中／工程已打开／增强排队／导出中／已导出待验收／已交付。队列中、点击按钮和草稿存在都不是完成。
- 用户让旧集保持现状时，以新要求为准，不从历史继续点重启旧修复。

## 基础技能与依赖

short-drama-edit 可用区间、镜序、声音和验收指导可复用。调用其CLI前核对真实契约；直拼 render 不会自动实现本流程所有剪映后期。没有工具所需的上游ID/文件时不伪造，按本项目真实清单完成剪映时间线。

其它电脑未安装两个基础技能时，本包仍可指导资料确认和制作决策，但不能据此声称能控制剪映。先定位可用官方操作，或经用户同意补齐依赖；保留下一步，不静默换其它编辑器。
