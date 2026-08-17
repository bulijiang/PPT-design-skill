# 受控词汇表（Controlled Vocabularies）

> **用途**：所有 `page_type`、`layout_type`、`chart_type`、`narrative_role`、`density` 字段必须从此表中选择。
> **原则**：不使用自由文本描述这些关键字段，以保证 GPT-5.5 输出的稳定性和一致性。
> **扩展**：如需新增枚举值，在对应表格末尾追加一行，并同步更新 `layout-expansion-rules.md`。

---

## 1. 页型（page_type）

| 枚举值 | 中文名 | 说明 |
|--------|--------|------|
| `cover` | 封面页 | 项目名称、客户名称、日期、一句话价值主张 |
| `executive_summary` | 执行摘要 | 3-5个核心结论提炼，30秒可读完 |
| `toc` | 目录页 | 章节导航，当前章节高亮 |
| `section_divider` | 章节分隔页 | 章节标题 + 一句话概括本章价值 |
| `context_trend` | 背景与趋势 | 行业宏观环境、竞争格局、技术趋势 |
| `pain_point` | 痛点诊断 | 客户现状问题分析，数据+根因 |
| `insight` | 核心洞察 | 从数据/调研中提炼的独到见解 |
| `solution_overview` | 方案总览 | 解决方案的整体架构图 |
| `solution_detail` | 方案详解 | 某个模块的深入展开 |
| `value_proposition` | 价值主张 | 方案为客户带来的具体价值（量化） |
| `roadmap` | 实施路线图 | 分阶段的落地计划 |
| `case_study` | 案例举证 | 过往成功案例，Before/After 对比 |
| `team` | 团队资质 | 核心团队成员与经验 |
| `investment` | 投资回报 | ROI 分析、成本效益对比 |
| `risk_mitigation` | 风险与保障 | 潜在风险与应对措施 |
| `next_steps` | 下一步行动 | 具体合作推进步骤与时间节点 |
| `thank_you` | 致谢页 | 联系方式 + 感谢语 |
| `appendix` | 附录 | 补充数据、方法论说明 |

---

## 2. 布局类型（layout_type）

| 枚举值 | 说明 | 适用场景 |
|--------|------|---------|
| `left_text_right_graph` | 左文右图（40/60 分割） | 观点+数据证据、结论+图示支撑 |
| `right_text_left_graph` | 左图右文（60/40 分割） | 视觉主导的页面，图表先行 |
| `top_title_bottom_2col` | 顶部标题，下方双栏 | 对比分析、两个并列观点 |
| `top_title_bottom_3col` | 顶部标题，下方三栏 | 三个并列要点或模块 |
| `center_hub_spokes` | 中心辐射式 | 核心概念向外展开，架构总览 |
| `timeline_horizontal` | 横向时间轴 | 发展历程、路线图 |
| `pyramid_hierarchy` | 金字塔层级 | 从基础到顶层的能力/需求分层 |
| `process_flow_horizontal` | 横向流程图 | 步骤清晰的过程描述 |
| `process_flow_vertical` | 纵向流程图 | 自上而下的流程 |
| `comparison_table` | 对比表格 | 多维度方案对比 |
| `data_dashboard` | 数据仪表盘 | 多 KPI 指标展示 |
| `grid_cards_2x2` | 2×2 卡片矩阵 | 四个并列模块 |
| `grid_cards_3x2` | 3×2 卡片矩阵 | 六个并列要点 |
| `full_bleed_image` | 满版图片 + 文字叠加 | 冲击力强，案例/愿景页 |
| `single_column_centered` | 居中单栏 | 核心结论聚焦，极简 |
| `icon_list` | 图标+文字列表 | 要点罗列，图标增强记忆 |

---

## 3. 图表/可视化类型（chart_type）

| 枚举值 | 说明 |
|--------|------|
| `bar_horizontal` | 横向柱状图（适合长标签对比） |
| `bar_vertical` | 纵向柱状图 |
| `bar_stacked` | 堆叠柱状图（展示构成） |
| `line_chart` | 折线图（趋势） |
| `pie_donut` | 饼图/环形图（占比） |
| `radar` | 雷达图（多维度评估） |
| `scatter_bubble` | 散点图/气泡图（相关性） |
| `waterfall` | 瀑布图（增减变化） |
| `gantt` | 甘特图（项目排期） |
| `architecture_diagram` | 架构拓扑图（系统/方案架构） |
| `process_diagram` | 流程示意图 |
| `comparison_table` | 对比表格 |
| `icon_matrix` | 图标矩阵 |
| `number_callout` | 大数字+说明（KPI 强调） |
| `quotation` | 引用/金句展示 |
| `timeline` | 时间线 |
| `venn_diagram` | 韦恩图（交集关系） |
| `funnel` | 漏斗图（转化） |
| `heatmap` | 热力图（密度分布） |

---

## 4. 论证角色（narrative_role）

| 枚举值 | 说明 |
|--------|------|
| `premise` | 前提/背景设定 — 建立共识基础 |
| `evidence` | 证据/数据支撑 — 用事实强化论证 |
| `insight` | 洞察提炼 — 从数据中得出独到判断 |
| `counter_argument` | 反面论证 — 预判并回应质疑 |
| `conclusion` | 结论/判断 — 推导出核心观点 |
| `transition` | 过渡/衔接 — 连接两个论证段落 |
| `call_to_action` | 行动号召 — 推动决策 |

---

## 5. 信息密度（density）

| 枚举值 | 说明 | 字数参考 |
|--------|------|---------|
| `sparse` | 极简，1 个核心信息 + 1 个视觉元素 | ≤ 30 字 |
| `moderate` | 适中，1 个结论 + 2-4 个支撑点 | ≤ 80 字 |
| `dense` | 信息密集型，多数据点并行展示 | ≤ 150 字 |
