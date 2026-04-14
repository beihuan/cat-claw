# 🐱 Cat Claw

乳白矮脚曼基康的全能助理配置仓库。

## 仓库结构

```
cat-claw/
├── SOUL.md                              # 灵魂文档 — 身份、性格、行为准则
├── IDENTITY.md                          # 身份配置 — 名称、物种、风格
├── HEARTBEAT.md                         # 心跳配置 — 定期检查任务（当前为空）
├── .gitignore
└── skills/
    ├── chinese-literature/              # 汉语言文学文献检索与综述生成
    │   ├── SKILL.md                     #   工作流定义（方向综述 + 论点溯源）
    │   └── references/
    │       └── api-patterns.md          #   学术数据库检索参考（含秘塔AI搜索配置）
    ├── neverland-farm/                  # NeverLand 农场文字 MUD 游戏
    │   └── SKILL.md                     #   农场运营自动化
    └── sentence-anatomy-tutor/          # 英文长难句解析
        ├── SKILL.md                     #   解析工作流
        ├── config.json                  #   配置
        ├── assets/
        │   └── prompt_flow.md           #   提示词流程
        └── references/
            └── methodology.md           #   解析方法论
```

## Skills 说明

| Skill | 用途 | 触发词 |
|-------|------|--------|
| **chinese-literature** | 学术文献检索 + 文献综述生成 | 查文献、找论文、文献综述、找出处 |
| **neverland-farm** | 文字 MUD 农场养成游戏自动化 | 种地、农场 |
| **sentence-anatomy-tutor** | 英文长难句语法结构拆解 | 解析长难句、看不懂这句英文 |

## 运行环境

- 平台：OpenClaw
- 工作目录：`/home/z/my-project/`
