📘 PPT Design Skill
A Claude Code skill that transforms a PPT outline into fully structured, slide‑by‑slide design documents.

🚀 Overview
PPT Design Skill is a Claude Code skill that converts a raw PPT outline into a complete page‑by‑page design specification.
It integrates brand configuration, project constraints, and controlled vocabularies to generate consistent, high‑quality design documents for every slide.

Each generated slide includes:

Full copywriting (complete text content)

Visual structure (layout, hierarchy, composition guidance)

An AI‑ready image prompt (optimized for image generation models such as image2)

Versioning and revision logs (auto‑managed by the skill)

This skill is ideal for teams that need repeatable, high‑quality PPT design workflows powered by AI.

✨ Key Features
1. Page‑by‑page PPT design generation
Turn any PPT outline into detailed slide specifications with copy, layout, and visual guidance.

2. Brand configuration support
Use config/global-brand.yaml to define brand tone, color rules, typography, and visual identity.

3. Project constraints
Use config/project-constraints.yaml to enforce project‑specific rules such as forbidden content, required structure, or compliance notes.

4. Controlled vocabularies
Ensure consistent terminology across slides using rules/controlled-vocabularies.md.

5. Visual prompt generation
Automatically produce high‑quality prompts for AI image generation tools.

6. Versioning & revision logs
The skill maintains version history and revision notes for every generated output.

📂 Project Structure
代码
PPT-design-skill/
├── config/
│   ├── global-brand.yaml
│   ├── global-brand.example.yaml
│   ├── project-constraints.yaml
│   └── project-constraints.yaml.bak.*
│
├── rules/
│   ├── controlled-vocabularies.md
│   ├── layout-expansion-rules.md
│   ├── output-template.yaml
│   ├── quality-checklist.md
│   └── extensions/
│       ├── skill.md
│       ├── output-template.yaml
│       ├── layout-expansion-rules.md
│       └── README.md
│
├── outputs/
│   └── README.md
│
├── skill.md
└── README.md
🛠 How It Works
Provide a PPT outline (section titles, bullet points, or a full structure).

The skill expands each slide using:

Brand rules

Project constraints

Controlled vocabulary

Layout expansion rules

The skill outputs:

A complete design document

AI‑ready visual prompts

Version metadata

Revision logs

📦 Configuration
Brand Configuration (config/global-brand.yaml)
Define brand tone, color palette, typography, and visual identity.

Project Constraints (config/project-constraints.yaml)
Specify project‑level rules such as:

Required sections

Forbidden content

Compliance requirements

Layout restrictions

Controlled Vocabulary (rules/controlled-vocabularies.md)
Ensure consistent terminology across slides.

🧩 Extensions
The rules/extensions/ folder contains modular rule files that extend the skill’s behavior, including layout rules, output templates, and quality checklists.

📜 Versioning
The skill automatically manages:

Version numbers

Revision logs

Change history

This ensures traceability across iterations.

📄 License
MIT License (recommended for open-source distribution).

🤝 Contributions
Contributions, issues, and feature requests are welcome.
Feel free to open a PR or start a discussion.

> A Claude Code skill that turns a PPT outline into page-by-page design docs: full copy, visual structure, and an image-ready prompt for each slide, with versioning and a revision log.

**PPT Design Skill**
一个面向 **咨询解决方案类 PPT** 的逐页设计 Skill：把一份大纲，结合品牌配置、项目约束与受控词汇表，逐页细化为包含完整文案、视觉结构和可直接用于图像生成（image2）的中文视觉提示词的独立文档，并自动管理版本与修订日志。

> 注：文中 image2 为默认文生图模型，同样支持其它文生图大模型（如 Midjourney / Stable Diffusion / DALL·E 等），生成的视觉提示词可直接复用。

---

## ✨ 特性

- **逐页深度生成** — 每页只传达一个核心结论，视觉服务于逻辑，装饰让位于论证
- **约束驱动** — 颜色 ≤3 种、受控词汇表（页型/布局/图表/论证角色/密度 5 组枚举）强制校验
- **材料路由器** — 你是领域专家，每页指定参考文件或联网检索，Skill 负责读取、引用与引用溯源
- **可直接出图** — 每页输出独立 MD，含可直接复制粘贴到 image2 的中文视觉 prompt
- **版本可追溯** — `_v1 / _v2` 版本递增，旧版保留，统一 `revision-log.md` 修订日志
- **质量自检** — 17 项检查点，最多两轮自动修正，阻断项明确标注

---

## 🚀 快速开始

### 1. 填写品牌配置（必填）

复制并修改 `config/global-brand.yaml`，填写品牌颜色、字体与视觉风格：

```yaml
# config/global-brand.yaml（示例见 global-brand.example.yaml）
brand:
  company_name: "某物流科技平台"
  logo_position: "右上角"
  logo_size: "宽120px"

color_palette:
  primary: "#0033A0"      # 主色
  secondary: "#00B5E2"    # 辅助色
  accent: "#E87722"       # 强调色
  # ...
```

### 2. （可选）填写项目约束

在 `config/project-constraints.yaml` 中声明本项目的禁止项、必须项、受众与叙事结构。

### 3. 启动 Skill

在 Claude Code 中：

```
请按照 ppt-design-skill/skill.md 中定义的流程，帮我设计一套PPT方案。
```

### 4. 提供大纲

把你的 PPT 大纲粘贴给 Skill，格式不限 —— 简单的章节 + 页码列表，或详细的每页概要均可。

### 5. 逐页讨论 → 出图

Skill 逐页生成独立 MD 文件，`outputs/` 下每个项目一个文件夹。

---

## 💬 交互指令

| 指令 | 行为 |
|------|------|
| `读 02-准入管理.md 05-合规摘要.md` | 读取指定文件作为本页参考材料 |
| `跳过材料` | 纯逻辑页，基于大纲与全局配置直接生成 |
| `联网查 2026年物流行业趋势` | 联网检索并标注来源 URL |
| `继续` / `下一页` | 沿用上一页配置进入下一页 |
| `先生成，缺的标待补充` | 快速通道，缺失处标记 `[待补充]` |
| `修改 P15 把冻结路径箭头改强调色` | 重生成该页，版本递增、保留旧版 |
| `重做 P12` / `跳过本页` | 重做或跳过指定页 |
| `查看进度` | 展示已生成 / 待生成页面清单 |

---

## 📁 目录结构

```
ppt-design-skill/
├── skill.md                          # Skill 执行指令
├── README.md                         # 本文件
├── config/
│   ├── global-brand.yaml             # ★ 必填：品牌配置
│   ├── global-brand.example.yaml     #   配置示例
│   └── project-constraints.yaml      # 可选：项目约束
├── rules/
│   ├── controlled-vocabularies.md    # 受控词汇表（5 组枚举）
│   ├── output-template.yaml          # 输出模板（7 字段组）
│   ├── layout-expansion-rules.md     # 展开规则
│   ├── quality-checklist.md          # 质量清单（17 项）
│   └── extensions/                   # 预留：其他 PPT 类型扩展
└── outputs/                          # ★ 生成产物
    └── 2026-06-06_XX项目/
        ├── P01_封面_v1.md
        ├── P02_执行摘要_v1.md
        ├── P15_准入管理方案_v2.md     # v2 = 修订版
        └── revision-log.md
```

---

## 🔧 扩展其他 PPT 类型

`rules/extensions/` 预留给产品发布、年终汇报、融资路演等类型。在该目录下创建子文件夹，放入对应的受控词汇表和展开规则即可，无需修改核心规则文件。

---

## ❓ FAQ

**Q：为什么每页都要我指定参考文件？**
你比任何算法都更清楚什么文件适合什么页面。指定文件只需几秒，却能大幅提升生成精度。

**Q：可以一次指定多页的材料吗？**
不建议。本 Skill 设计为逐页深度讨论，每页的逻辑与视觉都需独立推敲，批量模式会牺牲质量。

**Q：生成的 image2 prompt 为什么是中文？**
便于查看与微调。如需英文 prompt，可在 `layout-expansion-rules.md` 中自行切换。

**Q：版本号如何管理？**
初版 `_v1`，每次修改版本号递增，旧版本不删除，修改记录统一在 `revision-log.md`。
