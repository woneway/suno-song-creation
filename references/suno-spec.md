# Suno 平台规格速查(截至 2026-07,重点 v5.5)

> 调研日期 2026-07-03,来源:官方 Release Notes/帮助中心 + 近 6 个月社区实测交叉验证。
> 标注:【官方】= suno.com/help.suno.com 原文;【共识】= 多个独立近期来源一致;【不确定】= 来源单一或冲突。
> **平台迭代极快:行为不符时以当场实测为准,并回写更新本文件。**

## 1. 版本与字符上限

| 版本 | 发布 | 定位 |
|---|---|---|
| v4.5-all | 2025-10 | 免费档专用 |
| v5 | 2025-09 | 录音室级音质、12-stem |
| **v5.5(现旗舰)** | **2026-03-26** | Voices / Custom Models;Pro($10)/Premier($30) 专用 |

Custom 模式上限(v4.5/v5/v5.5,与订阅档位无关)【共识】:

| 字段 | 上限 | 质量甜点 |
|---|---|---|
| Lyrics | 5,000 字符 | **约 3,000 字符(40–60 行)**——超过后明显赶进度、跳段 |
| Styles | 约 1,000 字符 | **15–30 个词 / 4–7 个描述符**;前置词权重更高,写满互相打架 |
| Song Title | 100 字符 | — |

- 单次生成最长 **8 分钟**(V4.5/V5 官方确认;v5.5 同,推断),Extend 可续【官方+推断】
- 额度:约 5 credits/首,一次出 2 首 ≈10;Pro 2,500/月、Premier 10,000/月,用尽后每天补 50;月度额度不结转【官方】

## 2. 结构标签(Meta Tags)

官方无正式标签文档,以下为社区逆向共识【共识】:

- **段落类(遵循度最高)**:[Intro] [Verse]/[Verse 1] [Pre-Chorus] [Chorus] [Post-Chorus] [Bridge] [Breakdown] [Build-Up] [Drop] [Hook] [Interlude] [Outro] [Break]
- **演唱类(中-高)**:[Male Vocal] [Female Vocal] [Duet] [Choir] [Harmonies] [Rap] [Spoken Word] [Whisper] [Scream] [Ad-lib] [Humming] [Backing Vocals]
- **乐器/音效(中等,看流派匹配)**:[Instrumental] [Guitar Solo] [Piano Solo] 等;[Sound Effect: ...] 能被理解但执行随机【不确定】(v5.5 官方推荐:音效用 Sounds 模式单独生成再进 Studio 叠)
- **控制类**:[End](实测有效,防拖尾)[Fade Out] [Silence] [Crescendo] [Key Change](后几个不稳定)

**机制要点**:
1. 标签是**概率性引导非硬约束**;同文本 [Chorus] 再现时尝试复用旋律。
2. **参数化标签是最强控制手段**:`[Verse 1: whispered vocals, acoustic guitar only]`(冒号后修饰词,v4.5+ 遵循良好);也支持 `[Bridge | Guitar Solo]` 竖线并联。
3. 编号([Verse 1]/[Verse 2])帮模型"各主歌不同旋律、副歌重复"。
4. 标签**只放 Lyrics 栏**;放 Styles 栏会被当风格词误读。大小写无关。
5. 拼写错误的标签会被当歌词唱出来;无 [Outro]/[End] 结尾易突兀或拖尾。

## 3. Styles 栏:数值遵循度与词类排序

| 指令 | 实际遵循度【共识】 |
|---|---|
| BPM 数值 | **近似引导,非节拍锁**(配速度形容词双保险) |
| Key(A minor 等) | 提高概率、不保证 |
| 具体和弦进行 | **基本不可控**;指定 key 是更有效替代 |
| 拍号(3/4、6/8) | **不条件化生成模型**(Studio 的拍号仅编辑网格);用 waltz/swaying feel 等风格词驱动 |

词类有效性排序:①流派/子流派(权重最高且**顺序敏感**,主流派放最前)②人声描述(最可控维度之一)③配器(建议非保证,流派内乐器命中率高)④情绪词(1–2 个够,堆多稀释)⑤制作/年代词(有效);**无效**:艺人名(被过滤)、混音工程术语(sidechain 等被忽略)。

**Exclude Styles**(Pro/Premier;Advanced Options 内)【官方+共识】:
- 专用负向字段,远比在 Styles 里写 "no drums" 可靠;但仍是引导非禁令。
- **≤5 项最干净**,15 项会让模型困惑、产出稀薄。
- V4.5+ 起 Styles 栏内否定句("no drums")也开始生效(旧"忽略否定"结论仅 V4 前成立)。
- **纯音乐三层封锁**:Styles `instrumental, no vocals` + Lyrics `[Instrumental]` + Exclude `no voice, no singing, no chanting`。

## 4. 三滑块

官方口径【官方】:Weirdness(Safe→Chaos,**50%=正常预期**);Style Influence(贴合 Styles 输入的程度);Audio Influence(仅在使用音频素材——上传/Voice/Persona/Cover 时出现)。

社区推荐区间【共识】:

| 滑块 | 区间 | 要点 |
|---|---|---|
| Weirdness | 40–60% 通用;商业曲 0–20;实验 60–80 | **"81% 悬崖"**:以上进入碎片化 glitch 输出 |
| Style Influence | 50–70% 默认;Styles 精准且精简时 70–85 | 高贴合必须配精简 prompt;100%+臃肿 Styles=糊成一团 |
| Audio Influence | Cover/参考音频 40–70;**Voice/Persona 高保真 70–85** | 调高换相似度,代价闷声/artifacts;**"借音色不借唱法"场景可反其道用 30–40**(本仓库实测) |

法则:滑块控制变异不是精确锁;一次只动一个对比。

## 5. Personas / Voices

- 2026-03 起 Create 面板的 Voices 按钮整合了旧 Personas;从歌曲提取:歌曲 ⋯ 菜单 → Remix → Voice(Create a Voice),选取人声段、命名保存【官方;本仓库 2026-06 实测可用】。
- **Style Persona 默认公开(注意关掉);v5.5 真人 Voices 默认私有**【官方】。私人作品建议一律设私有。
- Persona 保留**音色与基础 delivery**(气声/沙哑),不保留具体旋律型与断句;跨大流派套用不稳定【共识】。
- Voices 需 v5.5 模型才生效;Custom Models(上传 ≥6 首训练,最多 3 个)为 v5.5 独占【官方】。

## 6. 编辑功能矩阵(含订阅门槛)

| 功能 | 能力 | 门槛/限制 |
|---|---|---|
| Extend | 从选定时间点续写 | 每次是新生成耗额度;多次续写风格漂移 |
| Get Whole Song | 把原曲+全部 Extend 拼成整曲 | 在最后一段 Extend 上执行;拼缝偶有小瑕疵 |
| Replace Section | 框选中段改词/重生成,其余保留 | **Pro/Premier**;首次很少完美,预算 2–5 次(中文修多音字利器) |
| Song Editor | 波形选区:重生成/改词/移动/删除/加段/淡入出 | 免费档受限,付费全量 |
| Crop | 裁首尾 | 中段删除用 Editor 的 Remove |
| Cover | 保旋律歌词,重塑风格/演唱 | 付费;大变换用 Cover 不用 Remaster |
| Remaster | 结构演绎不变,细化音质(三档强度) | 升级旧歌音质、提升咬字清晰 |
| Stems 分轨 | 三分法(2026-06):Split from Mix(2 stems,全档位)/ Auto Split(12 类,Pro+)/ Advanced Split(~100 种乐器,**仅 Premier**) | 相似频段串音;对自生成歌远好于第三方工具 |
| Studio | 生成式 DAW:多轨、stem 变体、Warp、Remove FX(去混响得干声)、导出 audio/MIDI | **仅 Premier**;拍号仅编辑层 |

## 7. 中文歌曲已知问题与对策【共识】

1. **多音字**唱错/跳字(v5 改善未根除):①同音字替换法(首选:"重"→"崇",代价字幕非原字);②拼音标注法 `重(chong)逢` 大部分有效、小概率不识别;整句拼音无效。([Pronunciation:] 标签传闻未获官方确认【不确定】)
2. **咬字含糊**:v5 普通话仍偶发"大舌头";修法:Replace Section 只重做那一两句;歌词顶端加 `[This is a Mandarin song]` 有助稳定发音。
3. **中英混排**:直接写进 Lyrics,模型自动切换,无需声明。
4. **儿化音**:无可靠实测【不确定】,建议改写规避。
5. **Styles 用英文写更稳**(歌词中文、风格英文是中文社区主流打法);英文语义理解更成熟。
6. 艺人名无效且被过滤 → 用六维拆解法转译(见 production-advanced 第五节)。

## 8. 商用与导出(2026-07 态势)

| 档位 | 所有权与商用 |
|---|---|
| Free | **歌曲归 Suno**,仅个人非商用;**订阅后不追溯**获得免费期歌曲商用权 |
| Pro/Premier | 订阅期内制作的歌归你,可商用,Suno 不抽成 |
| 任何档位 | **自己写的歌词永远归自己** |

- 平台"所有权"≠可登记的版权:纯 AI 生成缺乏人类作者性难登记;加入人类创作(原创歌词/编排/真人录音)增强主张。订阅不含侵权赔偿兜底。
- 导出:MP3 全档位;**WAV 仅付费档**;分轨见 §6。(Warner 协议曾预告收紧下载政策,截至 2026-06 核验为"已宣布未落地"【不确定】)
- 诉讼态势:Warner 已和解合作(2025-11,未来推授权模型);UMG/Sony 诉讼未决(简易判决推迟至 2027-01);GEMA(德)判决 2026-07-31。**实操**:付费期内创作+自写歌词+留过程记录;不要用 Cover 翻唱商业歌曲。
