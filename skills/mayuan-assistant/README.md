# mayuan-assistant

《马克思主义基本原理》课程作业助手（Agent Skill）。首次调用时自动从校方页面下载 2023 版课本到工作空间作为唯一作答依据，支持图片或文字形式的题目输入，按六条规则作答并输出 Word 文档（无 Python 环境则输出纯文字）。

## 这是什么

一个符合 Agent Skills 通用规范（SKILL.md + frontmatter）的可复用技能包，由一个文件夹构成：

```
mayuan-assistant/
├── SKILL.md   # 技能本体（规则 + 执行流程）
└── README.md  # 本文件（安装说明）
```

## 适用工具

带工具调用能力的 AI 编程助手 / Agent 均可使用，例如：

- **TRAE**（TraeCode）
- **Claude Code**
- **Cline / Roo Code** 等兼容 Agent Skills 规范的工具

纯对话型助手（不带网页抓取 / 文件下载 / 执行命令能力）无法执行下载课本步骤，不适合本技能。

## 安装步骤

1. 将 `mayuan-assistant` 整个文件夹复制到当前项目（或用户级）的 skills 目录下：

   | 工具 | 安装位置 |
   | --- | --- |
   | TRAE | `.trae/skills/mayuan-assistant/` |
   | Claude Code | `.claude/skills/mayuan-assistant/` |
   | 其他兼容工具 | 按该工具约定的 skills 目录放置 |

2. 无需额外配置。工具会自动扫描 skills 目录并读取 `SKILL.md`。

## 首次使用

直接提问马原相关题目（文字或图片均可），技能会自动触发并完成：
下载课本 → 校验（364 页）→ 检索作答 → 输出结果。

## 依赖

- 运行环境需具备网络访问能力（首次调用需访问校方页面下载课本）
- 生成 `.docx` 需要 Python 与 `python-docx`、`pypdf`；若环境无 Python，技能会自动降级为纯文字输出，不影响使用
- 课本下载地址从页面 HTML 动态提取，不依赖固定链接；若校方下架页面，技能会提示无法获取课本
