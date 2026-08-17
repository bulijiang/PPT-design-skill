# 布局 → image2 Prompt 展开规则（Layout Expansion Rules）

> **用途**：根据 `layout_type` 将结构化字段展开为 image2 可直接使用的中文视觉生成 prompt。
> **使用**：Phase 2 Step E 调用，按当前页的 `layout_type` 匹配对应规则，填充字段后输出。
> **原则**：展开规则是"填参模板"而非"自由创作"——GPT-5.5 的工作是模板参数替换，以保证 prompt 稳定可复现。

---

## R0: 全局页眉区（Global Header，所有规则通用）

> **用途**：所有布局规则均在页面顶部绘制统一页眉区，其余内容在页眉区下方布局。
> 页眉区不随 `layout_type` 改变，保证整份 PPT 视觉一致。

```
页眉区（页面顶部横栏，高度约占页面 12%，左右各留 8% 边距）：
- 左侧：主标题"{可见内容.headline}"，字体{品牌配置.typography.title_font}
  {品牌配置.typography.title_size}，颜色{品牌配置.color_palette.primary}，靠左对齐；
  副标题"{可见内容.subtitle}"紧跟主标题正下方，字体
  {品牌配置.typography.subtitle_font}{品牌配置.typography.subtitle_size}，
  颜色{品牌配置.color_palette.text_secondary}，靠左对齐
- 右侧：预留一个 Logo 占位空位置（宽约 120px，高约 40px，与页眉区垂直居中对齐），
  该位置不绘制任何 Logo 图形或文字，联友科技 Logo 由用户后续统一手动粘贴
```

---

## R1: `left_text_right_graph` — 左文右图

```
一张专业的咨询方案PPT页面，{品牌配置.color_palette.primary}与
{品牌配置.color_palette.secondary}配色方案，{品牌配置.color_palette.background}背景。

页眉区按 R0 全局页眉区规范（左侧主标题+副标题，右侧 Logo 占位空位）。

页眉区下方，页面左侧占{视觉结构.spatial_split.left_ratio}：
- 正文内容使用{品牌配置.typography.body_font}{品牌配置.typography.body_size}，
  行高{品牌配置.typography.line_height}，颜色{品牌配置.color_palette.text_primary}：
  · {逐条列出可见内容.body_text}
- 底部强调文字"{可见内容.bottom_line}"，颜色{品牌配置.color_palette.accent}

页面右侧占{视觉结构.spatial_split.right_ratio}：
- {视觉结构.chart_modules[0].chart_type}，展示{视觉结构.chart_modules[0].data_description}
- 图表主色调用{品牌配置.color_palette.primary}，辅助元素用
  {品牌配置.color_palette.secondary}
- 关键数据点"{视觉结构.chart_modules[0].emphasis_point}"使用
  {品牌配置.color_palette.accent}色突出显示
- 图表轴标签使用{品牌配置.typography.label_font}{品牌配置.typography.label_size}

右下角页码{页面元信息.page_number}，字体{品牌配置.typography.label_font}
{品牌配置.typography.label_size}，颜色{品牌配置.color_palette.text_secondary}。

整体风格：{逐项列出品牌配置.visual_style.keywords}。
留白充足，无多余装饰元素。专业咨询级设计品质。
严禁绘制以下内容：{逐条列出优先级.do_not_render}
以下内容必须清晰可见：{逐条列出优先级.must_show}
```

---

## R2: `top_title_bottom_2col` — 上标题下双栏

```
一张专业的咨询方案PPT页面，{品牌配置.color_palette.primary}与
{品牌配置.color_palette.secondary}配色方案，{品牌配置.color_palette.background}背景。

页眉区按 R0 全局页眉区规范（左侧主标题+副标题，右侧 Logo 占位空位）。

页眉区下方，等分为2栏：
左栏内容：
- {展示body_text的前半部分或第一组内容}
右栏内容：
- {展示body_text的后半部分或第二组内容}
两栏之间用细线或适当间距分隔，栏内文字使用{品牌配置.typography.body_font}
{品牌配置.typography.body_size}，行高{品牌配置.typography.line_height}。

右下角页码{页面元信息.page_number}。

整体风格：{品牌配置.visual_style.keywords}。栏间分隔清晰但克制。
严禁绘制：{优先级.do_not_render}
必须可见：{优先级.must_show}
```

---

## R3: `center_hub_spokes` — 中心辐射式

```
一张专业的咨询方案PPT页面，{品牌配置.color_palette.primary}与
{品牌配置.color_palette.secondary}配色方案，{品牌配置.color_palette.background}背景。

页眉区按 R0 全局页眉区规范，标题使用"{页面元信息.page_title}"、副标题"{可见内容.subtitle}"，右侧 Logo 占位空位。

页面中心：一个圆形枢纽节点，标注"{可见内容.headline}"，颜色
{品牌配置.color_palette.primary}填充，白色文字，字体{品牌配置.typography.subtitle_font}
{品牌配置.typography.subtitle_size}。

从中心向外辐射{N}条连接线（颜色{品牌配置.color_palette.secondary}，1.5pt），
每条线的末端连接一个圆角矩形卡片：
{逐卡描述：卡片标题 + 简短描述}
卡片白色背景，{品牌配置.color_palette.primary}色1pt边框。
卡片内文字使用{品牌配置.typography.body_font}{品牌配置.typography.body_size}。

整体风格：清晰的架构图美学。{品牌配置.visual_style.keywords}。
严禁绘制：{优先级.do_not_render}
必须可见：{优先级.must_show}
```

---

## R4: `timeline_horizontal` — 横向时间轴

```
一张专业的咨询方案PPT页面，{品牌配置.color_palette.primary}与
{品牌配置.color_palette.secondary}配色方案，{品牌配置.color_palette.background}背景。

页眉区按 R0 全局页眉区规范（左侧主标题+副标题，右侧 Logo 占位空位）。

页面中部：一条横向时间轴，{N}个里程碑节点由实线连接，线条颜色
{品牌配置.color_palette.primary}，2pt粗细。每个里程碑包含：
- 圆形节点（直径12px），{品牌配置.color_palette.primary}色填充
- 节点上方：阶段名称，字体{品牌配置.typography.label_font}{品牌配置.typography.label_size}
- 节点下方：时间标签，颜色{品牌配置.color_palette.text_secondary}
- 垂直描述卡片，内容使用{品牌配置.typography.body_font}{品牌配置.typography.body_size}
当前/最新阶段节点使用{品牌配置.color_palette.accent}色填充，略大于其他节点。

时间轴节点内容：{逐节点列出阶段名称+时间+关键描述}

整体风格：清晰的路线图美学。{品牌配置.visual_style.keywords}。
严禁绘制：{优先级.do_not_render}
必须可见：{优先级.must_show}
```

---

## R5: `comparison_table` — 对比表格

```
一张专业的咨询方案PPT页面，{品牌配置.color_palette.primary}与
{品牌配置.color_palette.secondary}配色方案，{品牌配置.color_palette.background}背景。

页眉区按 R0 全局页眉区规范（左侧主标题+副标题，右侧 Logo 占位空位）。

页面中部：一张{N}列{M}行的对比表格：
- 表头行：{品牌配置.color_palette.primary}色背景，白色文字，
  字体{品牌配置.typography.subtitle_font}
- 数据行：白色与浅{品牌配置.color_palette.secondary}（5%透明度）交替底色
- 关键差异单元格：{品牌配置.color_palette.accent}色细边框高亮
- 所有文字使用{品牌配置.typography.body_font}{品牌配置.typography.body_size}

表格内容：{逐行描述对比维度与各列数据或结论}

整体风格：清晰的数据呈现。{品牌配置.visual_style.keywords}。
严禁绘制：{优先级.do_not_render}
必须可见：{优先级.must_show}
```

---

## R6: `grid_cards_2x2` / `grid_cards_3x2` — 卡片矩阵

```
一张专业的咨询方案PPT页面，{品牌配置.color_palette.primary}与
{品牌配置.color_palette.secondary}配色方案，{品牌配置.color_palette.background}背景。

页眉区按 R0 全局页眉区规范（左侧主标题+副标题，右侧 Logo 占位空位）。

主体区域：{rows}行×{columns}列的卡片网格，间距均匀（16-20px）：
- 每张卡片：白色背景，轻微阴影（2px模糊，10%透明度），4px圆角
- 卡片顶部：小图标（{品牌配置.color_palette.primary}色）+ 卡片标题，
  字体{品牌配置.typography.subtitle_font}{品牌配置.typography.subtitle_size}
- 卡片正文：描述文字，字体{品牌配置.typography.body_font}
  {品牌配置.typography.body_size}，颜色{品牌配置.color_palette.text_primary}
- 如有关键数据：在卡片中用{品牌配置.color_palette.accent}色大数字展示

卡片内容：{逐卡描述标题+正文+数据}

整体风格：现代卡片式布局。{品牌配置.visual_style.keywords}。
严禁绘制：{优先级.do_not_render}
必须可见：{优先级.must_show}
```

---

## R7: `data_dashboard` — 数据仪表盘

```
一张专业的咨询方案PPT页面，{品牌配置.color_palette.primary}与
{品牌配置.color_palette.secondary}配色方案，{品牌配置.color_palette.background}背景。

页眉区按 R0 全局页眉区规范（左侧主标题+副标题，右侧 Logo 占位空位）。

主体区域：仪表盘布局，{N}个数据可视化面板按清晰网格排列：
{逐模块描述每个chart_module的图表类型、数据内容和面板位置}

关键指标以大数字展示（字体{品牌配置.typography.title_font}，
字号比标题大4pt），颜色{品牌配置.color_palette.primary}，
单位标签使用{品牌配置.typography.label_font}放在数字下方。
最关键的指标用{品牌配置.color_palette.accent}色突出。

所有图表统一使用{品牌配置.color_palette.primary}/
{品牌配置.color_palette.secondary}配色。网格线最少化，浅灰色。

整体风格：高管仪表盘美学。{品牌配置.visual_style.keywords}。
严禁绘制：{优先级.do_not_render}
必须可见：{优先级.must_show}
```

---

## R8: `single_column_centered` — 居中单栏

```
一张专业的咨询方案PPT页面，{品牌配置.color_palette.primary}与
{品牌配置.color_palette.secondary}配色方案，{品牌配置.color_palette.background}背景。

页眉区按 R0 全局页眉区规范，标题使用"{页面元信息.page_title}"、副标题"{可见内容.subtitle}"，右侧 Logo 占位空位。

页面正中央（水平垂直居中，页眉区下方）：
- 大字标题"{可见内容.headline}"，字体{品牌配置.typography.title_font}，
  比标准标题大8pt，颜色{品牌配置.color_palette.primary}，居中
- {如有key_metrics}一个超大数字"{key_metrics[0].value}"，
  字体{品牌配置.typography.title_font} 72pt，
  颜色{品牌配置.color_palette.accent}，居中
- 下方辅助说明"{body_text[0]}"，字体{品牌配置.typography.body_font}
  {品牌配置.typography.body_size}，颜色{品牌配置.color_palette.text_secondary}，居中

中央内容块周围最大限度留白。无边线、无卡片、无装饰线条。极致极简。

整体风格：极简高冲击力声明页。{品牌配置.visual_style.keywords}。
严禁绘制：{优先级.do_not_render}
必须可见：{优先级.must_show}
```

---

## R9: `pyramid_hierarchy` — 金字塔层级

```
一张专业的咨询方案PPT页面，{品牌配置.color_palette.primary}与
{品牌配置.color_palette.secondary}配色方案，{品牌配置.color_palette.background}背景。

页眉区按 R0 全局页眉区规范（左侧主标题+副标题，右侧 Logo 占位空位）。

页面中右：一个由{N}层水平条堆叠而成的金字塔三角形，底部最宽，顶部最窄：
- 底层（基础）：最宽横条，{品牌配置.color_palette.primary}色20%透明度填充，
  标签字体{品牌配置.typography.subtitle_font}
- 中间层：逐层变窄，{品牌配置.color_palette.primary}色透明度递增（40%→60%→80%）
- 顶层（塔尖）：最窄横条，{品牌配置.color_palette.primary}色实心填充，
  标签用{品牌配置.color_palette.accent}色突出
每层左侧标注简短说明，字体{品牌配置.typography.body_font}
{品牌配置.typography.body_size}，颜色{品牌配置.color_palette.text_secondary}。

金字塔层级内容：{逐层描述名称+说明}

整体风格：战略咨询层级图美学。{品牌配置.visual_style.keywords}。
严禁绘制：{优先级.do_not_render}
必须可见：{优先级.must_show}
```

---

## R10: `process_flow_horizontal` / `process_flow_vertical` — 流程图

```
一张专业的咨询方案PPT页面，{品牌配置.color_palette.primary}与
{品牌配置.color_palette.secondary}配色方案，{品牌配置.color_palette.background}背景。

页眉区按 R0 全局页眉区规范（左侧主标题+副标题，右侧 Logo 占位空位）。

页面中部：一条{横向/纵向}流程线，{N}个步骤由箭头串联：
- 每个步骤：圆角矩形（12px圆角），{品牌配置.color_palette.primary}色85%不透明度填充，
  白色文字，字体{品牌配置.typography.subtitle_font}{品牌配置.typography.subtitle_size}
- 步骤间箭头：{品牌配置.color_palette.secondary}色，实心三角形箭头
- 每个步骤下方：简短描述，字体{品牌配置.typography.body_font}
  {品牌配置.typography.body_size}，颜色{品牌配置.color_palette.text_secondary}，居中
- 当前/活跃步骤：{品牌配置.color_palette.accent}色填充，白色文字，略大于其他步骤

流程步骤内容：{逐步骤列出名称+描述}

整体风格：清晰的流程可视化。{品牌配置.visual_style.keywords}。
严禁绘制：{优先级.do_not_render}
必须可见：{优先级.must_show}
```
