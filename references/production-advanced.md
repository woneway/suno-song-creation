# 制作进阶:旋律文字化 · 编曲 Build 曲线 · 弦乐写法 · 后期链 · 参考曲拆解

> 深化自 2026-07 专项调研(官方 Release Notes/帮助文档 + 2026 社区实测)。
> 与 music-theory.md 板块 2-7 配合:那边是基础概念,这边是拿来即用的操作层。

## 一、旋律的文字化控制(四条通道)

Suno 无法逐音符控旋律,能间接控制的是:

1. **歌词音节即节奏型**(最强通道):字数与句读直接决定旋律节奏——短句+重复字型 ≈ 重复动机。
2. **段落参数化标签控制音区/能量**:`[Verse: low register, intimate]` `[Chorus: soaring melody, higher register]`(v5 起参数化标签有效)。
3. **风格描述词**:`catchy vocal hook`、`repetitive melodic motif`、`anthemic sing-along chorus`、`simple stepwise melody`。
4. **段落编号**:`[Verse 1]`/`[Verse 2]` 帮模型"同段同旋律、异段异旋律"。

不可转译:具体音程、和弦对位、精确的弧线顶点位置(只能靠 Final Chorus 标签近似)。

**背后的旋律学常识**(用于判断生成结果好坏):
- 动机(motif)= 2–4 个音的最小细胞;变化手法从保守到激进:原样重复→模进(同型移高/低)→保节奏换音高→保音高换节奏→扩缩时值。**同一动机连用不过三,第三次要变。**
- **音域设计**(V-C 流行曲式的判准):主歌用全曲最低音区+最窄音域,副歌用最高音区;流行歌主副歌同音区易显平。人声总音域 ≤1.5 个八度可保传唱性。**非流行曲式不适用此判准**:AABA/循环曲式的段落对比靠和声与密度,bossa/爵士的窄音域是合法身份形态,勿按"平"误判重抽。
- **Hook 旋律特征**:级进为主保顺口,嵌一个 ≥4 度的特征跳进做记忆点(或全级进+一个强节奏记忆点);hook 的节奏型比音高更易被记住;结尾落主音="完结",落不稳定音="钩着人等下一句"。
- **可唱性基线(全曲风必载)**:音域/BPM/人声呈现/重复工程与筛选端硬判据的完整杠杆见 **references/singability.md**——本节四通道是"旋律怎么控",那边是"控到人能跟着唱"。

## 二、中文流行 Ballad 的编曲 Build 曲线(段落 × 配器惯例)

| 段落 | 华语抒情歌惯例 | Suno 标签写法 |
|---|---|---|
| Intro | 主奏乐器独奏动机 + 氛围音 | `[Intro - solo piano, ambient]` |
| V1 | 人声 + 单一和声乐器;无鼓或极简 | `[Verse 1: piano and vocals only]` |
| Pre-C1 | 加 pad/弦乐长音,bass 进,鼓渐入 | `[Pre-Chorus: strings swell, drums building]` |
| C1 | 鼓组进但**七分力**;弦乐长音铺底不给满 | `[Chorus: full band, soft strings]` |
| 间奏 | 主奏乐器 solo 回收动机 | `[Interlude - piano solo]` |
| V2 | 鼓保持,加一层(吉他分解/弦乐副旋律/句间加花) | `[Verse 2: add drums, string countermelody]` |
| C2 | 满编;弦乐高八度;和声人声进 | `[Chorus: full band, lush strings, backing harmonies]` |
| Bridge | 减法(抽鼓)或转调铺垫;末尾 stripped + 一拍静默再爆 | `[Bridge - stripped down, vocals and piano]` |
| Final C | 升半音/全音;弦乐最高音区齐奏;合唱;ad-lib | `[Final Chorus - key change up, soaring strings, choir]` |
| Outro | 回收 intro 动机,渐弱/留白 | `[Outro - fade out, solo piano]` |

## 三、弦乐在华语抒情歌中的四种写法

1. **长音铺底(pad 化)**:和弦内音、二分/全音符,与人声密度**互补**——人声密时弦乐拉长音,人声长音时弦乐做连接填充。
2. **句间加花(fill/呼应)**:在人声乐句空隙进出,一问一答。
3. **副旋律/对位**:V2 或 C2 加一条不抢主旋律的中高音线,让声部"流动"。
4. **高潮八度齐奏**:final chorus 小提琴组高八度 unison 上行线 + 大提琴低音加温,"镀金"时刻。

声部配置口诀:**上密下疏中不空**(高频活跃、低频克制、中频填实)。
提示词转译:`sustained string pads` / `string fills between vocal phrases` / `string countermelody` / `soaring unison strings`。

## 四、AI 生成音乐的发布级后期链(2026)

**Suno 端(官方能力,2026-07 时点)**:
- v5:2025-09(音质/人声提升,老歌可 Remaster 到 v5);Studio(浏览器生成式 DAW,Premier 档):2025-09;v5.5:2026-03(Voices 录自己声音、Custom Models);**分轨大升级:2026-06,用生成模型逐轨"重生成"而非传统掩码分离**。
- 分轨三模式:Auto Split(一键最多 **12 stems**,50 credits)/ Split from Mix(抽单一乐器+其余,20 credits)/ Advanced Split(仅 Premier,从近 100 种乐器自选,20 credits/stem);Studio 可导出 12 条时间对齐 WAV 进 DAW。
- 外部备选:iZotope RX Music Rebalance、UVR5(免费)。

**流程:生成 → 分轨 → 修 → 混 → 母带 → 交付**
1. 生成端定稿,下载 **WAV** 再进后期;
2. 分轨(优先 Suno 原生);
3. 修音:人声轨 Melodyne/Auto-Tune 修音准时值;RX 做频谱修复,去"AI shimmer"毛刺与段落接缝噪声;
4. 混音:分轨平衡;AI 鼓瞬态偏软,必要时鼓采样替换/增强;
5. 母带:Ozone(新版 Stem EQ 可在立体声内对人声/鼓/bass 分别 EQ,对"只有成品没有分轨"的 AI 歌对症)或 LANDR 自动母带;
6. **响度交付标准**:Spotify/YouTube/Tidal 等 **-14 LUFS integrated**,Apple Music **-16 LUFS**;True Peak ≤ **-1 dBTP**(Spotify 建议 -2 防转码削波)。单一母带「-14 LUFS / -1 dBTP」通吃全平台;**响度战争无意义**——归一化会把超响母带拉回,只损失动态。

**轻量替代**(非专业场景,如本仓库工作流):GarageBand 叠环境音/呼吸声 + 音量自动化,已能解决 80% 的"塑料感";上面的完整链是发行级 QC 的升级路径。

## 五、参考曲目六维拆解法(合法反推提示词)

**平台底线**:Suno 禁止提示词出现真实艺人名(moderation 拦截,style 与歌词字段都不允许);风格不受版权保护,但**不复刻具体旋律与歌词文本、不上传受版权保护音频做 cover/persona 素材、营销不用"AI 版某某"表述**。

把"想要像某首歌"翻译成可写的特征:

1. **速度与律动**:测 BPM(慢歌报 160+ 先除 2)、straight/swing、是否 half-time、鼓型(four-on-the-floor?鼓刷?);
2. **人声 character**:性别/声部/音区、音色(breathy/husky/clear)、处理(close-miked/reverb)、习惯(句尾假声?behind the beat?)——**描述声音性质,不描述"谁"**;
3. **制作配色**:乐器清单+各自角色(谁铺底谁加花)、mix 美学(dry/lush、lo-fi/polished)、年代感(90s/2010s);
4. **情绪美学**:两三个准确的情绪词(melancholic、bittersweet、defiant);
5. **结构拆解**:逐段计时——intro 几秒、段落顺序、第一副歌出现时间、爆点位置、outro 类型 → 直接翻成段落标签序列;
6. **和声与律动骨架**:听出进行类型(6415/卡农…)与和声节奏 → Suno 不认级数,翻成风格词(`emotional ballad progression`、`nostalgic anthem chords`)。

**组装公式(2026 共识)**:曲风+副流派 → 情绪/能量 → 人声 → 配器 → 制作/速度。**词量口径以 suno-spec §1 为唯一事实源**(甜点 15–30 词/4–7 个核心描述符;v5.5 上限约 1000 字符,旧"200 字符"限制过时);行为指令密集的串可到 40+ 词,接受权重稀释并配合 Style Influence 调高(案例:长椅 v3.3 ≈46 词/SI 82)。

本仓库实例:「陈奕迅《圣诞结》那种感觉」→ `warm tender male baritone, slightly husky breathy vocals, mature mid-low register, emotional cantopop-style mandarin ballad, lush cinematic strings, soft grand piano, slow 68 BPM, restrained heartfelt delivery`——六维里的②③④,一个名字都没提。
