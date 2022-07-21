### 简介

社区地址：[https://tushare.pro](https://tushare.pro/)

安装
```
pip install tushare
```

注册用户：已经用手机号注册。

调用token


### 获取数据

#### HTTP方式

POST请求

URL：https://api.tushare.pro

请求内容
```json
{
	"api_name"："",
	
	"token"："",
	
	"params"：[],
	
	"fields"：""
}
```

响应

```json
{
	"code"：0,
	
	"msg": null,
	
	"data": []
}
```

#### Python API
```python
import tushare as ts

pro = ts.pro_api()

pro = ts.pro_api('your token')

df = pro.query('trade_cal', exchange='', start_date='20180901', end_date='20181001', fields='exchange,cal_date,is_open,pretrade_date', is_open='0')

```

### 数据

大多数都需要很多积分，基础的数据只能获取沪深股票列表，交易日历，指数列表，和个股的日线数据。

有权限获取的接口

股市：
+ **stock_basic**：股票列表
+ **trade_cal**：交易日历
+ namechange：股票曾用名
+ hs_const：沪深股通
+ stock_company：上市公司基本信息
+ new_share：IPO新股信息
+ **daily**：日线行情
+ pro_bar：通用行情接口
+ suspend：停牌信息
+ suspend_d：每日停复牌信息
+ hsgt_top10：沪股通、深股通每日前十大成交详细数据
+ ggt_top10：港股通每日成交数据
+ hk_hold： 沪深港股通持股明细
+ margin：融资融券每日交易汇总数据
+ margin_detail：沪深两市每日融资融券明细
+ top10_holders：前10大股东
+ top10_floatholders：前10大流通股东
+ share_float：获取限售股解禁
+ index_basic：指数基本信息
+ us_basic：美股列表
+ us_tradecal：美股交易日历
+ us_daily：美股日线行情，只能试用
+ trade_cal：期货交易日历

宏观经济
+ shibor：SHIBOR利率数据
+ shibor_quote：SHIBOR报价数据
+ shibor_lpr：LPR贷款基础利率
+ libor：Libor拆借利率
+ hibor：Hibor利率
+ us_tycr：美国国债收益率
+ us_trycr：国债实际收益率曲线利率
+ us_tbr：美国短期国债利率数据
+ us_tltr：国债长期利率
+ us_trltr：国债实际长期利率平均值
+ major_news：长篇通讯信息
+ fund_sales_ratio：各渠道公募基金销售保有规模占比数据
+ fund_sales_vol：销售机构公募基金销售保有规模数据

