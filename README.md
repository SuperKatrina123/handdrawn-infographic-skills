# handdrawn-infographic

一个 Claude Code Skill：把结构化文字（大纲、概念讲解、对比、模式清单、流程、Agent 架构等）转成手绘白板风格的信息图。

两阶段工作流：先产出 **布局方案 + 图像 Prompt** 给你确认，确认后才调用 Gemini 生图（或只交付 Prompt 自己生）。

## 视觉锚点

- **背景**：暖色奶油纸（`#F5F1E8`），带淡淡纸纹
- **线条**：手绘黑墨水，带抖动，圆角矩形
- **配色**：muted pastel —— dusty rose / lavender / sage green / baby blue / peach / soft yellow（不饱和、不霓虹、不渐变）
- **高亮**：关键句用 sage-green 或 soft-yellow 手绘荧光块
- **箭头**：单笔手绘带小三角箭头；虚线表示隔离；X 表示禁止路径
- **图标**：黑色线描小 doodle（链条、分叉、奖杯、放大镜、齿轮……）
- **可选彩蛋**：火柴人 + 对话气泡，承载一句「道理」

## 六种布局原型

决策顺序：**metaphor → radial → progression → 1 → 2 → 3–6**。

| 原型 | 何时用 |
|---|---|
| **Metaphorical illustration** | 文本以具象隐喻为骨架（脚手架、花园、冰山、工厂） |
| **Concentric radial** | 结构围绕中心向外展开（core → ring → ring） |
| **Progression strip** | 同一结构在 3–4 个阶段演化（turn 1 → 2 → 3） |
| **Single-scene** | 讲透一个机制 / 流程 |
| **Comparison** | 2 个对立方案 / 顺序两阶段（sub-variant：Phase 1 → Phase 2 with handoff） |
| **Grid** | 3–6 个并列模式 / 原则 |

详见 `references/layout-archetypes.md`。

## 用法

在 Claude Code 里直接描述你要画的东西，比如：

> 把这段文字画成手绘信息图：「Parent agent delegates tasks to sub-agents in parallel. Each sub-agent has isolated context, its own tools, one job. They don't talk to each other. Results funnel back as compressed summaries so the parent context stays clean.」

Skill 会先给你：
1. 选定的布局原型 + 一句理由
2. ASCII 布局草图
3. 每个卡片的颜色角色清单
4. 完整的英文 image prompt

确认后再出图，或者只要 prompt 自己拿去生。

## 目录结构

```
handdrawn-infographic/
├── SKILL.md                         # 主流程 + 风格锚点 + 反模式
├── README.md                        # 本文件
└── references/
    ├── layout-archetypes.md         # 六种原型的判定树和结构规范
    └── prompt-template.md           # 英文 prompt 模板 + 色板 + 7 个完整示例
```

## 安装

把整个 `handdrawn-infographic/` 目录放到 `~/.claude/skills/` 下即可：

```bash
git clone git@github.com:SuperKatrina123/handdrawn-infographic-skills.git ~/.claude/skills/handdrawn-infographic
```

## License

MIT
