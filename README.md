# handwriting-homework-pipeline

马原作业 → 手写稿流水线（三个可复用 Agent Skills 的集合）。

把「马原课程答题」和「手写稿生成」串成一条完整流水线：用户给一道马原题目（文字或图片），自动完成答题 → 生成 Word 文档 → 转成手写稿 zip → 交付，最后推荐图片压缩工具。

## 仓库结构

```
handwriting-homework-pipeline/
└── skills/                          # 所有 skill 都在这
    ├── mayuan-assistant/            # 子 skill①：马原答题 → Word 文档
    ├── handwriting-generator/       # 子 skill②：Word/文字 → 手写稿 zip
    └── handwriting-homework-pipeline/  # 主 skill：编排上述两者
```

## 自动安装（给 AI / 用户看）

以下步骤供 AI 助手或用户执行，把本仓库安装为可用 skill：

1. 将 `skills/` 下的**三个文件夹**（`mayuan-assistant`、`handwriting-generator`、`handwriting-homework-pipeline`）整体复制到目标工具的 skills 目录：

   | 工具 | 目标目录 |
   | --- | --- |
   | TRAE（TraeCode） | `.trae/skills/` |
   | Claude Code | `.claude/skills/` |
   | 其他兼容 Agent Skills 规范的工具 | 该工具约定的 skills 目录 |

   即最终结构为：`<skills目录>/mayuan-assistant/SKILL.md`、`<skills目录>/handwriting-generator/SKILL.md`、`<skills目录>/handwriting-homework-pipeline/SKILL.md`。

2. 无需任何配置或凭据。工具会自动扫描 skills 目录并读取各 `SKILL.md`。

3. 主 skill 依赖两个子 skill，三者缺一不可。

## 使用示例

安装后，向助手说一句：

> 把这道马原题做成手写稿：「为什么说对立统一规律是事物发展的根本规律？」

助手会自动：加载主 skill → 调 mayuan-assistant 按教材作答生成 Word → 调 handwriting-generator 弹字体选择框后生成手写稿 zip → 交付 zip 与 Word → 推荐图片压缩网站。

## 各 skill 说明

| Skill | 功能 | 关键依赖 |
| --- | --- | --- |
| `mayuan-assistant` | 马原答题，首次调用自动从校方页面下载 2023 版课本作为依据，输出 Word（无 Python 则纯文字） | 网络、Python + python-docx/pypdf |
| `handwriting-generator` | 浏览器自动化操作 autohanding.com 生成手写稿 zip，内置激活码（每日有免费次数上限） | 浏览器自动化、Python + python-docx、网络 |
| `handwriting-homework-pipeline` | 编排上述两个子 skill 的流水线 | 两个子 skill 同时安装 |

## 授权

本仓库以 **MIT 许可证** 开源，详见 [LICENSE](./LICENSE)。

## 合规声明（重要）

1. **教材版权**：`mayuan-assistant` 仅在运行时从其院校官方页面下载《马克思主义基本原理》（2023年版）作为**检索依据**，本仓库**不包含、不分发任何教材内容**。课本版权归高等教育出版社及编写组所有，请仅用于个人学习用途，遵守来源网站的使用条款。
2. **第三方服务**：`handwriting-generator` 通过浏览器自动化调用 **autohanding.com（凹凸工坊）** 服务，该服务及其条款归其运营方所有。请遵守其服务条款，勿滥用、勿绕过付费机制。
3. **激活码**：仓库内置的免费福利激活码由 autohanding.com 提供，每日有免费使用次数上限；**本仓库不包含任何付费激活码**。付费激活请前往 autohanding.com 官方渠道。
4. **内容用途**：本仓库仅提供技能编排与操作流程，用于个人学习、作业辅助等合法用途。用户应自行对使用行为负责。
5. **非官方关联**：本仓库与任何院校、出版社及 autohanding.com 均无隶属或背书关系。
