**采购经理人指数(Purchasing Managers' Index)**

一个宏观经济的先行指标，通常用来预测经济走势。低于50%说明经济处于衰退期，高于50%说明经济处于增长期。

为月度发布数据。

### 计算方法

通过对各个企业的采购经理人进行问卷调查，然后对调查结果进行汇总，通过扩散指数法计算每个分类的指标。计算每个分类指标的方法如下
$$
DI = P_1 + 0.5 \times P_2DI
$$
其中

- $P_1$ 为报告增长的数量占总调查结果数量的百分比
- $P_2$ 为报告不变的数量占总调查结果数量的百分比
- $P_3$ 为报告衰退的数量占总调查结果数量的百分比



如果都报告衰退，则指数值为0，如果都报告不变，则值为50%，如果都报告增长，则值为100%。因此，低于50%说明该分类处于收缩状态，高于50%说明该分类处于扩张状态。

得到分类指标后，对各分类进行加权平均，就可以得到PMI指数。


$$
PMI=\sum_0^n w_i \times DI_i
$$
其中$ w_i$为分类指标$DI_i$的权重。



因为月度发布的数据季节性因素影响较大，所以得到的PMI指数会通过X-13模型进行调整，剔除季节因素的影响。

### 思考

总体的经济状况看作每个企业经济状况的总和。

经济活动的最终目的都可以归结为人的欲望。经济活动的最终产品都要直接或间接的被人消费。资本主义会通过各种方式刺激人类的欲望，使对消费品的需求扩大。增加人口也可以使对消费品的需求扩大。在需求不足的情况下，政府通过扩张的财政政策来购买过剩的消费品，也可以是经济保持繁荣。

经济繁荣可以定义为社会生产的总产品的增加，经济衰退则为总产品的减少。在一个开放的国家中，社会总产品的影响因素可以归结为：本国消费需求、政府购买以及出口。

如果把制造业定义为一个通过设备和劳动，使用原材料生产产品的机构，则制造业企业运行的要素包括

- 资本(固定资产)
- 劳动
- 原材料
- 组织

这些个要素可以构成一个可以运行的企业，促使企业运行的原因还是需求。

制造业PMI指数各分类的意义

- 新订单：促进企业生产的需求。
- 生产：企业实际的生产量。企业实际生产增加，说明当前和预期的订单增加。
- 就业： 企业对劳动资源的需求。企业对劳动需求增加，说明生产需求增加。
- 供应商供货时间：反映原材料市场的供需情况。供货时间少说明原材料市场需求不足，可以快速满足需求。供货时间长，说明原材料市场供不应求。因此是一个逆指标。
- 原材料库存：企业需求增加时，会倾向增加原材料库存。



### 中国官方PMI

中国从2005年1月开始编制PMI指数，由国家统计局和中国物流与采购联合会联合发布。每月最后一日的9:00由国家统计局发布。在https://data.stats.gov.cn/index.htm 网站查询。

中国的PMI由5个分类指数加权平均得到，各分类和权重如下

- 新订单指数    30%
- 生产指数    25%
- 从业人员指数    20%
- 供应商配送时间指数    15% (逆指标，需要反向计算(100 - DI))
- 主要原材料库存指数    10%

得到的PMI指数会通过X-13模型进行调整，剔除季节因素的影响。

统计局会同时发布制造业PMI指数和非制造业PMI指数，并按照二者占GDP的比例加权得到综合PMI指数。

### 美国ISM的PMI

由 美国供应管理协会(Institute for Supply Management, ISM)编制 ([ ](http://www.ism.ws/)https://www.ismworld.org/)

ISM从1946年就开始编制PMI指数。

ISM的制造业PMI包含5个分类指标，分别为

- 新订单
- 生产
- 就业
- 交付
- 库存

2001年前，权重为新订单（30%）、生产（25%）、就业（20%）、交付（15%）、库存（10%）。2001年后，权重都为20%。

非制造业PMI没有分类指标，反映非制造业的总体变化情况。



### IHS Markit

IHS Markit 公司 (https://ihsmarkit.com/index.html) 会定期发布世界上主要经济体的PMI指数(https://www.markiteconomics.com/Public?language=en)。 包括制造业、服务业、建筑业和整个经济的PMI指数。

‌

#### 财新中国PMI

统计的中国的指数为**财新中国制造业通用PMI** 和 **财新中国通用服务业PMI** 。

**财新中国制造业通用PMI** 是5个单项的加权平均，5个单项和权重为

- 新订单  30%
- 产出  25%
- 就业人数 20%
- 供货时间  15%   (逆指标，需要反向计算)
- 采购库存 10%

会对数据进行季节性修正。

**财新中国服务业通用PMI**  的数据为 **服务业经营活动指数** 。

 两个PMI指数根据占GDP的比重加权平均，得到综合PMI。



### 日本TANKAN

 日本企业短期经济调查，由日本银行调查并编制，每季度发布一次。

 其中对经济的勘察判断调查，类似于PMI指数。