# 案例库与操作手册

> 来源:本仓库《正午的月亮》《归燕》《长椅宽出一半》的完整创作迭代(2026-06/07,Suno v5.5)。
> **定位声明:本文件的风格串与装置全部是"案例",不是默认模板。** 现有案例均为民谣/抒情体裁;跨体裁禁止直接套用——写任何歌之前先读 genre-profiles.md 载入对应曲风 profile。操作手册部分(标签写法/滑块/去AI味/听审/合规)为体裁无关内容。

## 一、案例风格串(全部为民谣/抒情体裁,仅同体裁参考)

### 案例 A:克制深情抒情歌(出处:《正午的月亮》)

适用:克制型情歌、想念、"闷在心里说不出口"。要点:`restrained / never loud / swells then pulls back` 三件套防狂放——**这是克制型歌曲的药,不是通用药**。

```
soft restrained male baritone, intimate and breathy, emotionally expressive but never loud; melancholic mandarin ballad with chinese campus folk influences, nostalgic 校园民谣 feel; warm fingerstyle acoustic guitar as the heart, gentle piano, subtle strings; dynamics rise and fall with feeling, chorus swells then pulls back, fragile whispered bridge, no belting; slow 66 BPM, bittersweet longing, clear tender mandarin
```

### 案例 B:一个声音世界内的两章对比(出处:《归燕》)

适用:歌里有"过去 vs 现在"两个时期的**民谣叙事**。核心原则(平台机制,通用):对比靠配器密度,不靠变速变风格(分开生成再拼会割裂,已验证否决)。

```
nostalgic mandarin folk ballad, slow and unhurried around 64 BPM, natural loose timing that breathes between phrases, never rushed; one warm continuous sound world — first half relaxed and playful with fingerstyle acoustic guitar, light shaker and soft whistling; after the interlude the arrangement strips right down to sparse soft piano, faint strings and voice, hushed and spacious; strong contrast in density between the two halves but the same tempo and the same warm male storyteller voice throughout, intimate and natural like talking to family; clear tender mandarin
```

### 案例 C:专业音乐参数版(实验性,遵循度"参考执行")

在 B 基础上加拍号/调性/和声色彩,把抽卡分布往对的方向推:

```
nostalgic mandarin folk ballad in 6/8 time, gentle lilting lullaby sway, around 64 BPM, key of G major; emotional chinese ballad chord progression; natural loose timing, laid-back behind-the-beat vocal phrasing; ...(其余同案例 B)
```

注:①拍号数字本身不影响生成,起作用的是 `lilting lullaby sway` 这类风格词(见 music-theory 3.1);②Suno 不认级数,和声只能给风格化描述(`rich seventh chords` 类;想精确控和声走 Studio 上传参考音频)。

## 二、Exclude 栏设计法

**核心原则(通用,有教训背书):Exclude 全曲生效,每首歌单独设计,禁止跨歌复制。** 两次翻车实录:①情歌的 `upbeat, energetic` 沿用到民谣,压死欢快上半场;②民谣的防欢池沿用到爵士,`upbeat swing` 把爵士命根子 swing 一起杀死(《长椅宽出一半》v1)。

设计方法:查目标曲风 profile 的「常见跑偏」→ 挑 3–5 项防"这首歌最可能的跑偏方向"。**≤5 项最干净**(社区实测,15 项会让模型困惑)。V4.5+ 起 Styles 栏写否定句("no big drums")也生效,可作补充。

本仓案例池(克制型民谣/抒情场景,仅同类参考):`powerful, belting, soaring vocals, anthemic, epic, loud` / `fast tempo, rushed, driving rhythm` / `tragic, mournful, crying, melodramatic`。爵士场景的反例与正解见 genre-profiles 爵士节 Suno 要点。

## 三、More Options 配置

| 项 | 推荐值 | 说明 |
|------|--------|------|
| Weirdness | 40–50% | 本仓实测经验值(非官方规律):太低偏"乖"、机器味;过高慢歌易跑调 |
| Style Influence | 70–80% | 本仓实测:风格串写了大量行为指令时调高更听话 |
| Audio Influence | 按目标选 | **两种打法**:高保真复刻原声用 70–85;"借音色不借唱法"(本仓场景)反其道用 30–40,唱法被带偏就再降或摘 Persona |
| Vocal Gender | 显式选 | 别依赖风格串里的 male/female 描述 |

滑块值是**起点不是教条**——每首歌按症状微调(见 SKILL.md 分层控制模型)。

## 四、段落标签写法(平台机制,通用)

1. **格式**:`[段落名: 配器 + 情绪]`,只写这两件事,短而明确执行率最高。
   - ✅ `[Verse 2: hushed and intimate, sparse piano only]`
   - ❌ 长篇形容词堆砌
2. **否定指令基本无效**:`do NOT turn sad` 听不懂 → 写正向词,"防跑偏"交给 Exclude 硬约束。
3. **环境音是低概率抽卡**:`[Sound Effect: ...]` 单独成行放歌词最顶部 + 风格串双写,成功率中等;**稳妥方案永远是后期叠音效**(爱给网 aigei.com / freesound.org + GarageBand)。
4. **实测有效的标签**(标签有效性是平台机制;**用在什么歌里由装置库/profile 决定**):
   - `[Spoken word, breathy whisper close to the mic]` — 贴麦低语
   - `[Humming: soft wordless humming]` — 无词哼唱
   - `[Instrumental Interlude: guitar fades, solo piano takes over]` — 间奏换配器
   - `[End]` — 显著提高干净收尾概率,防拖泥带水
5. **其他场景标签**(社区常用,按需):纯音乐用 Custom 模式 Instrumental 开关;对唱用 `[Male Vocal]` / `[Female Vocal]` / `[Duet]`;和声用 `backing harmonies`(风格串或段落标签)。

## 五、装置库(已验证的叙事/结构装置——按题材选用,禁止默认沿用上一首的组合)

> 每条格式:装置 / 出处 / 适用 / **反指征**。装置是菜单不是流程;同类装置还有很多(见括号内未验证选项),不要只在验证过的里面挑。

**进入装置**(第一行怎么开场):
- **环境音场景开场**(正午的月亮:校钟+蝉鸣) / 适用:有标志性声景的题材 / 反指征:声景与歌无关时是噱头。
- **场景白描开场**(归燕:老屋屋檐旧巢) / 适用:叙事歌 / 反指征:无。
- **时间状语开场**(长椅宽出一半 v1:下午三点半) / 适用:日常感、纪实感 / 反指征:连续多首都用时间开场。
- (未验证选项:对话开场、问句开场、宣言开场、爵士 rubato 引子 verse——见 genre-profiles 爵士节)

**推进装置**(叙事怎么走):
- **时间跳切**(归燕:小时候→长大;正午:在一起→分手→8 年后) / 适用:跨时期题材。
- **间奏换配器做时间转场**(归燕:吉他退、钢琴进=换时代) / 适用:两章结构 / 反指征:单一时空的歌。
- (未验证:物件视角、书信体、对话体、单场景实时、平行蒙太奇)

**hook 装置**:
- **镜像副歌**(归燕:同旋律、一字之差「暖得刚刚好→还是暖得刚刚好」) / 适用:民谣/流行"两个时期"题材 / **反指征:爵士(title 回归机制与之冲突);已在近作用过(指纹查重)**。注意:其中"同文本→同旋律"是平台机制,装置本身是流行/民谣审美。
- **钩子变奏**(分节歌式,同位置词义递进) / 适用:民谣分节歌。
- (未验证:AABA title 回归、蓝调 B 句反转、问答式 hook)

**收尾装置**:
- **揭底句 + 贴麦低语**(归燕:「奶奶 你看」;长椅 v1 复用后触发查重警报) / 适用:叙事性隐喻歌、有唯一谜底、谜底揭开瞬间成立 / **反指征:无叙事谜底的歌;hook 即题旨的直抒型歌;近作已用(这是听感辨识度最高的装置,复用=最快让两首歌变成一首歌)**。配套纪律:揭底后不加词。
- **无词哼唱收尾**(归燕) / 适用:想念绵延不断的收法 / 反指征:近作已用;爵士的对应装置是器乐 outro/tag ending。
- **首尾呼应回收**(正午的月亮:Outro 回收"正午/月亮/晚安") / 适用:意象闭环型 / 反指征:无。
- (未验证:留白不揭、环形结构、视角反转、悬置收尾——爵士挽歌传统,见 genre-profiles)

## 六、装置指纹存档(查重用;每首新歌定稿后追加)

> 查重规则(SKILL.md 第 4 步):新歌与最近 3–5 首逐维比对,**重合 ≥3 维 → 强制换 ≥2 维**(优先换收尾装置/题眼句型/进入方式);换曲风不抵扣;系列感需求显式豁免。

| 维度 | 正午的月亮(2026-07) | 归燕(2026-07) | 长椅宽出一半 v3(2026-07,爵士 ballad) |
|------|------|------|------|
| 1 视角 | 第一人称对前恋人"你",8 年后回望 | 第一人称回忆,结尾直呼"奶奶" | 第一人称对亡妻"你",单日现在时(torch) |
| 2 进入方式 | 环境音声景(校钟蝉鸣) | 场景白描(屋檐旧巢) | rubato 引子 verse(近念白) |
| 3 推进装置 | 时间跳切 | 时间跳切+间奏转场 | 单场景实时,实→忆(B)→实 |
| 4 意象域/路线 | 月亮/时差/海,单纵深 | 燕/巢/屋檐,单纵深 | 长椅/湖/秋,单一 conceit |
| 5 韵辙策略 | 主歌言前→副歌江阳,Bridge 转怀来 | 遥条辙一韵到底 | 稀疏韵段末押;B 段完全离开(候/旁/吧/白) |
| 6 曲式/hook 机制 | V-PC-C,副歌完全重复 | V-PC-C,镜像副歌 | AABA+solo 结构位;title 回归 3 次逐字,语境深化 |
| 7 题眼句型 | 意象命名型(够不到的月亮) | 意象句钩子变奏(暖得刚刚好) | 意象命名型(长椅宽出一半) |
| 8 弧线形状 | 克制型(swell-pull back) | 克制反转型(顶点最静处) | 平缓微澜,顶点=solo 后 A3 刺点 |
| 9 收尾装置 | 唱词 Outro 首尾呼应+声景 fade | 低语揭底+哼唱 | 悬置(未完成动作)+器乐 fade |

> 教训存档:长椅 **v1**(已废弃)曾与归燕重合 6–7 维(收尾标签字符串级相同),用户一听即指出"和归燕太像"——**换了曲风不等于换了装置**。v3 按爵士 profile 重写后,依 SKILL 第 4 步判重口径逐首两两比对:vs 归燕 0 维、vs 正午 2 维(视角人称+对象、题眼句型同为意象命名型,均题材绑定),通过。装置之外的**词面回声**也要查:v3 初稿曾残留「没人X」不在场句式(与归燕 5 处成规律)、「风」施动者(三首歌 4 处)、「V来V去」叠词——均为作者手癖级复制,GAN 相似度镜头查出后清零/降频。
>
> **家族听感存量(装置查重覆盖不到的层,下一首的差异化杠杆)**:仓库三首歌全部是 58–66 BPM 慢板、男声中低音、克制怀念不在场之人、安静收尾、Styles 以 tender/clear mandarin 类公式收尾(长椅 v3.2 起已改 `sung in mandarin`)。下一首新歌建议优先在这些维度里挑 1–2 个做差异:速度/性别与声部/题材姿态(怀念之外的情绪)/收尾能量/串尾语言标记写法。

## 七、去"AI 味"手段(按杠杆从小到大)

1. **prompt 层**:自由律动体裁(民谣/爵士/bossa/R&B)用 `natural loose timing that breathes between phrases, never rushed` + `behind-the-beat vocal phrasing`("赶"是机器感主因);**网格律动体裁(电子/说唱/朋克)禁用 loose timing 类词**(机器感病根在鼓型/音色);慢歌配低 BPM(快歌体裁防机器感靠律动词,不是降速);Weirdness 别太低。
2. **抽卡层**:一次 2 条 × 3–5 轮起步,难收敛加到 5–8 轮;按"有呼吸声、咬字有轻重"挑;局部瑕疵用 Replace Section 修,不整首重抽。
3. **后期层**:导出分轨,叠真实呼吸声(-20dB 句间)、去齿音加暖饱和、辅音重音自动化。
4. **真人层(杠杆最大)**:自己清唱 → Kits.AI / SoundID VoiceAI 换授权音色(真人的气息/强弱/咬字全保留,只换音色,合法);或 AI 主体 + 真人补唱关键句。

## 八、标准工作流

```
主题访谈 → 曲风确立+载入 genre-profiles 对应 profile
  → 视角/意象/韵律设计(密度与换韵按 profile)
  → 结构与装置设计 + 装置指纹查重(写词前!)
  → 写词(行长方向/hook 机制按 profile;交稿过 13 项 checklist,含装置复检)
  → 风格串(六维组装+profile Suno 要点)+ Exclude(按本歌跑偏方向单独设计)+ 滑块
  → v5.5 生成 2条 × 3–5 轮(难收敛加到 5–8 轮)
  → 按"成败句"挑版本(每首歌预先定义,勿沿用上一首的成败句型)
  → 局部修:Replace Section / Extend / Studio;演绎方向错但旋律好 → Remix→Cover(再生成,歌会变)
  → 满意版本 Get Whole Song / 下载 WAV
  → 后期:叠环境音、微调动态(GarageBand;发行级链路见 production-advanced 第四节)
  → 发布物料 + 配置.md 归档(含装置指纹小节)
```

**Remix vs Edit 心法**:Remix(Cover/Reuse Prompt)= 以这首为底再生成,歌会变;Edit(Replace Section/Extend/Crop/Studio)= 在这条音频上动手术。90 分的版本走 Edit,别 Remix。**唱法/旋律/曲风是全局属性,错了整体重抽。**
**订阅门槛提醒**:Replace Section/Editor、Advanced Split 等为付费档能力;免费档无商用权——工作流默认按 Pro 及以上写。

## 九、中文歌词发音踩坑清单(中文演唱物理,全曲风通用)

- **多音字必避**:"咯咯"→ luoluo(改"傻傻");"得/地/了/着/曾/降/重"等高危字,关键位置换无歧义字(完整清单见 music-theory 1.6)。
- 避不开时:①同音字替换("重"→"崇",首选);②拼音标注 `重(chong)逢`(大部分有效);已生成的咬字错误用 **Replace Section** 只重做那一两句。
- 歌词最顶端加 `[This is a Mandarin song]` 有助稳定普通话发音。
- **黏着语素不能单用**:"走得越来越遥"不像人话(改"翅膀硬了往外跑")。押韵永远不能牺牲口语自然度。
- 生僻字咬字易怪,常用字最稳;Styles 栏用英文写更稳(歌词中文、风格英文)。

## 十、歌词内容层的验证经验

- **含蓄 = 情绪藏着,不是句子看不懂**。被用户打回的教训:"两个季节 焐着同一块玻璃的暖"(意象跳两步,不懂——注意该歌为民谣,理解步数上限一步;爵士/说唱允许两步,见 genre-profiles)。
- **隐喻系统按 profile 的意象策略走**(民谣/爵士单意象域;说唱可换喻),混用即散指的是"无设计的混用"。
- **真实细节 > 形容词**(全曲风通用):"狸花猫只在她面前乖、挠过我一爪"这种编不出来的细节,一句顶十句抒情。
- **笑点不放段落末尾**:包袱后面要留温柔句接住,否则与下一段衔接断裂。
- 镜像副歌、揭底句等**装置的适用条件与反指征见第五节装置库**——它们是特定题材的选项,不是通用律令。

## 十一、生成结果听审清单(挑版本用)

预定义"成败句"之外,系统过一遍(前 4 项一票否决):

**Artifact 排查(Suno 特有毛病)**
1. 标签被唱出来 / 混入其他语言 / 人声中途突变(音色换人)
2. 段落接缝突兀、结构崩坏(漏段、擅自变奏出设计外的结构)
3. 咬字错误(多音字/洋腔)——对照歌词逐句听一遍
4. 结尾拖泥带水或戛然而止

**音乐性评估**
5. Hook 记忆点:听完能哼出题眼句吗(承载方式按 profile:流行=副歌;爵士=title 句)
6. 情绪弧线:形状符合设计吗,顶点在预期位置吗(**预期位置由 profile 定义**:流行=FC;爵士=solo 后最后一段;EDM=drop)
7. 人声真实感:有呼吸声、咬字有轻重、不过度演唱(melisma 泛滥=扣分,R&B 除外但也要有节制)
8. 编曲动态:段落间有密度对比,不是一堵墙
9. 混音质感:人声与伴奏平衡、无刺耳频段
10. **曲风身份**:对照 profile 身份要素逐条打钩(如爵士:swing 律动?behind the beat?和声色彩?solo 段成立?)

## 十二、体裁差异

**已升级为完整曲风 profile 库,见 references/genre-profiles.md**(12 曲风:身份要素/曲式/词法/弧线/跑偏/Suno 要点)。旧版"体裁速查表"只替换风格串关键词、不替换结构与词法,已被证明防不住跑偏(长椅 v1 教训),废弃。

## 十三、发布合规(中国,2026)

- Suno 付费订阅期间生成才有商用权(免费版不可商用)。
- 汽水音乐发布:优先查"汽水音乐人/字节系创作者"官方入驻通道(政策变化快,以当时 App 内规则为准);无个人通道再走数字发行商,签约前确认发行范围含汽水。
- **AI 生成内容必须标注**(《人工智能生成合成内容标识办法》2025-09-01 施行)。
- 版权归属:著作权保护要求人类独创性投入——**自写歌词是最有力的权利证据**(不存在公开的"30%"之类量化门槛,勿引用具体比例)。
- 禁克隆真人声音(2024 北京互联网法院首例 AI 声音侵权案,判赔约 25 万);"像某歌手"只能靠特征描述,不能在提示词写艺人名(Suno moderation 会拦)、不能传原曲、不能用其录音训练。
- 封面 ≥1440×1440,无 logo/水印/二维码。
- 发布前音频 QC:WAV 导出、响度 -14 LUFS / True Peak ≤ -1 dBTP(Apple -16)——详见 production-advanced.md 第四节。
