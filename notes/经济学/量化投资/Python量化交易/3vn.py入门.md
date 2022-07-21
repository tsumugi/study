vn.py 

### 简介

特性
+ 为交易而生
+ 实盘交易为切入点：完整的量化业务链包括数据获取、数据分析、策略回测和实盘交易。
+ 开源
+ 事件驱动

其他相关量化j交易项目
+ Zipline
+ Tushare
+ Trump2Cash
+ RQAlpha


通用组件
+ **vnpy.gateway** 接口，覆盖国内外所有交易品种的交易接口
+ **vnpy.app** 开箱即用的交易策略
	+ cta_strategy：CTA策略引擎模块
	+ cta_backtester：CTA策略回测模块
	+ spread_trading：多合约价差套利模块
	+ algo_trading：算法交易模块，常用算法：TWAP、Sniper、Iceberg、BestLimi等
	+ option_master：期权波动率交易模块
	+ portfolio_strategy：多合约组合策略模块
	+ script_trader：脚本策略模块
	+ chart_wizard：实时K线图表模块
	+ rpc_service：RPC服务模块
	+ excel_rtd：Excel RTD(RealTimeData)模块，
	+ data_manager：历史数据管理模块
	+ data_recorder：行情记录模块
	+ risk_manager：风险管理模块
	+ web_trader：Web服务模块
	+ portfolio_manager：投资组合管理模块
	+ paper_account：模拟交易账户模块
+ **vnpy.event** 事件驱动引擎
+ **vnpy.chart** K线图表
+ **vnpy.trader.database** 大数据库管理端模块
+ **vnpy.trader.datafeed** 标准化接口BaseDataFeed


### 基本使用

#### 启动

```bash
python run.py
```


#### 连接

SimNow仿真接口
+ 用户名: 6位数字(InvestorID)
+ 密码：(注册的账号需要修改一次密码后才能登录)
+ 经纪商代码：9999
+ 交易服务器：180.168.146.187:10202
+ 行情服务器：180.168.146.187:10212
+ 产品名称：simnow_client_test
+ 授权编码：0000000000000000 （16个0）

连接成功以后，日志组件会立刻输出登陆相关信息，同时用户也可以看到账号信息，持仓信息，合约查询等相关信息。

#### 使用

合约查询：默认查询所有

订阅行情：在交易组件选择交易所、填写合约代码，回车键即可查询，并在行情组件显示。


#### 日志
日志位置
``` shell
%HOME%\.vntrader\log
```
日志可以从轻到严重分成DEBUG、INFO、WARNING、ERROR、CRITICAL五个级别，分别对应10、20、30、40、50的整数值。


#### 数据库

datafeed数据服务

标准化的接口BaseDatafeed(vnpy.trader.datafeed)

database配置，支持主流的数据库


### 交易

加载交易接口
```python
# 写在顶部
from vnpy_ctp import CtpGateway

# 写在创建main_engine对象后
main_engine.add_gateway(CtpGateway)
```


配置信息可以直接修改json文件

两类账号
+ 仿真账号：SimNow两套环境用于盘中仿真交易以及盘后的测试。需要修改一次密码之后才能使用。请注意每套仿真环境的适用时间段是不同的。
+ 实盘账号：在期货公司开户，通过联系客户经理可以开通。

很多券商和期货公司都会提供测试账号，实盘账号也有测试账号。需要时再看。


### 数据库

支持Sqlite、MySQL、PostgreSQL、MongoDB、InfluxDB、Arctic(英国量化对冲基金Man AHL基于MongoDB开发的高性能金融时序数据库)、LevelDB等数据库。

需要建立名为 vnpy 的数据库。

可以存取行情数据，K线数据等。

### DataFeed

标准化的接口BaseDatafeed（位于vnpy.trader.datafeed中）

配置字段：
+ datafeed.name：数据服务接口的名称，必须为全称的小写英文字母
+ datafeed.username：数据服务的用户名
+ datafeed.password：数据服务的密码

如果是token方式授权请填写在database.password字段中


支持的7种DataFeed
+ RQData：RiceQuant的数据服务，官方推荐
+ UData：恒生电子最新推出的云端数据服务
+ TuShare：开源的Python金融数据接口项目
+ TQSDK：天勤TQSDK，信易科技推出的Python程序化交易解决方案
+ Wind
+ iFinD：同花顺iFinD是同花顺公司推出的面向专业机构用户的金融数据终端
+ TinySoft：天软金融数据


### CTA策略模块

CTA策略实盘模块

加载模块
```python
# 写在顶部
from vnpy_ctastrategy import CtaStrategyApp

# 写在创建main_engine对象后
main_engine.add_app(CtaStrategyApp)
```

用户自行开发的策略，要保存在
```
%HOME%\strategies
```
目录中


## vn.py架构

三层架构
+ 底层接口：底层接口负责对接行情和交易API，包括获取数据、发送交易指令等。
+ 中层引擎：包括事件引擎、订单路由和数据引擎，往下对接各种数据接口，往上服务各种应用模块。将底层数据整合，便于上层调用。
+ 上层应用：包括GUI图形界面、CTA策略模块、价差交易模块、行情记录模块等模块。

### 底层接口

CTP API：上海期货信息技术有限公司专门为期货交易开发的。《CTP客户端开发指南》。接口包括三个部分
+ 交易接口（Trader API） 负责订单处理、行情转发及银期转账业务；
+ 风控接口（Risk API）盘中进行高速的实时试算，以及时揭示并控制风险。
+ 结算接口（CSV）负责交易管理、账户管理、经纪人管理、资金管理、费率设置、日终结算、信息查询，以及报表管理等；

### 事件引擎

事件驱动

结构
+ 事件队列
+ 事件处理线程
+ 事件处理函数字典/通用事件处理函数列表
+ 定时器
+ 引擎开关


### 上层应用

PyQt

GUI组件

