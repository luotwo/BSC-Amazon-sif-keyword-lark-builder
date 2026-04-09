---
name: BSC-Amazon-sif-keyword-lark-builder
description: "当用户提到 Sif 关键词调研表、关键词调研 Excel、广告投放优化、要生成飞书多维表格/Base、飞书文档报告、飞书仪表盘，或要把关键词调研结果整理成可执行投放清单时，必须使用本 skill。它会先引导用户选择、上传或提供要分析的 Sif 关键词调研 Excel 文件，再基于关键词表生成广告投放优化分析，并产出飞书文档、飞书多维表格（Base）与仪表盘；同时必须询问用户是否还要生成可直接导入亚马逊广告后台调整的 CSV。"
metadata:
  requires:
    bins: ["python", "lark-cli"]
---

# BSC-Amazon-sif-keyword-lark-builder

开始前先阅读：
- `C:\Users\Administrator\.claude\skills\lark-shared\SKILL.md`
- `C:\Users\Administrator\.claude\skills\lark-base\SKILL.md`
- `C:\Users\Administrator\.claude\skills\lark-doc\SKILL.md`
- `references/sif-lark-workflow.md`

## 这个 skill 负责什么

把一份 Sif 关键词调研 Excel，转成可执行的广告投放分析交付物：
- 飞书文档报告
- 飞书多维表格（Base）
- 飞书仪表盘 / 运营监控版仪表盘
- 可选：亚马逊广告后台可导入 CSV

## 触发信号

出现以下任一类需求就应触发：
- 用户说“把这个关键词调研表做成飞书文档 / 多维表格 / 仪表盘”
- 用户说“基于 Sif 关键词表做广告投放优化方案”
- 用户说“生成可执行 campaign 结构、否词池、预算建议、监控面板”
- 用户说“顺便给我一份能导入亚马逊后台的 CSV”

## 输入要求

先确认用户是否已提供 Excel 文件。

若用户还没给文件，明确提示用户先选择、上传或提供要分析的 Sif 关键词调研 Excel 文件；可直接用下面这句：

`请先上传或提供你要分析的 Sif 关键词调研 Excel 文件路径，我再继续处理。`

如果用户已给出路径：
- 先读取并分析现有文件，不要反复追问
- 若文件不是广告后台报表，要明确说明无法直接计算真实 ACOS、ROAS、CTR、CPC、CVR，只能基于关键词相关性、搜索量、ABA、建议竞价、自然位竞争度给出优化方案

## 必做交互

在开始最终产出前，必须明确问用户一次：

`是否同时生成可直接导入亚马逊广告后台调整的 CSV？`

可接受的两类路径：
- 用户说“要” → 继续生成 CSV
- 用户说“不要 / 先不用” → 只生成飞书交付物

## 标准产出结构

默认至少产出以下内容：

### 1. 飞书文档
文档标题建议格式：
`《{产品或项目名} 广告投放优化方案（YYYY-MM-DD）》`

文档内容建议包含：
- 分析结论
- 重点机会词
- 建议广告结构
- 建议否词池
- 预算建议
- 7天优化规则
- 执行顺序
- 可执行投放清单
- 结尾下一步说明

### 2. 飞书多维表格（Base）
建议至少建这些表：
- `分析结论`
- `重点机会词`
- `建议广告结构`
- `建议否词池`
- `预算与优化规则`
- `可执行投放清单`

### 3. 飞书仪表盘
至少创建两类：
- 分析版仪表盘
- 运营可执行投放监控版

### 4. 可选 CSV
如果用户确认要生成，则输出：
- 可直接导入亚马逊广告后台的调整 CSV
- 若项目里已存在相同结构文件，优先复用既有列结构和命名风格

## 飞书 Base 执行规则

1. 创建 Base 时，优先使用：
- `lark-cli base +base-create`

2. 创建表时，使用：
- `lark-cli base +table-create`

3. 创建字段时，使用字符串类型枚举，不要用数字类型码。
正确示例：
- `{"field_name":"内容","type":"text"}`
错误示例：
- `{"field_name":"内容","type":1}`

4. 写记录时，`+record-upsert` 的 `--json` 必须直接传字段对象，不要包 `fields`。
正确示例：
- `{"模块":"分析说明","内容":"..."}`
错误示例：
- `{"fields":{"模块":"分析说明","内容":"..."}}`

5. 先分表再写记录，不要把所有分析塞进一个表。

## 飞书 Dashboard 执行规则

1. 创建 dashboard 用：
- `lark-cli base +dashboard-create`

2. `theme-style` 必须使用允许值，例如：
- `default`
- `SimpleBlue`
不要使用无效值如 `light`

3. 创建 block 前，先读：
- `C:\Users\Administrator\.claude\skills\lark-base\references\dashboard-block-data-config.md`

4. `group_by` 必须是数组对象，不是字符串。
正确示例：
- `"group_by":[{"field_name":"分类","mode":"integrated"}]`
错误示例：
- `"group_by":"分类"`

5. `count_all` 和 `series` 二选一，不能同时传。

## 推荐仪表盘组件

### 分析版
- 重点机会词分类占比
- 执行清单按 Campaign 分布
- 否词总数
- 机会词匹配方式分布
- 否词分类分布
- 执行清单总条数
- 广告结构目标分布

### 运营监控版
- 当前投放关键词总数
- 按 Campaign 监控投放量
- 按匹配方式监控分布
- 按备注监控优先级
- 否词池分类监控
- 高优先级否词总数
- 机会词分类监控
- 主推词数量

## 工作顺序

1. 确认 Excel 输入路径
2. 读取并分析关键词表
3. 生成本地分析内容
4. 询问是否生成亚马逊后台 CSV
5. 创建飞书文档
6. 创建飞书 Base
7. 建表、建字段、写记录
8. 创建分析版 dashboard
9. 创建运营监控版 dashboard
10. 如果用户确认，则生成 CSV
11. 返回所有关键链接、token、文件路径

## 回复要求

完成后回复应尽量直接，至少包含：
- 飞书文档链接
- Base 链接
- Dashboard 名称或 ID
- 若生成了 CSV，给出本地文件路径
- 如果 Excel 不是广告后台报表，明确提醒 ACOS / ROAS / CTR / CPC / CVR 属于推导外数据

## 不要做的事

- 不要跳过“是否生成 CSV”的询问
- 不要把 Dashboard data_config 写成错误结构
- 不要把 record-upsert 写成嵌套 `fields`
- 不要用数字字段类型码创建字段
- 不要把竞品词和核心词混在一个广告组策略里

## 示例触发

示例 1：
用户：`把这个 Sif 关键词表做成飞书多维表格和仪表盘，再看要不要出后台 CSV`

示例 2：
用户：`我有个关键词调研 Excel，想直接生成广告投放优化方案、飞书文档和 Base`

示例 3：
用户：`参考 Sif 模板，帮我做投放监控版，并且顺便问我要不要导出 Amazon CSV`
