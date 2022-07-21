## 基本操作

连接CTP

```python
from vnpy.app.script_trader import init_cli_trading
from vnpy_ctp import CtpGateway
from vnpy.trader.utility import load_json

setting = load_json("connect_ctp.json")
engine = init_cli_trading([CtpGateway])
engine.connect_gateway(setting, "CTP")
```

查询

```python
# 查询所有合约
engine.get_all_contracts(use_df=True)


# 查询资金
engine.get_all_accounts(use_df=True)

# 查询持仓
engine.get_all_positions(use_df=True)

# 查询活动委托
engine.get_all_active_orders(use_df=True)

# 订阅行情
engine.subscribe(["sc2209.INE"])

# 查询行情
engine.get_tick("sc2209.INE", use_df=True)
```

交易

```python
# 委托下单
vt_orderid = engine.buy("sc2209.INE", 32, 1000)

# 查询特定委托
engine.get_order(vt_orderid)

# 委托撤单
engine.cancel_order(vt_orderid)
```

