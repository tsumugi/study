一个Python的交易策略回测框架。

现在项目已经停止维护

每个zipline的算法都要实现两个方法
+ initialize(context)
+ handle_data(context, data)

zipline会先调用initialize函数来初始化，可以通过context传递变量和数据。
然后每次事件都会调用handle_data函数，会传递相同的context，还有一个data对象。data对象相当于一个事件的帧，包含当前的交易项OLHC(open, low, high, close) 开盘价、最低价、最高价和收盘价。

示例

``` python
# buyapple.py


from zipline.api import order, record, symbol

from zipline.finance import commission, slippage

  
  

def initialize(context):

 context.asset = symbol('AAPL')

  
 # Explicitly set the commission/slippage to the "old" value until we can

 # rebuild example data.

 # github.com/quantopian/zipline/blob/master/tests/resources/

 # rebuild_example_data#L105

 context.set_commission(commission.PerShare(cost=.0075, min_trade_cost=1.0))

 context.set_slippage(slippage.VolumeShareSlippage())

  

def handle_data(context, data):

 order(context.asset, 10)

 record(AAPL=data.current(context.asset, 'price'))


# Note: this function can be removed if running

# this algorithm on quantopian.com

def analyze(context=None, results=None):

 import matplotlib.pyplot as plt

 # Plot the portfolio and asset data.

 ax1 = plt.subplot(211)

 results.portfolio_value.plot(ax=ax1)

 ax1.set_ylabel('Portfolio value (USD)')

 ax2 = plt.subplot(212, sharex=ax1)

 results.AAPL.plot(ax=ax2)

 ax2.set_ylabel('AAPL price (USD)')

  

 # Show the plot.

 plt.gcf().set_size_inches(18, 8)

 plt.show()

```

主要的功能都在`zipline.api` 中

`order` 用来交易

`record` 用来记录

`analyze` 用来分析记录

给模型喂数据，可以使用Quand API获取NASDAQ的数据。

可以使用`zipline ingest`命令

运行算法`zipline run`
+ `-f` 指定算法文件
+ `-o` 结果输出
+ `--start --end` 开始和结束日期


