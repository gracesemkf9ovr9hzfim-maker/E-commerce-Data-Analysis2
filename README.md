# 📊 Olist E-commerce Data Analysis: Growth Drivers & Operations Bottlenecks
> 巴西最大百货电商平台 Olist 销售大盘诊断与用户流失归因分析

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-Data_Manipulation-150458.svg)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Data_Visualization-3776AB.svg)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626.svg)

## 🎯 项目目标 (Project Objective)
本项目基于巴西电商平台 Olist 的真实交易数据集（近 10 万笔订单），旨在通过全链路的数据清洗与多维分析，全面诊断平台的**营收健康度与运营瓶颈**。项目致力于为管理层提供基于数据的商业决策支持，核心目标包括：
1. **营收引擎定位**：发现具有高 ROI 的品类，验证电商二八定律，指导营销预算倾斜。
2. **体验痛点归因**：量化物流配送时效对用户评价（NPS）的致命影响，寻找体验生死线。
3. **高净值人群圈选**：构建 RFM 模型，精准定位超级 VIP 客户，优化精细化运营策略。

---

## 📁 数据说明 (Data Description)
本项目数据来源于 Kaggle 公开数据集（[Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)）。为避免仓库体积过大，原始 CSV 文件未上传至本仓库。
分析过程中主要调用了以下 5 张核心维度表，并通过 `customer_id` 与 `order_id` 等主键进行了复杂的多表级联（JOIN）：
- `olist_orders_dataset.csv` (订单状态与时间戳信息)
- `olist_order_items_dataset.csv` (订单商品明细与价格/运费)
- `olist_products_dataset.csv` (商品类目属性)
- `olist_customers_dataset.csv` (用户地域特征)
- `olist_order_reviews_dataset.csv` (用户 1-5 星评价数据)

---

## ⚙️ 分析步骤与核心架构 (Analysis Architecture)
本项目在 Jupyter Notebook 中独立完成，整体架构分为以下 5 大模块：

1. **数据预处理 (Data Preprocessing)**
   - 跨表合并与冗余字段清洗。
   - `Datetime` 格式强转，重构时间序列特征。
2. **宏观盘面分析 (Macro Trends & Geo-analysis)**
   - 提取年月特征，绘制 2016-2018 月度 GMV 增长折线图。
   - 按州（State）聚合销量，计算区域集中度。
3. **微观品类分析 (Micro Product & Pareto Principle)**
   - 计算各商品类目历史累计贡献，提取 Top 10 印钞机品类。
   - 验证帕累托法则（80/20 规则）在平台生态中的体现。
4. **口碑危机诊断 (Review Attribution & Logistics)**
   - 构造新特征 `delivery_days`（实际送达时间 - 下单时间）。
   - 关联分析“物流耗时”与“1-5星差评率”的倒挂规律。
5. **用户分层模型 (RFM Segmentation)**
   - 锁定 `customer_unique_id`，运用 `groupby().agg()` 聚合计算近期的活跃度(R)、频次(F)与累计金额(M)。
   - 设定业务阈值，圈选平台高净值 VIP 圈层。

---

## 💡 核心业务结论 (Key Business Insights)
1. **极度依赖大促，具有下沉空间**：平台在 2017 年 11 月（黑五）单月 GMV 史诗级爆发突破百万。空间上，单单圣保罗州（SP）就贡献了近 40% 的销售额，对其他州的物流与营销渗透严重不足。
2. **“二八定律”显著，营销应重仓头部**：「健康美容」与「手表礼品」两大品类累计贡献超 240 万雷亚尔利润，平台头部效应极强，建议将全站 80% 的广告资源聚焦于 Top 10 品类。
3. **14天为物流“生死线”**：数据实锤物流拖延是口碑崩盘的核心元凶。5星好评平均物流为 10.2天，但当物流拖延至 **20.8天** 时，1星差评率呈断崖式爆发。建议紧急优化偏远地区仓储，或对超 10 天未达订单实施主动客服干预。
4. **RFM 资产盘点**：成功在十万大军中提纯出“30天内活跃且历史消费超1000元”的超级 VIP，应立即启动专属客服与高规格复购礼包投放。

---

## 🚧 局限性与未来展望 (Limitations & Future Work)
- **缺乏成本数据**：数据集中仅包含销售额（Price）与运费（Freight），缺乏商品的进货底价（Cost），因此目前的测算为 GMV 而非绝对净利润（Net Profit）。
- **缺乏促销打折字段**：无法直接归因降价对销量的弹性影响（价格敏感度测试）。
- **未来方向 (Next Steps)**：未来可引入机器学习库（Scikit-Learn），利用历史购买序列训练一套 XGBoost 预测模型，提前预测即将流失的高危客户，将描述性分析升级为预测性分析。

---

## 💻 如何运行本项目 (How to Run)
1. 克隆本仓库至本地：`git clone [你的仓库链接]`
2. 确保本地已安装 Python 3.8+ 及 Jupyter 环境，并安装依赖：`pip install pandas matplotlib`
3. 前往 Kaggle 下载 [Olist 原始数据集](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)，解压并放入与代码同级的目录。
4. 在终端运行 `jupyter notebook`，打开 `.ipynb` 文件即可复现全部分析流程。
