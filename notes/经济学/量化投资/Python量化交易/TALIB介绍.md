## C/C++ API

### 介绍
```c
 include "ta_libc.h"
```

Windows环境需要MSVC

Linux环境需要g++


### 函数调用
使用前先调用
```c
TA_Initialize()
```

退出时调用
```
TA_Shutdown()
```

可以直接调用的接口都定义在`ta-lib/c/include/ta_func.h`中

输入数据放在一个数组中，输出数据也是一个数组。TA函数不会为用户的数据分配内存。因此要合理规划输出数组的大小。

函数的通用格式如下(例子为计算移动平均线)
```c
TA_RetCode TA_MA( int          startIdx,  
 int          endIdx,  
 const double inReal[],  
 int          optInTimePeriod,  
 int          optInMAType,  
 int         *outBegIdx,  
 int         *outNbElement,  
 double       outReal[],  
  )
```
所有函数的参数都类似：
+ inReal为输入数据的数组
+ startIdx、endIndex确定输入数组中要计算的数据的范围
+ optInTimePeriod 为计算数据的选项，此处为移动平均值的时间跨度
+ optInMAType 也是计算选项，此处为移动平均值类型(SMA或EMA)
+ outBegIdx 第一个输出结果对应的输入数组开始位置。
+ outNbElement 输出结果中有效结果的个数。
+ outReal 输出结果数组

调用示例
```c

TA_Real    closePrice[400];
TA_Real    out[400];
TA_Integer outBeg;
TA_Integer outNbElement;

/* ... initialize your closing price here... */

retCode = TA_MA( 0, 399,
                 &closePrice[0],
                 30,TA_MAType_SMA,
                 &outBeg, &outNbElement, &out[0] );

/* The output is displayed here */
for( i=0; i < outNbElement; i++ )
   printf( "Day %d = %f\n", outBeg+i, out[i] );

```

计算30日SMA均线，从第30个数据开始计算，outBeg结果是29，outNbElementj为371。

要合理的规划输出数据的大小。一般可以根据输入数组、范围批评和精确分配来确定输出数组的大小。


### 高级特性

抽象层，在`ta-lib/c/include/ta_abstract.h` 文件中定义了相关函数。应用于想要支持所有TA函数的应用。如果只是象调用几个TA函数，就没必要用抽象层，直接调用就可以了。

一些函数由于开始的点不同，结果也不同。可以用函数`TA_SetUnstablePeriod`和 `TA_GetUnstablePeriod` 来控制开始的位置

每个TA函数都包括float输入版，和double输入版，例如
```c
TA_MA( int    startIdx,  
 int    endIdx,  
 **const double  inReal[],  
** int           optInTimePeriod,  
 TA_MAType     optInMAType,  
 int          *outBegIdx,  
 int          *outNbElement,  
 double        outReal[] );

TA_RetCode TA_S_MA( int    startIdx,  
 int    endIdx,  
 **const float inReal[],**  
 int         optInTimePeriod,  
 TA_MAType   optInMAType,  
 int        *outBegIdx,  
 int        *outNbElement,  
 double      outReal[] );
```

其中`TA_S_`前缀的为float版本。不管哪个版本，计算都使用double来计算。提供两个版本是方面使用者。

### 函数列表

AD                  Chaikin A/D Line
ADOSC               Chaikin A/D Oscillator
ADX                 Average Directional Movement Index
ADXR                Average Directional Movement Index Rating
APO                 Absolute Price Oscillator
AROON               Aroon
AROONOSC            Aroon Oscillator
ATR                 Average True Range
AVGPRICE            Average Price
BBANDS              Bollinger Bands
BETA                Beta
BOP                 Balance Of Power
CCI                 Commodity Channel Index
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
CMO                 Chande Momentum Oscillator
CORREL              Pearson's Correlation Coefficient (r)
DEMA                Double Exponential Moving Average
DX                  Directional Movement Index
EMA                 Exponential Moving Average
HT_DCPERIOD         Hilbert Transform - Dominant Cycle Period
HT_DCPHASE          Hilbert Transform - Dominant Cycle Phase
HT_PHASOR           Hilbert Transform - Phasor Components
HT_SINE             Hilbert Transform - SineWave
HT_TRENDLINE        Hilbert Transform - Instantaneous Trendline
HT_TRENDMODE        Hilbert Transform - Trend vs Cycle Mode
KAMA                Kaufman Adaptive Moving Average
LINEARREG           Linear Regression
LINEARREG_ANGLE     Linear Regression Angle
LINEARREG_INTERCEPT Linear Regression Intercept
LINEARREG_SLOPE     Linear Regression Slope
MA                  All Moving Average
MACD                Moving Average Convergence/Divergence
MACDEXT             MACD with controllable MA type
MACDFIX             Moving Average Convergence/Divergence Fix 12/26
MAMA                MESA Adaptive Moving Average
MAX                 Highest value over a specified period
MAXINDEX            Index of highest value over a specified period
MEDPRICE            Median Price
MFI                 Money Flow Index
MIDPOINT            MidPoint over period
MIDPRICE            Midpoint Price over period
MIN                 Lowest value over a specified period
MININDEX            Index of lowest value over a specified period
MINMAX              Lowest and highest values over a specified period
MINMAXINDEX         Indexes of lowest and highest values over a specified period
MINUS_DI            Minus Directional Indicator
MINUS_DM            Minus Directional Movement
MOM                 Momentum
NATR                Normalized Average True Range
OBV                 On Balance Volume
PLUS_DI             Plus Directional Indicator
PLUS_DM             Plus Directional Movement
PPO                 Percentage Price Oscillator
ROC                 Rate of change : ((price/prevPrice)-1)100
ROCP                Rate of change Percentage: (price-prevPrice)/prevPrice
ROCR                Rate of change ratio: (price/prevPrice)
ROCR100             Rate of change ratio 100 scale: (price/prevPrice)100
RSI                 Relative Strength Index
SAR                 Parabolic SAR
SAREXT              Parabolic SAR - Extended
SMA                 Simple Moving Average
STDDEV              Standard Deviation
STOCH               Stochastic
STOCHF              Stochastic Fast
STOCHRSI            Stochastic Relative Strength Index
SUM                 Summation
T3                  Triple Exponential Moving Average (T3)
TEMA                Triple Exponential Moving Average
TRANGE              True Range
TRIMA               Triangular Moving Average
TRIX                1-day Rate-Of-Change (ROC) of a Triple Smooth EMA
TSF                 Time Series Forecast
TYPPRICE            Typical Price
ULTOSC              Ultimate Oscillator
VAR                 Variance
WCLPRICE            Weighted Close Price
WILLR               Williams' %R
WMA                 Weighted Moving Average


## Python版TA-Lib

基于Cython的TA-LIB封装。使用了numpy，性能更好。


先安装C/C++版本的ta-lib库

然后
```shell
python3 -m pip install TA-Lib
```


使用

直接调用TA函数

Function API

```python

import numpy
import talib

close = numpy.random.random(100)

output = talib.SMA(close)
```

Abstract API  

抽象层
```python
import numpy as np
from talib.abstract import *

inputs = {
    'open': np.random.random(100),
    'high': np.random.random(100),
    'low': np.random.random(100),
    'close': np.random.random(100),
    'volume': np.random.random(100)
}

output = SMA(inputs, timeperiod=25)

upper, middle, lower = BBANDS(inputs, 20, 2, 2)
```

Streaming API

处理流式数据，计算最新的指标，比Function API 更快。

```python
import talib
from talib import stream

close = np.random.random(100)

# the Function API
output = talib.SMA(close)

# the Streaming API
latest = stream.SMA(close)
```

查询所有的函数
```python
import talib

# list of functions
print talib.get_functions()

# dict of functions by group
print talib.get_function_groups()
```