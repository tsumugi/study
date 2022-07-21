


股票市场中，流通股的数量是相对固定的，即车上的座位数量是固定的。交易是不断上下车的过程，预期价格上升的人上车，预期价格下降的人下车。当前的价格反映了一种共识，或者是一种均衡状态。
+ 车上的人都预期价格会上升
+ 市场上买卖双方的均衡，如果价格下跌，会有人买入，价格上升会有人卖出。
打破均衡状态需要有资金的流入或流出。如果外部资金流入，就会有大量买盘，形成一种力量，不断推高成交价格。如果有资金希望流出，就会形成大量卖盘，压低成交价格。

均衡被打破。

均衡的概念，惯性。买入的人不可能快速卖出，除非有外部的消息输入导致决策变化。

价格的升降可以理解为一种资金流入和流出的过程。


符号说明
+ O 开盘价
+ C 收盘价
+ H 最高价
+ L 最低价
+ V 成交量
+ P 价格
+ t 交易日
+ n 周期

指标分类
+ 趋势跟踪
	+ 平均线指标
		+ 简单移动平均线(SMA)
		+ 加权移动平均线(WMA)
		+ 指数移动平均线(EMA)
		+ 双指数平均线(DEMA)
		+ 三指数移动平均线 T3(T3)
		+ 三指数移动平均线(TEMA) 
		+ 卡夫曼自适应移动平均线(KAMA)
		+ MESA自适应移动平均线(MAMA)
		+ 三角形移动平均线(TRIMA)
	+ 时间序列预测(最小二乘法，TSF)
+ 振荡指标
	+ 威廉R指标(WILLR)
	+ 相对强弱指标(RSI)
	+ 终极波动指标(ULTOSC)
+ 波幅和价格指标
	+ 波幅
		+ 真实波幅(TR)
		+ 平均真实波幅(ATR)
		+ 方差(VAR)
		+ 变动率(ROC)
	+ 价格
		+ 加权收盘价(WCLPRICE)
		+ 典型价格(TYPPRICE)
+ 成交量指标
	+ 柴金累积派发线(AD)


## 趋势跟踪

### 平均线指标(Moving Average)

MA   

#### 简单移动平均线(Simple Moving Average)

SMA

公式
$$
SMA_{n,t}(P) = \frac{\sum_{t-n}^t P_i}{n}
$$

#### 加权移动平均线(Weighted Moving Average)

WMA          

公式
$$
	WMA_{n,t}(P) = \frac{\sum_{t-n}^t i \times P_i} {n \times (n+1) / 2}
$$
简单的线性加权方式

####  指数移动平均线(Exponential Moving Average)

EMA 

公式
$$
EMA_t(P, k) = EMA_{t-1} + (P_t - EMA_{t-1}) \times k
$$

k 为指数，一般k的取值为$\frac{2}{t+1}$
此时，EMA为$EMA_t(P) = \frac{P_t \times 2 + EMA_{t-1} \times (t-1)}{t+1}$

#### 双重指数平均线(Double Exponential Moving Average)

DEMA 

公式
$$
DEMA_t(P,k) = 2 \times EMA_t(P,k) - EMA_t(EMA_t(P,k), k)
$$

#### 三重指数移动平均线 T3(Triple Exponential Moving Average (T3))

T3    

公式

$$
GD_t(P, k,f) =EMA_t(P,k) \times (1+f) - EMA_t(EMA_t(P,k), k) \times f
$$
$$
T3_t(P,k,f) = GD_t(GD_t(GD_t(P,k,f), k, f), k, f)
$$
#### 三重指数移动平均线(Triple Exponential Moving Average)

TEMA

公式

$$
TEMA_t(P,k) = 3 \times EMA_t(P, k) - 3 \times EMA_t(EMA_t(P, k), k) +  EMA_t(EMA_t(EMA_t(P, k), k), k)
$$

#### 卡夫曼自适应移动平均线(Kaufman Adaptive Moving Average)

KAMA 

#### MESA自适应移动平均线(MESA Adaptive Moving Average)

MAMA

####  三角形移动平均线(Triangular Moving Average)

TRIMA


#### 时间序列预测(Time Series Forecast)

TSF

最小二乘法的线性回归，根据历史数据拟合一条直线，计算直线的斜率和y轴截距，然后带入当天的值，预测当天的价格。


计算斜率(m)和y轴截距(b)
$$
m = \frac{n \times \sum_0^n (i \times P_i) - \sum_0^n i \times \sum_0^n P_i }{(\sum_0^n i)^2 - n \times \sum_0^n i^2}
$$
$$
b = \frac{\sum_0^n P_i - m \times \sum_0^n i}{n}
$$
预测价格
$$
  P_n = b + m \times n
$$

相关函数

LINEARREG          返回 $P_n = b + m \times (n-1)$
LINEARREG_ANGLE     角度表示的斜率
LINEARREG_INTERCEPT  截距
LINEARREG_SLOPE    斜率


#### 抛物线转向指标(Parabolic SAR)

SAR

SAR，Stop and Reverse，停止并反向操作。

SAR操作一般用来设置止损点。

构造方式是，先判断上升和下降趋势，一般通过Plus DM 或Minus DM来判断初始的趋势。

在上升趋势中，SAR值设在底部。如果市场未出现新低，上升趋势持续,，如果价格创新高，加速因子AF提高。
如果市场出现新低，突破了SAR，则立刻反转，SAR值设为近期最高价，加速因子AF重置，开始下降趋势。

在下降趋势中，SAR设在顶部，如果市场未出现新高，则下降趋势持续，如果价格创新低，加速因子AF提高。
如果市场出现新高，突破了SAR，则立刻反转，SAR值设在最近最低价，加速因子AF重置。

AF，加速因子，一个初始值，一个最大值，每次增加一个步长，直到最大值不再增加。一般初始值设为0.02，步长为0.02，最大值为0.2。

$$
SAR_t = SAR_{t-1} + AF \times (EP - SAR_{t-1})
$$
EP，在上升趋势中为，这个上升趋势中的最高价；在下降趋势中，EP为这个下降趋势中的最低价。

研判：
+ 价格向下跌破SAR时为卖出信号。
+ 价格向上突破SAR时为买入信号。
+ 市场为横向走势时，SAR指标的作用较小。


SAREXT，扩展方法，可以控制对初始趋势的判断。

#### 希尔伯特变换(Hilbert Transform)

寻找市场周期的指标

HT_DCPERIOD 

HT_DCPHASE

HT_PHASOR

HT_SINE

HT_TRENDLINE

HT_TRENDMODE



### 动量指标

#### 上升动量(Plus DM)和下降动量(Minus DM)

Directional Movement

PLUS_DM、MINUS_DM

+DM、-DM

公式：先计算最高价和最低价升高、降低的程度
$$
\begin{align}
& DiffP =  H_t - H_{t-1} \\
& DiffM = L_{t-1} - L_t
\end{align}
$$
PLUS_DM
$$
\begin{align}
 & if(DiffP > 0 \&\& DiffP > DiffM) \\
 & then(PLUS\_DM_t = DiffP) \\
 & else (PLUS\_DM_t = 0)
\end{align}
$$

MINUS_DM
$$
\begin{align}
 & if(DiffM > 0 \&\& DiffM > DiffP) \\
 & then(MINUS\_DM_t = DiffM) \\
 & else (MINUS\_DM_t = 0)
\end{align}
$$

最高价和最低价相对于昨日变动的幅度，来衡量买方和卖方的力量。如果最高价上升，且变动幅度大于最低价的变动幅度，则说明买方力量占优。如果最低价下降，且下降幅度大于最高价的上升幅度，说明卖方力量占优。其他情况，买卖双方力量均衡。

考虑了最高价和最低价，不重视收盘价的影响。

#### 上升方向指标(PLus DI)和下降方向指标(Minus DI)

Directional Indicator

PLUS_DI、MINUS_DI

+DI、-DI

PLUS_DI
$$
PLUS\_DI_t = \frac{\sum_{t-n}^n PLUS\_DM_t}{\sum_{t-n}^n TR_t}
$$
MINUS_DI
$$
MINUS\_DI_t = \frac{\sum_{t-n}^n  MINUS\_DM_t}{\sum_{t-n}^n TR_t}
$$

通过真实波幅TR，对DM标准化。


#### 趋向指标 (Directional Movement Index)

DX

$$
DX_t = \frac{abs(PLUS\_DI_t - MINUS\_DI_t)}{PLUS\_DI_t + MINUS\_DI_t} \times 100
$$

#### 平均趋向指标(Average Directional Movement Index)

$$
ADX_{n,t} = MA_{n,t}(DX_t)
$$

#### 平均趋向指标排名(Average Directional Movement Index Rating)

ADXR

$$
ADXR_{n,t} = \frac{ADX_t + ADX_{t-n}}{2}
$$


## 振荡指标

#### 威廉指标(Williams' %R)

WILLR

公式

$$
WILLR_t = \frac{max(H,n) - C_t}{max(H,n) - min(L,n)} \times 100
$$
说明：n日内的最大值和最小值为区间，看当日收盘价在这个区间中的位置，以此来表示当前市场的热度。n一般取值为14或20。
+ 取值范围为0-100，当收盘价等于n日内最高价时，值为0，当收盘价等于n日内最低价时，值为100。
+ 0-20为顶部，为超买区间。80-100为底部，为超卖区间。20-80为多空平衡状态。

研判
+ 20为卖出线，80为买进线。
+ 向上突破50时，市场转强，为买入信号；向下跌破50时，市场转弱，为卖出信号。

缺陷
+ 在一个连续上升趋势中，指标值可能一直为100，并不是超买标志。
+ 很难进行背离判断。

#### 相对强弱指标(Relative Strength Index)

RSI

公式

先统计n日内收盘价相对于前一日收盘价的变化，涨跌分别记录

$$
  \begin{align}
  & if (C_t - C_{t-1} > 0)\\
  & then (Gain_t = Gain_{t-1} + （C_t - C_{t-1})) \\
  & else (Loss_t = Loss_{t-1} + (C_{t-1} - C_t))
  \end{align}
$$
然后累加n日的值，计算RSI
$$
RSI_{t,n} = \frac{Gain_{t,n}}{Loss_{t,n} + Gain_{t,n}} \times 100
$$
说明：只关注收盘价，根据收盘价的变化，并累加这种变化，来判断近期的市场强弱。
+ 如果一直上升，则值为100.如果一直下降，则值为0. 一个反映趋势的指标。

研判
+ 50为中线，大于50，市场强势，小于50，市场弱势。
+ 上下为超买和超卖区，一般取值为70，30。超买区和超卖区的背离是价格反转信号。


#### 终极波动指标(Ultimate Oscillator)

ULTOSC

公式

真实最低价(True Low)
$$
TL_t = min(L_t, C_{t-1})
$$
相对买压(Relative Buy Pressure)
$$
RBP_{t,n} = \frac{\sum_{t-n}^t (C_i - TL_i)}{\sum_{t-n}^t TR_i}
$$
分别计算三个周期m，n，o的相对买压的加权平均值，得到ULTOSC
$$
ULTOSC_t = \frac{RBP_{m, t} \times 4 + RBP_{n,t} \times 2 + RBP_{o,t}}{7} \times 100
$$

m，n, o一般取值为7,14,28。权重可以按照比例选择。

说明：

也是通过收盘价在波动幅度中的位置来判断买卖状况。买压的概念，收盘价接近最高价，说明有足够多的买方力量来支撑价格，而且买后的惯性也使价格下降的可能性变小。可以用来衡量买方力量的强弱。买方力量通过真实波幅标准化，然后求和。可以得到一段时期内的买方力量的平均值。不同时段平均值的加权平均，来表示市场的相对强弱。

研判
+ 35和70为超卖、超买线，指标在35下或70上，走势和价格走势背离时，趋势反转信号。
+ 上升到50-70间，随后向下跌破50，为短线卖出信号。
+ 上升到70，随后跌破70，是中线卖出信号。

#### 随机指标(Stochastic)

STOCH

未成熟随机值 RSV  （FAST_K） STOCHF
$$
RSV_t = \frac{C_t - min(L, n)}{max(H,n) - min(L,n)}
$$
%K
$$
K_t = MA_{n,t}(RSV)
$$
%D
$$
D_t = MA_{m,t}(K)
$$
%J

$$
J_t = 3 \times K_t - 2 \times D_t
$$

STOCHRSI   RSI指标的K和D

#### 价格百分比振荡指标(Percentage Price Oscillator)

PPO

公式

$$
PPO_t = \frac{MA_{m,t}(P) - MA_{n,t}(P)}{MA_{n,t}(P)} \times 100
$$

快速移动均线与慢速移动均线的差值占慢速均线的百分比。

类似MACD指标，但是以百分比的形式呈现。

#### 异同移动平均线(Moving Average Convergence/Divergence)

MACD

快线(FAST)
$$
MACDFAST_t = MA_{m,t}(P) - MA_{n,t}(P)
$$

慢线(SLOW)
$$
MACDSLOW_{t,n} = MA_{t,n}(MACDFAST) 
$$

柱状图(HIST)
$$
MACDHIST_{t,n} = MACDFAST_t - MACDSLOW_{t,n}
$$

相关函数

MACDEXT            可控制MA类型

MACDFIX             12/26周期


#### 绝对价格振荡量( Absolute Price Oscillator)

APO

$$
APO_t = \frac{MA_{t,m}(P) - MA_{t,n}(P)}{MA_{t,n}(P)} \times 100
$$

## 价格和波幅

### 波动幅度

#### 真实波幅(True Range)

TRANGE

公式
$$
TRANGE_t = max(H_t - L_t, abs(C_{t-1} - L_t), abs(C_{t-1} - H_t))
$$
昨日收盘价，今日最高价，今日最低价之间的最大差距；用来表示一天价格的实际波幅。


#### 平均真实波幅(Average True Range)

ATR

公式

$$
ATR_t = \frac{ATR_{t-1} \times (n-1) + TR_t}{n}
$$
真实波幅的移动平均值，表示价格波动范围，价格变化的剧烈程度。可以用来衡量市场状态。
(此处的实现方式不是算术平均值，而是一种变体)

#### 标准化的平均真实波幅(Normalized Average True Range)

NATR

公式
$$
   NATR_{n,t} = \frac{ATR_{n,t}}{C_t}
$$

当日的平均真实波幅，除以当日的收盘价。



#### 方差(Variance)

VAR

$$
VAR_t = \frac{\sum_{t-n}^n P_i^2}{n} - (\frac{\sum_{t-n}^n P_i}{n})^2
$$
统计学中方差的计算公式，可以通过公式$\sigma ^2 = \frac{\sum_0^N(X - \overline{X})^2}{N}$  推导出来。

#### 标准差(Standard Deviation)

STDDEV 

公式
$$
STDDEV_t = \sqrt{VAR_t}
$$


#### 动量(Momentum)

MOM
$$
MOM_{n,t} = P_t - P_{t-n}
$$

#### 变动率(ROC)

衡量一段时间内价格变化的比率。主要有两种计算方式，一种是价格差占原来价格的百分比；另一种是两个价格的比值。

价格差百分比方式

ROCP 
$$
ROCP_{t,n} = \frac{P_t - P_{t-n}}{P_{t-n}}
$$

ROC  ($ROC = ROCP \times 100$)
$$
ROC_{t,n} = \frac{P_t - P_{t-n}}{P_{t-n}} \times 100
$$

比值方式
ROCR
$$
ROCR_{t,n} = \frac{P_t}{P_{t-n}}
$$
ROCR100 ($ROCR100 = ROCR \times 100$)

$$
ROCR100_{t,n} = \frac{P_t}{P_{t-n}} \times 100
$$


#### 阿隆指标(Aroon)

AROON

$$
AROONUP_{t,n} = \frac{n - (t - maxIndex_{n,t}(H))}{n} \times 100 
$$

$$
AROONDOWN_{t,n} = \frac{n - (t - minIndex_{n,t}(L))}{n} \times 100 
$$


#### 阿隆振荡量(Aroon Oscillator)

AROONOSC

$$
AROONOSC_{t,n} = \frac{maxIndex_{n,t}(H) - minIndex_{n,t}(L)}{n} \times 100 
$$


### 价格

#### 加权收盘价(Weighted Close Price)

WCLPRICE

公式

$$
WCLPRICE = \frac{H + L + 2 \times C}{4}
$$

#### 典型价格(Typical Price)
TYPPRICE 

公式
$$
TYPPRICE = \frac{C + L + H}{3}
$$
当日最高价、最低价和收盘价的平均值

#### 平均价格(Average Price)

AVGPRICE

$$
AVGPRICE_t = \frac{H_t + L_t + O_t + C_t}{4}
$$


#### 最大值和最小值

MAXINDEX     

MININDEX          

MINMAX     

MINMAXINDEX      

#### 中点(MidPoint)

MIDPOINT 

$$
MIDPOINT_{t,n} = \frac{max_{n,t}(P) + min_{n,t}(P)}{2}
$$

#### 中点价格(Midpoint Price)

MIDPRICE

$$
MIDPRICE_{n,t} = \frac{max_{n,t}(H) + min_{n,t}(L)}{2}
$$

#### 中间价(Median Price)

MEDPRICE

$$
MEDPIRCE_t = \frac{H_t + L_t}{2}
$$



## 成交量指标

#### 能量潮(On Balance Volume)

OBV

公式

$$
OBV_t = \begin{cases}
OBV_{t-1} + V_t & C_t > C_{t-1} \\
OBV_{t-1} - V_t & C_t < C_{t-1} \\ 
\end{cases}
$$
理论依据：
+ 投资者对股价的评论越不一致，成交量越大。可以用成交量来判断多空的力量。
+ 重力原理，股价上升需要的能量更大。
+ 惯性原理，热门股票在一段时间内量价波动都会很大，冷门股票都会很小。

研判
+ 股价上升，OBV下降时，出现背离，趋势可能反转。
+ OBV缓慢上升，买气渐强，为买入信号。
+ OBV急速上升，力量将用尽，卖出信号。


#### 柴金累积派发线(Chaikin A/D Line)
缩写：AD

公式
$$
AD_t = AD_{t-1} + \frac{(C - L) - (H - C)}{H - L} \times V
$$
$$AD_0 = 0$$
说明：是一个累加值，根据收盘价离最高价和最低价之间的距离来判断多空力量，用当日波幅标准化，然后乘以成交量。是一种近似的反映资金流入流出的指标。成交量是伴随整个价格波动的所有交易量，通过价格波动的比率来近似的模拟最终导致价格变化的力量占所有成交量的比率。累加反映了一种资金持续的流入流出的状况。
+ 收盘价离最高价更近，则为正值；收盘价离最低价更近，为负值。
+ 收盘价等于最高价，乘数为1
+ 收盘价等于最低价，乘数为-1
+ 收盘价位于最高最低价中心，值为0

研判
+ A/D线上升，且价格趋势上升，买入信号。
+ A/D线下降，且价格趋势下降，卖出信号。
+ A/D线与价格趋势线背离，趋势反转信号。

优点是考虑了成交量，

缺点是成交量没有标准化，值没有上下限，不容易研判。

#### 柴金累积派发震荡量( Chaikin A/D Oscillator)

ADOSC

公式

$$
ADOSC = EMA(AD, n_1) - EMA(AD, n_2)
$$
是AD指标的衍生指标。

说明：通过AD的移动平均线的波动，来衡量资金的流入流出。比AD指标更平滑。ADOSC指标为快线和慢线的差值。
+ 为正，说明资金流入增加；为负，说名资金流出减少。
+ 趋势上升，说明资金流入速度变快。趋势下降，说明资金流入速度变慢。

研判
+ 向上穿越零线时买入，向下穿越零线时卖出。
+ 与价格趋势背离时，说明动量不足，趋势可能反转。

#### 资金流量指标(Money Flow Index)

MFI

$$
MR_{t,n} = \frac{\sum_{t-n}^t(TYPRICE_t \times V, TYPRICE_t > TYPRICE_{t-1})}{\sum_{t-n}^t (TYPRICE_t \times V, TYPRICE_t < TYPRICE_{t-1})}
$$

$$
MFI_{t,n} = \frac{MR_{t,n}}{1+MR_{t,n}} \times 100
$$
研判
+ MFI和价格走势的背离，是趋势反转的信号
+ 20和80为超卖和超买区
+ MFI向上穿越均线是买入信号，MFI向下穿越均线是卖出信号



#### 布林带(Bollinger Bands)

BBANDS

$$
BBANDS_{t,n,f} = MA_{t,n}(P) \pm f \times STDDEV(P)
$$

#### 能量均衡指标(Balance Of Power)

BOP

$$
BOP_t = \frac{C_t - L_t}{H_t - L_t} \times 100
$$
#### 贝塔指数(Beta)

BETA

一个股票的价格相对于股市指数的波动性衡量。


#### 三重指数平均线的变动率(1 day Rate-Of-Change (ROC) of a Triple Smooth EMA)

$$
TRIX_t = ROC_{t,1}(EMA(EMA(EMA(P))))
$$
#### 顺势指标( Commodity Channel Index)

CCI

$$
CCI = \frac{TYPRICE - MA_n(TYPRICE)}{MA(abs(TYPRICE-MA(TYPRICE))) \times 0.15} 
$$

#### 钱德动量摆动指标(Chande Momentum Oscillator)

CMO

统计n日内收盘价相对于前一日收盘价的变化，涨跌分别记录

$$
  \begin{align}
  & if (C_t - C_{t-1} > 0)\\
  & then (Gain_t = Gain_{t-1} + （C_t - C_{t-1})) \\
  & else (Loss_t = Loss_{t-1} + (C_{t-1} - C_t))
  \end{align}
$$

$$
CORREL = \frac{Gain - Loss}{Gain + Loss} \times 100
$$



#### 皮尔逊相关系数

CORREL



#### 蜡烛图相关函数

CDL2CROWS           Two Crows
CDL3BLACKCROWS      Three Black Crows
CDL3INSIDE          Three Inside Up/Down
CDL3LINESTRIKE      Three-Line Strike 
CDL3OUTSIDE         Three Outside Up/Down
CDL3STARSINSOUTH    Three Stars In The South
CDL3WHITESOLDIERS   Three Advancing White Soldiers
CDLABANDONEDBABY    Abandoned Baby
CDLADVANCEBLOCK     Advance Block
CDLBELTHOLD         Belt-hold
CDLBREAKAWAY        Breakaway
CDLCLOSINGMARUBOZU  Closing Marubozu
CDLCONCEALBABYSWALL Concealing Baby Swallow
CDLCOUNTERATTACK    Counterattack
CDLDARKCLOUDCOVER   Dark Cloud Cover
CDLDOJI             Doji
CDLDOJISTAR         Doji Star
CDLDRAGONFLYDOJI    Dragonfly Doji
CDLENGULFING        Engulfing Pattern
CDLEVENINGDOJISTAR  Evening Doji Star
CDLEVENINGSTAR      Evening Star
CDLGAPSIDESIDEWHITE Up/Down-gap side-by-side white lines
CDLGRAVESTONEDOJI   Gravestone Doji
CDLHAMMER           Hammer
CDLHANGINGMAN       Hanging Man
CDLHARAMI           Harami Pattern
CDLHARAMICROSS      Harami Cross Pattern
CDLHIGHWAVE         High-Wave Candle
CDLHIKKAKE          Hikkake Pattern
CDLHIKKAKEMOD       Modified Hikkake Pattern
CDLHOMINGPIGEON     Homing Pigeon
CDLIDENTICAL3CROWS  Identical Three Crows
CDLINNECK           In-Neck Pattern
CDLINVERTEDHAMMER   Inverted Hammer
CDLKICKING          Kicking
CDLKICKINGBYLENGTH  Kicking - bull/bear determined by the longer marubozu
CDLLADDERBOTTOM     Ladder Bottom
CDLLONGLEGGEDDOJI   Long Legged Doji
CDLLONGLINE         Long Line Candle
CDLMARUBOZU         Marubozu
CDLMATCHINGLOW      Matching Low
CDLMATHOLD          Mat Hold
CDLMORNINGDOJISTAR  Morning Doji Star
CDLMORNINGSTAR      Morning Star
CDLONNECK           On-Neck Pattern
CDLPIERCING         Piercing Pattern
CDLRICKSHAWMAN      Rickshaw Man
CDLRISEFALL3METHODS Rising/Falling Three Methods
CDLSEPARATINGLINES  Separating Lines
CDLSHOOTINGSTAR     Shooting Star
CDLSHORTLINE        Short Line Candle
CDLSPINNINGTOP      Spinning Top
CDLSTALLEDPATTERN   Stalled Pattern
CDLSTICKSANDWICH    Stick Sandwich
CDLTAKURI           Takuri (Dragonfly Doji with very long lower shadow)
CDLTASUKIGAP        Tasuki Gap
CDLTHRUSTING        Thrusting Pattern
CDLTRISTAR          Tristar Pattern
CDLUNIQUE3RIVER     Unique 3 River
CDLUPSIDEGAP2CROWS  Upside Gap Two Crows
CDLXSIDEGAP3METHODS Upside/Downside Gap Three Methods
