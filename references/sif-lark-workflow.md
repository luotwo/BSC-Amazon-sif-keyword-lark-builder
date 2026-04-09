# Sif 关键词表 → 飞书交付物工作流

## 适用场景

当用户提供的是 Sif 关键词调研 Excel，而不是亚马逊广告后台 Search Term / Campaign / Keyword / Placement 报表时：
- 可输出投放优化分析
- 可输出 Campaign / Ad Group / Keyword / Negative Keyword 结构建议
- 不可直接给出真实 ACOS、ROAS、CTR、CPC、CVR 结论

## 推荐内容骨架

1. 分析结论
2. 重点机会词
3. 建议广告结构
4. 建议否词池
5. 预算建议
6. 7天优化规则
7. 执行顺序
8. 可执行投放清单
9. 下一步建议

## 推荐 Base 表结构

### 分析结论
字段：
- 模块
- 内容

### 重点机会词
字段：
- 分类
- 关键词
- 匹配方式
- 建议竞价

### 建议广告结构
字段：
- Campaign
- 目标
- 关键词
- 设置

### 建议否词池
字段：
- 分类
- 否词

### 预算与优化规则
字段：
- 模块
- 内容

### 可执行投放清单
字段：
- Campaign
- Ad Group
- 关键词
- 匹配方式
- 建议竞价
- 备注

## 已验证的关键经验

### 1. Base 创建
- 使用 `lark-cli base +base-create`
- 若返回 URL，应直接回传给用户

### 2. 字段创建
- `type` 用字符串枚举，如 `text`
- 不要使用数字字段码

### 3. 记录写入
- `+record-upsert --json` 直接传字段对象
- 不要嵌套 `fields`

### 4. Dashboard 主题
- 使用允许值，如 `default`、`SimpleBlue`
- 不要使用 `light`

### 5. Dashboard block data_config
- `group_by` 必须是数组
- `count_all` 与 `series` 互斥
- 涉及 filter 时，遵循标准结构：

```json
{
  "filter": {
    "conjunction": "and",
    "conditions": [
      {"field_name":"分类","operator":"is","value":"高优先级否词"}
    ]
  }
}
```

## 推荐交付口径

给用户返回时，建议汇总：
- 飞书文档标题 / 链接
- Base 链接
- Dashboard ID / 名称
- 是否生成 CSV
- 若未生成真实广告指标，提醒原因
