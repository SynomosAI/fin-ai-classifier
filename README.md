# fin-ai-classifier

> **状态：RESERVED（占位 · 开放认领）** — 本仓已按平台协议规范建好行业接入四件套骨架，
> 等待具备本域资质的运营方认领并填充真实规则。

把「这个金融 AI 应用属于哪一级风险、要配哪些义务」拆成可核验的属性，让 AI 只做分级提示，不做合规结论。

## 这个域管什么

金融场景 AI 应用风险分级与义务映射

金融 AI 覆盖信贷、保险、投顾、反洗钱等场景，风险差异极大。AI 能做的是按场景与影响把风险等级与对应义务摆清楚，合规认定须由机构与监管完成。

## 域标识

| 项 | 值 |
|---|---|
| 域 ID | `fin`（全局唯一，一经分配不复用） |
| 域名称 | 金融 · AI 应用风险分级 |
| Profile 版本 | `domain/1.0` |
| 当前状态 | `RESERVED` |
| 占位时间 | 2026-09-12 |

## 属性清单

| 属性键 | 类型 | 说明 |
|---|---|---|
| `fin.risk_class` | enum | 风险分级，区分用途参照分级治理通行做法 · 取值 minimal/limited/high/unacceptable/undetermined |
| `fin.use_case_type` | enum | 应用场景，决定风险基线与叠加义务 · 取值 credit_decision/insurance_underwriting/investment_advice/aml_monitoring/customer_service/internal_ops/other |
| `fin.human_oversight` | enum | 人工监督强度 · 取值 none/post_hoc/in_the_loop/human_decides |
| `fin.disclosure_obligation` | boolean | 是否需向客户披露 AI 参与情况 |

## 本域红线（不可逾越，机器可读）

1. 不生成任何面向客户的投资建议、产品推荐或买卖结论
2. 不得输出「已合规」「监管已认可」类结论性表述
3. 高风险类应用须人工复核，AI 不得单独给出可上线结论

> 红线在 `gate-map.json` 中均有对应阻断规则。平台校验器会检查「每条红线都有规则覆盖」，
> 缺失即校验失败——**制度与系统不允许不同步**。

## 行业接入四件套

| 文件 | 作用 |
|---|---|
| `domain.manifest.json` | 本域声明：属性清单、签发方要求、有效期、红线 |
| `gate-map.json` | 本域「什么动作要多少摩擦」：silent / warn / confirm / block / require-owner |
| `privacy.json` | 本域隐私声明：默认关闭、最小必要、可撤回、可删除 |
| `checker` | 本域核验器（MCP 工具，**只出示核验，不下判定**） |

## 核心原则

**平台只当擂台，不当货架。** 本域的核验器只回答「这条声明是否可核验、缺什么要件」，
不回答「这件事是否合规、该不该做」。判定权在本域的资质方、监管方与人。

**隐私是准入条件，不是整改事项。** 缺失 `privacy.json` 或任一必填字段不符，
符合性校验直接失败——不是警告，是拒绝接入。

## 参考依据

- 生成式人工智能服务管理暂行办法
- 中国人民银行人工智能算法金融应用评价规范（参照）
- 金融机构人工智能应用监管指引（参照）

> 上列依据仅用于说明本域属性的来源与口径，不构成法律意见。具体适用以现行有效文本与主管部门解释为准。

## 认领方式

本域面向具备相应资质的机构开放。认领后请：

1. Fork 本仓，填注 `operator` 与 `checker_endpoint`
2. 按本域现行有效规则校准属性取值与红线表述
3. 跑平台侧校验器自测（五项判据全过方可提交）
4. 提 PR，附资质证明与规则依据

## 许可与署名

代码与配置按 MIT 许可使用。文档的知识版权归 SynomosAI 所有。

© 2026 SynomosAI. All rights reserved.
