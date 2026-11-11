# Open Writing Skill：喂出你个人文风的开源去 AI 味写作骨架

这不是把某一个人的说话腔调硬塞给你的专用配置，而是一套**零代码依赖、开箱即用、10 分钟就能换上你自己文风**的通用写作 Skill 骨架。

适用于 Claude Code、Cursor、Codex、Antigravity 等所有支持 `SKILL.md` 的 AI 工具；如果你平时只用网页版聊天框，仓库里也准备好了单文件一键复制版。

---

## 为什么市面上的“禁用词清单”写不出好文章？

很多人去 AI 味的第一反应，是去网上抄几百个禁用词（不准用赋能、闭环、不是……而是……），对着大模型下死禁令。用过就知道，效果往往很拧巴：

1. **光靠下禁令，模型只会无所适从**：大模型本质上是个模仿高手。你连发二十条“不准这样、严禁那样”，却不拿一篇真正的好文章给它看，它脑子里全是你要封杀的词，最后要么换个同义词继续端着，要么把句子删成干巴巴的产品说明书。
2. **所有要求塞进同一个文件会串味**：同一个人写三千字深度复盘，和发一条百来字的日常短动态，说话节奏完全相反。全混在一个大提示词里，写出来的长文碎嘴，短文又像裹脚布。
3. **推理开太高，文章反而像八股文**：现在不少模型针对写代码做了重度特化，一旦把深度思考（Thinking）拉满，动笔前先盘算一堆起承转合和免责声明，天然就带着一股汇报材料的假味。

---

## 这套骨架靠哪三件事解决问题？

1. **拿真实好文章原文打底（Few-Shot 样板 + 结构提炼）**：不搞空洞的形容词总结，直接把你自己写得最顺手、或者你最欣赏的真实人类文章原文放进音色卡，配几句大白话讲清它的推进节奏，让模型直接照着学腔调。
2. **按题材拆开音色卡，写什么只读哪一张**：仓库默认拆好了深度长文、日常短评与工具推荐、互动提问、踩坑随笔四张独立音色卡。每次动笔只读取对应的一张卡，上下文干干净净，绝不串味。
3. **最外层只留二三十个重灾区禁词做兜底护栏**：路由范文指清楚了，最后只用一份精简锋利的全局禁词表拦住最扎眼的口头禅和结尾升华客套话，单轮直出就能拿到干净自然的稿子。

> **模型与参数建议**：日常写文章改稿，实测首选 **Gemini 系列模型**，并把思考等级（Thinking Level）调到 **Low（低）**。少让模型在脑子里过度盘算修辞套路，顺着范文的语感自然往下流淌，人味最足。

---

## 目录结构

```text
open-writing-skill/
├── SKILL.md                          # 总入口：按题材挑一张音色卡按需读取，守住事实与改稿底线
├── voices/                           # 按场景拆分的音色卡（正向风格描述 + 专属禁忌 + 标杆范文原文）
│   ├── deep-article.md               # 音色卡 1：深度长文、经验复盘与通识科普
│   ├── short-post.md                 # 音色卡 2：日常短评、观点输出与开源工具推荐
│   ├── probe-question.md             # 音色卡 3：互动提问与社区话题探针
│   └── craft-notes.md                # 音色卡 4：日常踩坑随笔与选型算账心得
├── references/
│   ├── banned-words.md               # 全局兜底护栏：精简二三十个高频塑料词与八股句式
│   └── bad-vs-good-examples.md       # 真实正反例对照手册：一眼看懂什么样的样本算差、什么算好
└── prompts/
    └── web-single-prompt.md          # 网页端单文件浓缩版（适合 Google AI Studio / 网页聊天框直接复制）
```

---

## 安装与使用方式

### 方式一：本地 Agent 工具一键安装（推荐）

使用 `skills` CLI 一键装入你的全局或项目目录：

```bash
npx skills add realchendahuang/open-writing-skill
```

或者直接克隆到对应工具的技能目录：

```bash
# Claude Code 全局技能目录
git clone https://github.com/realchendahuang/open-writing-skill.git ~/.claude/skills/open-writing-skill

# Cursor / Codex / Antigravity 项目级技能目录
git clone https://github.com/realchendahuang/open-writing-skill.git .agents/skills/open-writing-skill
```

### 方式二：网页聊天框直接复制使用

如果你平时只在网页版 Gemini 或 Google AI Studio 里写文章，直接打开仓库里的 [`prompts/web-single-prompt.md`](prompts/web-single-prompt.md)，把里面的文本复制进 **System Instructions（系统提示词）**，换上两篇你自己的文章就能直接开写。

---

## 10 分钟喂出你个人文风的三步实操

仓库里的音色卡已经内置了几篇调好味道的真实范文，装上就能直接用。想让它彻底变成你自己的口气，只需要花 10 分钟做三步：

1. **翻出 2~3 篇纯人类写的旧文章**：去你以前的博客、公众号、朋友圈长文或备忘录里，挑几篇你自己亲手写的、读着最顺眼的旧文；如果自己平时写得少，就去挑一位你最喜欢的作家或博主的原文（注意：千万别拿 AI 生成的稿子当范文喂进去）。拿不准怎么挑样本时，可以先翻看 [`references/bad-vs-good-examples.md`](references/bad-vs-good-examples.md)。
2. **对号入座填进 `voices/` 槽位**：把长文粘进 `voices/deep-article.md`，短评粘进 `voices/short-post.md`，顺手用两句大白话写清这篇开头怎么切入、中间怎么举例、结尾怎么收住。
3. **跑一篇试写抓漏网词**：用 **Gemini + Thinking Low** 丢一段粗略想法试写一篇。如果成稿里还蹦出一两个让你皱眉头的词，顺手加进 `references/banned-words.md`。来回微调两三次，长出来的就完全是你自己的笔触了。

---

## 开源协议

[MIT License](LICENSE)
