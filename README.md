# 中国商品期货成本线与估值分位数据集

71 个中国商品期货品种的**现金流成本线 / 完全成本上沿 / 估值分位**日频数据，附 300 个交易日的收盘价序列。

> Daily cost-curve and valuation dataset for 71 Chinese commodity futures, with 300-day close price series.

维护：[AutoBotHub 研究团队](https://autobothub.com/about.html) · 数据主页：<https://autobothub.com/open-data.html>

---

## 这是什么

商品期货的估值判断常需要一个「成本锚」：价格相对产业成本处在什么位置。

本数据集把每个品种的**成本区间**与**当前价格**放在一起，给出可直接计算的比例与分位，用于回答：

- 现价跌破现金流成本了吗？（产能出清压力的常用参考位）
- 现价在完全成本上沿之上还是之下？
- 这个位置在过去 300 个交易日里出现过几次？

字段与口径在 [开放数据页](https://autobothub.com/open-data.html) 有完整说明。

## 文件

| 文件 | 内容 |
|---|---|
| `cost_curve.csv` | 71 品种汇总：最新价、现金流成本线、完全成本上沿、两个比值、序列起止 |
| `series/<code>.csv` | 单品种日线：`date, close, symbol, source` |
| `datapackage.json` | Frictionless Data 描述文件 |

单品种 CSV 也可直接从站点取：`https://autobothub.com/data/open/series/<code>.csv`

## 字段

| 字段 | 含义 |
|---|---|
| `品种代码` | 交易所品种代码（小写），如 `au` / `rb` / `m` / `ta` |
| `主力合约` | 当前主力合约代码，如 `au2612` |
| `最新价` | 主力连续合约最新收盘价 |
| `现金流成本线` | 产业现金成本对应的价格水平 |
| `完全成本上沿` | 含折旧与财务费用的完全成本上边界 |
| `价格/现金流成本` | 最新价 ÷ 现金流成本线。**< 1 表示跌破现金成本** |
| `价格/完全成本上沿` | 最新价 ÷ 完全成本上沿。**< 1 表示在完全成本之内** |
| `序列起始` / `序列结束` | 该品种日线覆盖区间 |
| `交易日数` | 区间内有效交易日数量 |

## 口径与限制（引用前请读）

1. **成本参数是模型估计值，不是交易所公布数据。** 不同机构的成本口径差异很大，**跨品种直接比较比值无意义**——只能同品种纵向比较。
2. **贵金属 `pt`（铂）与 `pd`（钯）的成本参数尚未校准**，其"价格/成本"比值显著偏离 1，**请勿直接引用这两个品种的成本字段**。
3. 成本区间在样本期内视为不变；实际产业成本随原料、能源、汇率变动。
4. 价格取主力连续合约收盘价，**换月处存在跳空，未做复权**。
5. 国债期货（`t` / `tf` / `ts` / `tl`）的价格单位与商品不同，比值仅作相对位置参考。
6. 数据按日更新，不保证与交易所结算价逐分一致。
7. 部分品种上市较晚（如 `pt` / `pd` 序列自 2025-11 起），样本长度短于 300 日。

**本数据集为研究与教育用途，不构成投资建议，不构成任何买卖点位建议或收益承诺。期货交易风险极大。**

## 更新与版本

- **日更数据**：<https://autobothub.com/open-data.html>（每个交易日更新一次，以 `cost_curve.csv` 的 `序列结束` 字段为准）
- **本仓库是定期快照**，不保证与本站逐日同步。引用本仓库时，请用最新 commit 日期标注快照时点；需要最新数据请引用上面的站点链接。


## 引用

```
AutoBotHub 研究团队. (2026). 中国商品期货成本线与估值分位数据集.
https://autobothub.com/open-data.html
```

BibTeX：

```bibtex
@misc{autobothub_costcurve_2026,
  title        = {中国商品期货成本线与估值分位数据集},
  author       = {{AutoBotHub 研究团队}},
  year         = {2026},
  howpublished = {\url{https://autobothub.com/open-data.html}},
  note         = {CC BY 4.0}
}
```

## 许可

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.zh)

转载、二次分析、商业使用均可，需注明来源并链接到 <https://autobothub.com/open-data.html>。

## 相关

- 品种数据页（永久地址，合约换月不变）：<https://autobothub.com/variety/>
- 研究记录归档：<https://autobothub.com/reports-archive.html>
- 站点与方法说明：<https://autobothub.com/about.html>
