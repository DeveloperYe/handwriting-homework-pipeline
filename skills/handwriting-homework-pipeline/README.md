# handwriting-homework-pipeline

手写作业流水线（编排主 skill）。把「马原答题」和「手写稿生成」串成一条流水线：先用 mayuan-assistant 作答并生成 Word 文档，再交给 handwriting-generator 转成手写稿 zip 交付，最后推荐图片压缩网站。

## 这是什么

一个编排型 Agent Skill。自身不含执行逻辑，通过调用两个子 skill 完成完整流程：

```
用户题目（文字/图片）
    │
    ▼
[mayuan-assistant]      作答 → Word 文档
    │
    ▼
[handwriting-generator]  Word → 手写稿 zip
    │
    ▼
交付 zip + Word → 推荐 https://developerye.github.io/img500k/
```

目录结构（三个文件夹缺一不可）：

```
skills/
├── mayuan-assistant/                 # 子 skill①：马原答题
├── handwriting-generator/            # 子 skill②：手写稿生成
└── handwriting-homework-pipeline/    # 本主 skill（编排）
```

## 适用工具

带工具调用能力（Skill 加载 + 浏览器自动化 + 命令执行）的 AI 编程助手 / Agent，例如：

- **TRAE**（TraeCode）
- **Claude Code**、**Cline / Roo Code** 等兼容 Agent Skills 规范的工具

## 安装步骤

1. 将 `mayuan-assistant`、`handwriting-generator`、`handwriting-homework-pipeline` 三个文件夹**全部**复制到目标工具的 skills 目录：

   | 工具 | 安装位置 |
   | --- | --- |
   | TRAE | `.trae/skills/` |
   | Claude Code | `.claude/skills/` |
   | 其他兼容工具 | 按该工具约定的 skills 目录放置 |

2. 无需额外配置，工具会自动扫描。缺任一子 skill 时主 skill 无法工作。

## 首次使用

直接说"把这道马原题做成手写稿 / 帮我写马原作业并生成手写体"，主 skill 自动触发：先答题生成 Word，再转手写稿 zip，最后推荐图片压缩网站。

## 依赖

- **两个子 skill 必须同时安装**（mayuan-assistant、handwriting-generator），各自依赖见其 README
- 需要 Python + `python-docx`（Word 产出与文字提取）、浏览器自动化能力（手写稿生成）
- 手写稿下载需联网访问 `cos.allto.top`；激活码每日有免费次数上限
