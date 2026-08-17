# 规则扩展目录

本目录预留给其他 PPT 类型的受控词汇表和展开规则。

## 计划支持的类型

- 产品发布类 PPT
- 年终总结/汇报类 PPT
- 融资路演类 PPT
- 学术/技术分享类 PPT

## 扩展方式

每种新类型在 `extensions/` 下创建独立子目录，包含：

```
extensions/
├── 产品发布/
│   ├── controlled-vocabularies.md    # 该类型的页型/布局/图表枚举
│   ├── layout-expansion-rules.md     # 该类型的展开规则
│   └── quality-checklist.md         # 该类型的自检清单（可选）
├── 年终汇报/
│   └── ...
```

扩展时不需要修改核心 `rules/` 文件，Skill 根据项目类型按需加载对应规则包。

---

> **当前状态**：仅支持「咨询解决方案类 PPT」。其他类型待后续开发。
