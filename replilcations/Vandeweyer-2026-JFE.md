# 中文精要：Vandeweyer-2026-JFE

> Vandeweyer, Q., Yang, M., & Yannelis, C. (2026). Discount factors and monetary policy: Evidence from dual-listed stocks. Journal of Financial Economics, 175, 104190. [Link](https://doi.org/10.1016/j.jfineco.2025.104190) (rep), [PDF](https://bfi.uchicago.edu/wp-content/uploads/2024/06/BFI_WP_2024-64.pdf), [Google](<https://scholar.google.com/scholar?q=Discount factors and monetary policy: Evidence from dual-listed stocks>), [Replication](https://data.mendeley.com/datasets/vf2sj5z66j/2), [中文精要]()

- 该文的 readme.docx 文档写得非常细致，包括论文的复现说明、数据说明、代码说明等，值得学习借鉴。
- [Claude 对话](https://claude.ai/share/92f8507d-0483-4511-b248-4e59de0ff5c0)
- [提示词](https://github.com/lianxhcn/myprompt/blob/main/body/paper_notes.txt)


---

## 1. 简介

货币政策如何影响股票价格？这是金融学中的核心问题之一。传统研究通常将货币政策对股价的影响分解为两个渠道：一是通过影响企业未来现金流 (cash flow channel)，二是通过改变投资者的折现因子 (discount factor channel)。然而，在实证研究中，这两个渠道往往难以分离——因为货币政策公告通常会同时释放关于经济状况的信息，进而同时影响现金流预期和折现率。

本文提出了一种巧妙的识别策略来分离这两个渠道：利用在中国大陆 (A 股) 和香港 (H 股) 两地同时上市的股票。由于资本管制的存在，两地市场高度分割，同一公司的 A 股和 H 股价格可能出现显著差异。但关键在于，**这两种股票代表对同一现金流的索取权**——因此，任何因现金流预期变化导致的价格变动应该同时影响 A 股和 H 股。通过研究美国货币政策意外 (monetary policy surprises) 对 A/H 股价格比率的影响，作者成功剥离了现金流渠道，从而识别出纯粹的折现因子效应。

**主要发现**：

1. **显著的折现因子渠道**：100 个基点 (basis points, bp) 的意外降息会导致 A/H 价格比率下降约 30 个基点 (即 H 股相对 A 股上涨约 3%)，这一效应在 5 天内持续存在。

2. **非对称效应**：折现因子的调整主要由「周期放大型意外」(cycle-amplifying surprises) 驱动——即在宽松周期中的意外降息和在紧缩周期中的意外加息。而「周期矛盾型意外」(contradictory surprises，如紧缩周期中的降息) 则不产生显著效应。

3. **横截面异质性**：高 beta、小市值、低市盈率以及高滞后 A/H 比率的股票对货币政策意外更敏感，这与风险溢价调整的理论预测一致。

**计量方法**：

- 本文主要采用**事件研究法 (event study)** 和**双重差分 (difference-in-differences, DID)** 框架。
- 具体而言，作者使用 Kuttner (2001) 方法构建货币政策意外变量，然后检验这些意外如何影响 A/H 价格比率。
- 关键的识别假设是：在没有折现率变化的情况下，A/H 比率应该平稳演变——因为两者是对同一现金流的索取权。

---

## 2. 研究问题与制度背景

### 2.1 研究动机

货币政策通过何种机制影响资产价格？这个问题不仅关系到我们对金融市场运行机制的理解，也对货币政策的制定和传导具有重要意义。现有文献已经充分讨论了货币政策对现金流的影响 (通过总需求渠道)，但对折现因子渠道的研究却面临严重的识别难题。

为什么折现因子渠道难以识别？根本原因在于，货币政策公告往往伴随着关于经济状况的信息释放。例如，Fed 意外加息可能向市场传递「经济比预期更强劲」的信号，这会同时提高未来现金流预期和改变折现率。Nakamura and Steinsson (2018) 称之为「Fed 信息效应」(Fed information effect)。在这种情况下，单纯观察股价对货币政策的反应，很难区分哪部分来自现金流预期的变化，哪部分来自折现率的调整。

本文的核心贡献在于提供了一个**干净的识别策略**，能够剥离现金流渠道，从而单独识别折现因子效应。这一策略的关键在于利用 A-H 股的双重上市结构。

### 2.2 制度背景：A-H 股双重上市

#### 市场分割

中国大陆和香港维持着两个独立的股票市场体系：

- **大陆市场**：上海证券交易所 (SSE) 和深圳证券交易所 (SZSE)，发行 A 股 (以人民币计价，主要面向境内投资者) 和少量 B 股 (以外币计价)。

- **香港市场**：香港联合交易所 (SEHK)，中国大陆企业在此发行 H 股 (以港币计价)。

截至 2024 年底，共有 374 家中国企业在香港上市，其中部分同时在大陆发行 A 股。**对于这些双重上市的公司，A 股和 H 股代表对完全相同的现金流的索取权**——相同的投票权和分红权。

然而，由于中国严格的资本管制，两地市场高度分割：

- 大陆投资者无法直接购买 H 股
- 境外投资者进入 A 股市场面临诸多限制

这种分割导致 A 股和 H 股价格长期存在显著差异，A 股通常以溢价交易 (A/H 比率 > 1)。图 1 展示了 A/H 比率的时间序列变化。

#### 货币政策制度

**香港**：采用联系汇率制度 (Linked Exchange Rate System)，港币与美元挂钩 (汇率维持在 7.75-7.85 HKD/USD)。为维持固定汇率，香港金融管理局 (HKMA) 的政策利率紧跟美联储目标利率。

**中国大陆**：人民币实行有管理的浮动汇率制度，中国人民银行 (PBoC) 实施独立的货币政策。虽然 2005 年后汇率制度逐步灵活化，但 PBoC 仍通过外汇干预和资本管制维持相对稳定的汇率。

这种制度安排意味着：**美国货币政策意外会直接影响香港的利率 (进而影响 H 股投资者的折现率)，但对中国大陆的货币政策和 A 股投资者的折现率影响有限**。

---

## 3. 数据来源与变量界定

### 3.1 股票价格数据

**数据来源**：Wind 资讯数据库，涵盖 2000 年 6 月至 2024 年 9 月期间所有 A-H 股双重上市公司的日度收盘价。样本期内共有 143 只双重上市股票。

**关键变量构造**：

- $P_A$：A 股价格 (人民币)
- $P_H$：H 股价格 (港币)
- A/H 比率 = $P_A / (P_H \times \text{HKD/CNY 汇率})$

所有价格统一换算为人民币以消除汇率影响。

**样本构造**：围绕每次 FOMC 公告日，保留前后各 5 个交易日的观测值，构成事件研究样本。

### 3.2 货币政策意外 (Monetary Policy Surprises)

遵循 Kuttner (2001) 和 Bernanke and Kuttner (2005) 的方法，使用联邦基金期货价格变化来识别货币政策意外：

$$\text{Surprise}_s = \Delta \text{Target Rate}_s - E[\Delta \text{Target Rate}_s]$$

其中，$E[\Delta \text{Target Rate}_s]$ 通过当日联邦基金期货价格变化推算。

**样本期选择**：

- 基准样本：2000 年 6 月至 2024 年 9 月的 129 次 FOMC 公告
- 排除零利率下限 (Zero Lower Bound, ZLB) 时期：2008 年 12 月至 2015 年 12 月，以及 2020 年 3 月至 2022 年 3 月

表 2 列出了所有纳入分析的 FOMC 公告日期、目标利率变化和意外成分。

### 3.3 银行间利率数据

为验证美国货币政策对香港金融条件的传导，作者收集了以下利率数据：

- **HIBOR** (Hong Kong Interbank Offered Rate)：3 个月期港币银行间拆借利率及其期货价格
- **LIBOR** (以美元计价)：3 个月期美元 LIBOR (2000-2023)
- **SHIBOR** (Shanghai Interbank Offered Rate)：3 个月期人民币银行间拆借利率 (2006-2024)

**数据来源**：HKMA、Datastream 和 Bloomberg。

### 3.4 其他变量

**横截面特征变量** (用于异质性分析)：

1. **市盈率 (PE ratio)**：市值/年度盈利，滞后一年以避免内生性
2. **市值 (Market Capitalization)**：$\text{MC} = H\text{Shares} \times P_H + A\text{Shares} \times P_A$，滞后 3 个月
3. **CAPM Beta**：基于 5 年滚动窗口、月度收益率与上证综指收益率的回归系数
4. **滞后 A/H 比率**：滞后 3 个月的 A/H 价格比率

**美国出口份额数据** (用于稳健性检验)：从 FactSet GeoRev 获取各公司对美出口占比，用于检验现金流渠道是否影响结果。

**分析师盈利预测数据** (用于稳健性检验)：从 I/B/E/S 数据库获取香港和大陆分析师对同一公司的 EPS 预测，用于检验两地投资者的现金流预期是否存在系统性差异。

### 3.5 描述性统计

表 1 Panel A 展示了公司-公告层面的描述性统计 (8,496 个观测值)：

- A 股均价：15.99 元，中位数 7.06 元
- H 股均价：8.35 元 (折合人民币)，中位数 3.61 元  
- A/H 比率均值：2.34，中位数 1.82 (即 A 股平均较 H 股溢价 82%)

表 1 Panel B 展示了公告层面的统计 (129 次公告)：

- 目标利率均值：2.88%，中位数 2.25%
- 意外成分均值：-0.015 (即平均略偏向意外降息)
- HIBOR 与目标利率高度相关 (均值 2.68%)

---

## 4. 研究设计与识别策略

### 4.1 概念框架

考虑一个简化的资产定价模型。假设经济由两个地区 $A$ (大陆) 和 $H$ (香港) 组成，贸易一体化但金融市场完全分割。同一公司的股票在两地同时上市，代表对相同未来现金流 $E[x_i]$ 的索取权。

各地区投资者使用各自的折现因子 $R^A$ 和 $R^H$ 对现金流进行折现：

$$P_A^i = \frac{1}{R_A^i(m_A)} E[x_i(m_A, m_H)], \quad P_H^i = \frac{1}{R_H^i(m_H)} E[x_i(m_A, m_H)]$$

其中，$m_A$ 和 $m_H$ 分别代表两地的货币政策立场 (monetary policy stance)。

**关键洞察**：取两地股价的比率，现金流预期项约掉：

$$\frac{P_A^i}{P_H^i} = \frac{R_H^i(m_H)}{R_A^i(m_A)}$$

这意味着，**A/H 价格比率的变化仅反映两地折现因子的相对变化**，与现金流预期无关！

进一步，折现因子可分解为无风险利率和风险溢价：

$$R_J^i = r_f(m_J) + r_{p,i}(m_J), \quad J \in \{A, H\}$$

由于香港利率紧跟美联储，而大陆货币政策独立，美国货币政策意外主要影响 $R_H$，对 $R_A$ 影响有限。因此，**美国货币政策意外对 A/H 比率的影响可以视为对香港投资者折现因子的因果效应**。

### 4.2 基准回归模型

基于上述框架，作者估计如下 DID 模型：

$$(P_A/P_H)_{ist} = \alpha_i + \eta_s + \lambda_t + \beta \cdot \text{Surprise}_s \times \text{Post}_t + \varepsilon_{ist}$$

其中：

- $i$：公司
- $s$：FOMC 公告事件
- $t$：事件时间 (相对公告日的天数，$t \in [-5, 5]$)
- $(P_A/P_H)_{ist}$：公司 $i$ 在事件 $s$ 的事件时间 $t$ 的 A/H 比率
- $\text{Surprise}_s$：事件 $s$ 的货币政策意外 (单位：百分点)
- $\text{Post}_t$：公告后虚拟变量 ($t \geq 0$ 时为 1)
- $\alpha_i$：公司固定效应 (吸收公司特定的 A/H 溢价水平)
- $\eta_s$：公告固定效应 (吸收公告时点的宏观经济状况)
- $\lambda_t$：事件时间固定效应 (吸收事件窗口内的共同时间趋势)

**核心系数 $\beta$** 衡量：1 个百分点的意外利率变化导致 A/H 比率变化多少。

- 若 $\beta > 0$：意外加息 → H 股相对下跌 → A/H 比率上升
- 若 $\beta < 0$：意外降息 → H 股相对上涨 → A/H 比率下降

**标准误聚类**：在公司层面聚类，以允许同一公司不同事件间的残差相关。

### 4.3 事件研究规格 (Event Study Specification)

为展示动态效应，作者还估计如下事件研究模型：

$$(P_A/P_H)_{ist} = \alpha_i + \eta_s + \lambda_t + \sum_{\tau=-4}^{5} \beta_\tau \cdot \text{Surprise}_s \times \mathbb{1}(t=\tau) + \varepsilon_{ist}$$

其中，$\beta_\tau$ 捕捉公告前后各时点上货币政策意外对 A/H 比率的影响。$\tau = -1$ 时的系数标准化为 0 (基准组)。

### 4.4 识别假设与潜在威胁

**核心识别假设**：在没有货币政策公告的情况下，A/H 比率应该平稳演变——即不存在其他因素在 FOMC 公告时点上同时仅影响 A 股或 H 股投资者的折现率。

**潜在威胁及应对**：

1. **现金流预期的异质性反应**  
   *威胁*：如果大陆和香港投资者对同一公司现金流的预期在货币政策公告后出现系统性分化，仍可能导致 A/H 比率变化。  
   *应对*：
   - 按对美出口份额分组检验 (Appendix A)：如果现金流渠道重要，出口企业应更敏感。结果显示无显著差异。
   - 检验两地分析师的 EPS 预测是否分化 (Appendix B)：结果显示两地分析师预测高度一致，且不因货币政策意外而分化。

2. **汇率变动**  
   *威胁*：如果 HKD/CNY 或 USD/CNY 汇率在 FOMC 公告后发生变化，可能影响 A/H 比率计算。  
   *应对*：Appendix C 展示事件研究结果，证实汇率（即期和远期）在公告前后无显著变化——这与港币盯住美元、人民币相对稳定的制度安排一致。

3. **信息流动不完全**  
   *威胁*：如果两地投资者获取信息的速度或质量存在差异，可能导致股价短期偏离。  
   *应对*：香港和大陆地理、文化接近，信息流动障碍较小。且作者发现效应持续 5 天，排除了纯粹的信息摩擦解释。

---

## 5. 主要实证结果

### 5.1 货币政策对银行间利率的传导

在分析股价反应之前，作者首先验证美国货币政策意外是否确实传导到香港金融条件，而不影响大陆。图 3 展示了事件研究结果：

- **HIBOR 和 HIBOR 期货** (左上、右上)：1 个百分点的意外加息导致 3 个月 HIBOR 上升约 1 个百分点，呈现近乎一对一的传导。
- **LIBOR (美元)** (左下)：作为参照，显示相似的传导模式。
- **SHIBOR** (右下)：几乎无反应，证实大陆货币政策的独立性。

**结论**：美国货币政策意外强烈影响香港利率，但不影响大陆利率——这为后续识别策略提供了关键支持。

### 5.2 基准回归结果

表 3 展示了基准 DID 回归结果 (Equation 3 的不同规格)：

| 规格 | 公司 FE | 事件时间控制  | 公司特定趋势 | 系数 $\beta$ |
| ---- | ------- | ------------- | ------------ | ------------ |
| (1)  | 否      | 无            | 无           | 0.306***     |
| (2)  | 否      | Post 虚拟变量 | 无           | 0.292***     |
| (3)  | 是      | Post 虚拟变量 | 无           | 0.293***     |
| (4)  | 是      | 事件时间 FE   | 共同         | 0.292***     |
| (5)  | 是      | 事件时间 FE   | 分离         | 0.276***     |

**解读**：

- 所有规格下，$\beta$ 系数稳定在 0.28-0.31 之间，且在 1% 水平上显著。
- **经济含义**：1 个百分点 (100 bp) 的意外降息导致 A/H 比率下降约 30 bp，即 H 股相对 A 股上涨约 $30/230 \approx 13\%$（A/H 均值为 2.3）。
- 对于更常见的 25 bp 意外，效应约为 3% 的相对股价变化。
- 这一效应**显著大于** Bernanke and Kuttner (2005) 估计的 1% 整体股价反应——可能因为本文剥离了现金流渠道和「Fed 信息效应」的对冲影响。

### 5.3 动态效应：事件研究

图 4 展示了事件研究系数 $\beta_\tau$ ($\tau \in [-4, 5]$)：

- **公告前** ($\tau < 0$)：系数围绕 0 波动，无显著趋势 → **平行趋势假设成立**。
- **公告日及之后** ($\tau \geq 0$)：系数显著为正，且在公告后 3 天达到峰值，随后略有回落但仍显著。

**重要发现**：折现因子调整**不是瞬时完成的**，而是在公告后数天内逐步显现。这与以下文献一致：

- Binsbergen and Grotteria (2024)：抵押贷款收益率需数周才完全调整
- Brooks et al. (2018)：债券市场存在公告后漂移 (post-FOMC drift)
- Neuhierl and Weber (2024)：将漂移归因于折现因子修正

**方法论启示**：仅关注公告日当天反应的高频策略可能**低估**货币政策的真实效应——因为同时释放的宏观信息可能在短期内对冲折现率效应。

### 5.4 非对称效应：周期放大 vs. 周期矛盾

表 4 将样本按货币政策周期 (加息期/降息期/平稳期) 和意外方向 (加息意外/降息意外/接近零) 交叉分组：

| 周期阶段 | 意外方向   | 系数 $\beta$ | 公告数 |
| -------- | ---------- | ------------ | ------ |
| 加息期   | 意外加息 ✓ | 0.390***     | 8      |
| 加息期   | 意外降息   | -0.096       | 8      |
| 降息期   | 意外降息 ✓ | 0.355***     | 19     |
| 降息期   | 意外加息   | 0.047        | 13     |
| 平稳期   | 任何意外   | 不显著       | 34     |

(✓ 表示「周期放大型意外」)

**关键发现**：

- **仅有周期放大型意外**（加息期的意外加息、降息期的意外降息）产生显著的折现因子效应，系数约为 0.35-0.39。
- **周期矛盾型意外**（如加息期的意外降息）系数接近 0 且不显著。

**理论解释**：这一非对称性与「Fed Put」文献一致 (Cieslak and Pang, 2021; Haddad et al., 2025)：

- 投资者根据货币政策意外**更新对 Fed 反应函数的信念** (Bauer et al., 2022)。
- 周期放大型意外提供**更强的信号**，表明 Fed 对经济下行风险的反应更激进 (或对通胀的容忍度更低)。
- 例如，降息期的意外降息 → 投资者上调对「Fed Put」强度的预期 → 风险溢价下降 → 股价上涨。

图 5 直观展示了这一非对称性：仅在周期放大型意外后，H 股价格出现明显变化 (相对 A 股)。

### 5.5 横截面异质性分析

表 6 检验了四个股票特征如何调节货币政策意外的影响 (Triple-DID 规格)：

#### A. 市盈率 (PE Ratio)

- **低 PE 股票** (价值股)：$\beta = 0.346$***
- **高 PE 股票** (成长股)：$\beta = 0.162$***
- **差异显著**（$p < 0.01$）

**解释**：价值股对折现率变化更敏感，因为其现金流更集中在近期。这与 Lettau and Wachter (2007)、Binsbergen et al. (2012) 的现金流久期理论一致。

#### B. 市值 (Market Capitalization)

- **小市值股票**：$\beta = 0.367$***
- **大市值股票**：$\beta = 0.237$***

**解释**：小公司面临更高的宏观风险暴露，因此折现率对宏观公告更敏感 (Fama and French, 1992)。

#### C. CAPM Beta

- **低 Beta 股票**：$\beta = 0.220$***
- **高 Beta 股票**：$\beta = 0.381$***

**解释**：高 Beta 股票对风险溢价变化更敏感——这直接支持了货币政策通过风险溢价渠道影响股价的机制。这也与 Savor and Wilson (2014) 和 Cieslak et al. (2019) 的发现一致：CAPM 在宏观公告日表现更好。

#### D. 滞后 A/H 比率

- **低滞后比率**：$\beta = 0.211$***
- **高滞后比率**：$\beta = 0.396$***

**解释**：A/H 溢价本身可能反映某些持久的股票特征 (如流动性、投资者情绪)，这些特征与折现率敏感性相关。

---

## 6. 稳健性检验

### 6.1 现金流预期异质性

**Appendix A：按对美出口份额分组**

表 A.1 展示，将样本分为零出口和正出口两组后，两组的 $\beta$ 系数无显著差异 (0.194 vs. 0.208)。这排除了现金流渠道的重要性——如果现金流预期差异重要，出口企业应更敏感于美国货币政策。

**Appendix B：分析师预测**

作者从 I/B/E/S 获取大陆和香港分析师对同一公司的 EPS 预测，构建预测比率并进行事件研究。图 B.1 显示两地预测高度一致 (散点紧贴 45 度线)；图 B.2 和表 B.1 显示，货币政策意外不导致预测比率显著变化。

**结论**：大陆和香港投资者的现金流预期**没有因货币政策意外而系统性分化**。

### 6.2 汇率渠道

**Appendix C**

- 图 C.1：HKD/CNY 和 USD/CNY 即期汇率在公告前后几乎无变化。
- 图 C.2 和 C.3：事件研究证实即期和 6 个月远期汇率均不对货币政策意外做出反应。

**结论**：汇率稳定性排除了汇率渠道的干扰。

### 6.3 样本和规格的稳健性

表 7 展示了多种样本调整下的结果：

1. **纳入 ZLB时期**：$\beta = 0.130$***（系数略小但仍显著）
2. **排除接近零的意外**：$\beta = 0.291$***（与基准一致）
3. **排除节假日公告**：$\beta = 0.286$***
4. **排除节假日前后交易日**：$\beta = 0.295$***

所有结果均保持稳健。

**Appendix D：动态异质性处理效应**

采用 stacked DID 方法 (Baker et al., 2022; Cengiz et al., 2019) 控制动态异质性处理效应，结果甚至略强 ($\beta = 0.445$***)。

**Online Appendix E** 进一步展示了对以下方面的稳健性：

- 替代聚类方法 (双向聚类、bootstrap)
- 不同固定效应规格
- 扩展事件窗口 (10 天)
- 排除个别异常公告的敏感性分析

### 6.4 方差分解

表 5 进行时间序列层面的方差分解：将 A/H 比率平均值 (等权或市值加权) 对货币政策意外回归，$R^2$ 约为 2.6%-3.2%。

**解释**：货币政策意外能解释 A/H 比率时间序列变异的一小部分——这符合预期，因为 A/H 溢价受多种因素影响 (流动性、投资者情绪、资本管制松紧等)。但关键在于，本文识别了其中**由折现因子变化驱动的因果成分**。

---

## 7. 结论与启示

**主要贡献**

本文提供了**迄今最干净的证据**，证明货币政策通过折现因子渠道显著影响股票价格：

1. **方法创新**：利用 A-H 双重上市结构，首次成功分离现金流和折现因子渠道。
2. **量化发现**：100 bp 意外降息导致 H 股相对上涨约 13%（相对 A 股），效应持续 5 天。
3. **非对称性**：仅周期放大型意外产生显著效应——支持投资者学习 Fed 反应函数的理论。
4. **横截面模式**：高 Beta、小市值、价值股对折现率冲击更敏感，符合资产定价理论预测。

**政策启示**

1. **货币政策传导机制**：央行不应低估其政策对资产价格的影响——折现因子效应可能被传统方法低估。
2. **金融稳定**：如果投资者对 Fed 反应函数的信念是时变的，那么货币政策的资产价格效应也是时变的——这对金融稳定监测有重要意义。
3. **跨境溢出效应**：美国货币政策通过折现率渠道对新兴市场资产价格产生显著溢出——即使在资本管制下。

**研究局限与未来方向**

1. **机制黑箱**：本文清晰识别了折现因子效应的存在，但对其内部机制 (风险溢价 vs. 时间折现率？投资者异质性？) 的区分仍有限。
2. **非对称性的微观基础**：为何仅周期放大型意外产生效应？需要更丰富的理论模型和微观证据 (如调查数据)。
3. **长期效应**：5 天窗口已显示效应持续，但更长期的影响 (如季度、年度) 有待探索。
4. **其他市场**：本文方法能否推广到其他存在双重上市的市场 (如 ADR)？

---

## 参考文献

* Baker, A. C., Larcker, D. F., & Wang, C. C. (**2022**). How much should we trust staggered difference-in-differences estimates? *Journal of Financial Economics*, 144(2), 370–395. [Link](https://doi.org/10.1016/j.jfineco.2021.10.008), [PDF](http://sci-hub.ren/10.1016/j.jfineco.2021.10.008), [Google](https://scholar.google.com/scholar?q=How+much+should+we+trust+staggered+difference-in-differences+estimates+Baker+Larcker+Wang+2022).

* Bauer, M. D., Pflueger, C. E., & Sunderam, A. (**2022**). Perceptions about monetary policy. *NBER Working Paper* No. 30480. [Link](https://doi.org/10.3386/w30480), [PDF](https://www.nber.org/system/files/working_papers/w30480/w30480.pdf), [Google](https://scholar.google.com/scholar?q=Perceptions+about+monetary+policy+Bauer+Pflueger+Sunderam+2022).

* Bernanke, B. S., & Kuttner, K. N. (**2005**). What explains the stock market's reaction to Federal Reserve policy? *Journal of Finance*, 60(3), 1221–1257. [Link](https://doi.org/10.1111/j.1540-6261.2005.00760.x), [PDF](http://sci-hub.ren/10.1111/j.1540-6261.2005.00760.x), [Google](https://scholar.google.com/scholar?q=What+explains+the+stock+market%27s+reaction+to+Federal+Reserve+policy+Bernanke+Kuttner+2005).

* van Binsbergen, J. H., & Grotteria, M. (**2024**). Monetary policy wedges and the long-term liabilities of households and firms. *NBER Working Paper* No. 32137. [Link](https://doi.org/10.3386/w32137), [PDF](https://www.nber.org/system/files/working_papers/w32137/w32137.pdf), [Google](https://scholar.google.com/scholar?q=Monetary+policy+wedges+and+the+long-term+liabilities+of+households+and+firms+van+Binsbergen+Grotteria+2024).

* van Binsbergen, J., & Koijen, R. S. (**2017**). The term structure of returns: Facts and theory. *Journal of Financial Economics*, 124(1), 1–21. [Link](https://doi.org/10.1016/j.jfineco.2017.01.009), [PDF](http://sci-hub.ren/10.1016/j.jfineco.2017.01.009), [Google](https://scholar.google.com/scholar?q=The+term+structure+of+returns:+Facts+and+theory+van+Binsbergen+Koijen+2017).

* Brooks, J., Katz, M., & Lustig, H. (**2018**). Post-FOMC announcement drift in U.S. bond markets. *NBER Working Paper* No. 25127. [Link](https://doi.org/10.3386/w25127), [PDF](https://www.nber.org/system/files/working_papers/w25127/w25127.pdf), [Google](https://scholar.google.com/scholar?q=Post-FOMC+announcement+drift+in+U.S.+bond+markets+Brooks+Katz+Lustig+2018).

* Cengiz, D., Dube, A., Lindner, A., & Zipperer, B. (**2019**). The effect of minimum wages on low-wage jobs. *Quarterly Journal of Economics*, 134(3), 1405–1454. [Link](https://doi.org/10.1093/qje/qjz014), [PDF](http://sci-hub.ren/10.1093/qje/qjz014), [Google](https://scholar.google.com/scholar?q=The+effect+of+minimum+wages+on+low-wage+jobs+Cengiz+Dube+Lindner+Zipperer+2019).

* Cieslak, A., & Pang, H. (**2021**). Common shocks in stocks and bonds. *Journal of Financial Economics*, 142(2), 880–904. [Link](https://doi.org/10.1016/j.jfineco.2021.06.008), [PDF](http://sci-hub.ren/10.1016/j.jfineco.2021.06.008), [Google](https://scholar.google.com/scholar?q=Common+shocks+in+stocks+and+bonds+Cieslak+Pang+2021).

* Cieslak, A., Morse, A., & Vissing-Jorgensen, A. (**2019**). Stock returns over the FOMC cycle. *Journal of Finance*, 74(5), 2201–2248. [Link](https://doi.org/10.1111/jofi.12818), [PDF](http://sci-hub.ren/10.1111/jofi.12818), [Google](https://scholar.google.com/scholar?q=Stock+returns+over+the+FOMC+cycle+Cieslak+Morse+Vissing-Jorgensen+2019).

* Fama, E. F., & French, K. R. (**1992**). The cross-section of expected stock returns. *Journal of Finance*, 47(2), 427–465. [Link](https://doi.org/10.2307/2329112), [PDF](http://sci-hub.ren/10.2307/2329112), [Google](https://scholar.google.com/scholar?q=The+cross-section+of+expected+stock+returns+Fama+French+1992).

* Haddad, V., Moreira, A., & Muir, T. (**2025**). Whatever it takes? The impact of conditional policy promises. *American Economic Review*, 115(1), 295–329. [Link](https://doi.org/10.1257/aer.20230486), [PDF](https://amoreira2.github.io/alan-moreira.github.io/WhateverItTakes.pdf), [Google](https://scholar.google.com/scholar?q=Whatever+it+takes+The+impact+of+conditional+policy+promises+Haddad+Moreira+Muir+2025).

* Kuttner, K. N. (**2001**). Monetary policy surprises and interest rates: Evidence from the Fed funds futures market. *Journal of Monetary Economics*, 47(3), 523–544. [Link](https://doi.org/10.1016/S0304-3932%2801%2900055-1), [PDF](http://sci-hub.ren/10.1016/S0304-3932%2801%2900055-1), [Google](https://scholar.google.com/scholar?q=Monetary+policy+surprises+and+interest+rates:+Evidence+from+the+Fed+funds+futures+market+Kuttner+2001).

* Lettau, M., & Wachter, J. A. (**2007**). Why is long-horizon equity less risky? A duration-based explanation of the value premium. *Journal of Finance*, 62(1), 55–92. [Link](https://doi.org/10.1111/j.1540-6261.2007.01201.x), [PDF](http://sci-hub.ren/10.1111/j.1540-6261.2007.01201.x), [Google](https://scholar.google.com/scholar?q=Why+is+long-horizon+equity+less+risky%3F+A+duration-based+explanation+of+the+value+premium+Lettau+Wachter+2007).

* Nakamura, E., & Steinsson, J. (**2018**). High-frequency identification of monetary non-neutrality: The information effect. *Quarterly Journal of Economics*, 133(3), 1283–1333. [Link](https://doi.org/10.1093/qje/qjy004), [PDF](http://sci-hub.ren/10.1093/qje/qjy004), [Google](https://scholar.google.com/scholar?q=High-frequency+identification+of+monetary+non-neutrality:+The+information+effect+Nakamura+Steinsson+2018).

* Neuhierl, A., & Weber, M. (**2024**). Monetary momentum. *Chicago Booth Research Paper* No. 20-05. [Link](https://doi.org/10.2139/ssrn.3030126), [PDF](https://papers.ssrn.com/sol3/Delivery.cfm/SSRN_ID4821145_code4373405.pdf?abstractid=3030126&mirid=1&type=2), [Google](https://scholar.google.com/scholar?q=Monetary+Momentum+Neuhierl+Weber+2024).

* Savor, P., & Wilson, M. (**2014**). Asset pricing: A tale of two days. *Journal of Financial Economics*, 113(2), 171–201. [Link](https://doi.org/10.1016/j.jfineco.2014.04.005), [PDF](http://sci-hub.ren/10.1016/j.jfineco.2014.04.005), [Google](https://scholar.google.com/scholar?q=Asset+pricing:+A+tale+of+two+days+Savor+Wilson+2014).

