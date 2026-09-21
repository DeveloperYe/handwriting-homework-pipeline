# handwriting-generator

手写稿生成器（Agent Skill）。通过浏览器自动化操作凹凸工坊（autohanding.com），把纯文字或 docx 文档转成带纸张背景、手写字体、涂改痕迹的真实感手写稿图片。激活码已内置。

## 这是什么

一个符合 Agent Skills 通用规范（SKILL.md + frontmatter）的可复用技能包，由一个文件夹构成：

```
handwriting-generator/
├── SKILL.md   # 技能本体（执行流程 + 激活码）
└── README.md  # 本文件（安装说明）
```

## 适用工具

带**浏览器自动化**与**命令执行**能力的 AI 编程助手 / Agent，例如：

- **TRAE**（TraeCode，含 browser_use 子代理）
- **Claude Code**
- **Cline / Roo Code** 等支持浏览器自动化的工具

本技能必须能操作真实浏览器（点击、输入、下拉、抓网络请求）并执行本地命令（下载/解压），纯对话型助手无法使用。

## 安装步骤

1. 将 `handwriting-generator` 整个文件夹复制到当前项目（或用户级）的 skills 目录下：

   | 工具 | 安装位置 |
   | --- | --- |
   | TRAE | `.trae/skills/handwriting-generator/` |
   | Claude Code | `.claude/skills/handwriting-generator/` |
   | 其他兼容工具 | 按该工具约定的 skills 目录放置 |

2. 无需额外配置。工具会自动扫描 skills 目录并读取 `SKILL.md`。

## 首次使用

直接说"把手写稿生成… / 把手打文字转成手写… / 把这个 docx 转成手写稿"，技能会自动触发，浏览器操作凹凸工坊完成：填文字 → 选字体/纸张 → 调凌乱度 → 预览 → 输激活码下载 → 交付手写稿图片。

## 依赖

- 运行环境需具备浏览器自动化能力（操作 autohanding.com 页面）
- docx 输入需 Python + `python-docx`（提取文字）；PDF 输入需 `pypdf`；图片输入需 OCR/图片识别能力
- 下载手写稿需联网访问 `cos.allto.top`（文件直链，签名 token 数分钟内过期，须及时下载）
- 技能内置激活码已实测可用；若失效，需用户手动提供新激活码

## 合规声明

本技能通过浏览器自动化调用 autohanding.com（凹凸工坊）第三方服务，请遵守其服务条款。内置免费福利激活码有每日次数上限，本技能不含任何付费激活码。用于个人学习、作业辅助等合法用途，用户自行对使用行为负责。
