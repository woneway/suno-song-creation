# suno-song-creation

用 [Suno](https://suno.com) 进行专业级中文歌曲创作的 [Claude Code](https://claude.com/claude-code) skill——一套从主题到发布的通用唱作方法论。

## 是什么

这不是一份 prompt 合集，而是一条完整的创作流水线：

- **主题 → 歌词**：主题访谈、叙事视角、意象系统、韵辙与押韵策略
- **曲风 profile 驱动**：曲式、句长结构、hook 机制、情绪弧线都没有跨曲风默认值，由 12 个曲风 profile（民谣/流行/摇滚/R&B/说唱/中国风/电子/爵士/蓝调/bossa/city-pop…）提供唯一默认来源
- **配置与生成**：风格串六维组装、Exclude 逐歌设计、滑块参数、段落标签写法
- **迭代修正**：分层控制模型——症状定位到词/标签/风格串/Exclude/Persona 哪一层，不瞎改
- **去AI味与查重**：装置指纹 9 维查重门禁，杜绝"每首歌都是上一首的换皮"
- **发布合规**：封面规格、歌曲介绍、AI 标注与商用权清单

核心理念：**Suno 是概率执行者，不是 DAW**——锁死方向（词+标签+Exclude）→ 多抽 → 按预定义成败句挑 → 局部修，而不是整首重抽；**词是唯一完全受控的层**，时间花在词上，额度省在生成上。

## 安装

```bash
# 项目级（仅当前项目可用）
git clone https://github.com/woneway/suno-song-creation.git .claude/skills/suno-song-creation

# 或用户级（所有项目可用）
git clone https://github.com/woneway/suno-song-creation.git ~/.claude/skills/suno-song-creation
```

安装后在 Claude Code 中直接说"想写一首关于……的歌"即可触发，或显式调用 `/suno-song-creation`。

## 文件结构

| 文件 | 内容 |
|------|------|
| `SKILL.md` | 主流程：核心认知、分层控制模型、平台机制事实、创作八步流程 |
| `references/genre-profiles.md` | 12 曲风 profile：身份要素/曲式/词法/弧线/常见跑偏/Suno 要点 |
| `references/proven-templates.md` | 案例库与操作手册：实测风格串、装置库、装置指纹存档、Exclude/滑块、听审清单、发布合规 |
| `references/lyrics-advanced.md` | 歌词进阶：大师技法、押韵进阶、词曲咬合、交稿 13 项 checklist |
| `references/music-theory.md` | 音乐基础：十三辙、倒字、曲式、BPM/和声、配器、人声术语 |
| `references/production-advanced.md` | 制作进阶：旋律文字化、编曲 build 曲线、发布级后期链、参考曲六维拆解 |
| `references/suno-spec.md` | Suno 平台规格：字段上限、标签清单、滑块机制、编辑功能门槛、中文已知问题 |

## 案例 Demo

`demo/` 收录了用本 skill 创作的四首完整案例，每首含全量配置（`配置.md`：歌词、风格串、参数、踩坑记录、装置指纹）、成品音频与封面：

| 歌名 | 曲风 | 一句话 |
|------|------|--------|
| 《归燕》 | 民谣（指弹吉他） | 写给过世的奶奶，全曲用燕子做隐喻，结尾一句「奶奶 你看」揭底 |
| 《正午的月亮》 | 民谣（校园声景） | 写给异国恋——12 小时时差，国内的正午是她的深夜 |
| 《主场欢送会》 | Boom bap 说唱 | 中国男篮主场首负日本，密集内韵的黑色幽默冷讽 |
| 《长椅宽出一半》 | Vintage 爵士 ballad（AABA） | 86 岁老人与坐了六十年的长椅——人少了一半，椅子就"宽"了 |

🎵 **这四首歌都能听**：打开**汽水音乐**，搜索 **归燕 / 正午的月亮 / 主场欢送会 / 长椅宽出一半**，即可试听完整版。

## 时效声明

Suno 版本、订阅权益、平台政策迭代极快；所有"实测/规格"类结论以文内标注日期为准。使用时若发现行为不符，以当场实测为准。
