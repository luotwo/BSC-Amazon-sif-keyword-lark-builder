# BSC-Amazon-sif-keyword-lark-builder

把 **Sif 关键词调研 Excel** 快速整理成可执行交付物：
- 飞书文档
- 飞书多维表格（Base）
- 飞书仪表盘（Dashboard）
- 可选：亚马逊广告后台可导入 CSV

适合新手直接使用。

---

## 适用场景

当你拿到的是 **Sif 关键词调研表**，而不是亚马逊广告后台的 Search Term / Campaign / Keyword / Placement 报表时，用这个 skill 最合适。

它会：
- 识别这是关键词调研表，不误判成广告报表
- 生成广告投放优化分析
- 输出飞书文档、Base、Dashboard
- 在最终产出前主动询问你是否生成 Amazon CSV

---

## 安装

### 1. GitHub 仓库

仓库地址：

`https://github.com/luotwo/BSC-Amazon-sif-keyword-lark-builder`

如果你需要下载源码或查看最新版本，优先从这个 GitHub 仓库进入。

### 2. 目录方式

GitHub 目录：

`https://github.com/luotwo/BSC-Amazon-sif-keyword-lark-builder/tree/main`

适合支持“从目录加载 skill”的环境。

### 3. 新手安装步骤

如果你是第一次接触，按这个顺序操作最稳：

1. 先确认你本机能正常打开 Claude Code / Claude CLI
2. 打开仓库：
   - `https://github.com/luotwo/BSC-Amazon-sif-keyword-lark-builder`
3. 下载源码（Code → Download ZIP）或用 git clone 拉取仓库
4. 在你的 Claude Code 环境里按目录导入这个 skill
5. 导入完成后，重新开一个新会话测试触发
6. 直接复制“快速开始”里的示例提问进行测试

如果你的环境后续支持 `.skill` 安装包，也可以再补充发布安装包。

---

## 使用前准备

请先确认：

- 已安装并可使用 Claude Code / Claude CLI
- 本机可执行 `python`
- 已安装 `lark-cli`
- `lark-cli` 已完成飞书认证
- 已准备好一份 Sif 关键词调研 Excel

准备好你自己的 Sif 关键词调研 Excel 文件，后续使用时把实际文件路径发给 Claude 即可。

---

## 快速开始

直接给 Claude 发送类似下面的话：

```text
我这边有个 Sif 关键词调研 Excel，需要你帮我整理成飞书文档、飞书多维表格和分析仪表盘。我先把文件路径发你，你再开始。
```

或者：

```text
参考 Sif 关键词模板，给我做一个运营可执行的投放监控版，飞书 Base 和 dashboard 都要。
```

如果你还想生成可导入亚马逊后台的 CSV，等 skill 询问时直接回复：

```text
要
```

如果暂时不要，就回复：

```text
先不用
```

---

## 标准输出

正常情况下会产出：

- 飞书文档链接
- 飞书 Base 链接
- 分析版 Dashboard 名称或 ID
- 运营监控版 Dashboard 名称或 ID
- 如果你确认生成 CSV，还会返回本地 CSV 文件路径

---

## 第一次操作步骤

如果你是第一次跑，建议按下面顺序：

1. 打开 Claude Code / Claude CLI
2. 确认 skill 已安装或已加载
3. 准备好你的 Sif Excel 路径
4. 复制“快速开始”里的示例提问发给 Claude
5. 等它分析后，回答是否生成 CSV
6. 等待返回飞书链接、Base 链接、Dashboard 信息和 CSV 路径

如果第一次只是想验证流程，建议先回答：

```text
先不用
```

先只看飞书文档、Base 和 Dashboard 是否创建成功。

---

## 重要说明

Sif 关键词调研表不是广告后台报表。

所以这个 skill 可以输出：
- 投放优化建议
- Campaign / Ad Group / Keyword 结构建议
- 否词池建议
- 预算建议
- 执行清单

但不能直接计算真实广告指标，例如：
- ACOS
- ROAS
- CTR
- CPC
- CVR

如果你还要这些真实指标诊断，需要额外提供广告后台报表。

---

## 排错指南

### 1. 没有触发 skill

优先检查你的提问里是否明确出现这些信息：
- Sif 关键词调研表 / 关键词调研 Excel
- 飞书文档 / 飞书 Base / 飞书仪表盘
- 广告投放优化 / 投放监控 / CSV

建议直接用“快速开始”里的示例提问。

### 2. 飞书创建失败

优先检查：
- `lark-cli` 是否可用
- 飞书账号是否已认证
- 当前账号是否有文档、Base、Dashboard 权限
- 是否缺少飞书开放平台 scope

### 3. 只想出飞书，不想出 CSV

当 skill 询问时，直接回答：

```text
不要
```

或：

```text
先不用
```

### 4. 只有 Excel，没有广告后台报表

可以正常使用。

这是这个 skill 的主要场景之一。

### 5. 想继续做真实 ACOS / ROAS 诊断

补充提供这些报表之一即可：
- Search Term
- Campaign
- Keyword
- Placement

---

## 文件位置

GitHub 根目录：

`https://github.com/luotwo/BSC-Amazon-sif-keyword-lark-builder/tree/main`

主要文件：

- `https://github.com/luotwo/BSC-Amazon-sif-keyword-lark-builder/blob/main/SKILL.md`
- `https://github.com/luotwo/BSC-Amazon-sif-keyword-lark-builder/blob/main/README.md`
- `https://github.com/luotwo/BSC-Amazon-sif-keyword-lark-builder/blob/main/references/sif-lark-workflow.md`
- `https://github.com/luotwo/BSC-Amazon-sif-keyword-lark-builder/blob/main/evals/evals.json`
- `https://github.com/luotwo/BSC-Amazon-sif-keyword-lark-builder`

---

## 一句话

如果你有一份 **Sif 关键词调研 Excel**，想快速生成 **飞书文档 + 飞书 Base + 飞书仪表盘 + 可选 Amazon CSV**，直接把 Excel 路径发给 Claude 即可。
如果需要了解，共创，学习相关亚马逊运营Skill，请添加我们公众号和相关联系方式，进行分享相关亚马逊相关运营Skill源文件
![9f453825a605ac5a92149be126636dc4](https://github.com/user-attachments/assets/9680fd49-0f0f-4642-8601-462ca28f1c77)
![微信图片_20260409165035_4249_87](https://github.com/user-attachments/assets/16305816-7646-416e-9c37-e132bd592fa7)
---<img width="844" height="376" alt="image" src="https://github.com/user-attachments/assets/0c809a29-8dad-4fd0-b5ce-d439e250a60a" />


