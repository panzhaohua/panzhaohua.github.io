---
title: pyecharts和pandas入门一
category: Python基础
date: 2019-12-31
---
pyecharts和pandas入门一

```python
from pyecharts import options as opts
from pyecharts.charts import Bar
import pandas as pd
#导入模块
```


```python
df = pd.read_excel('v20191216全量机器mac码  .xlsx')
df = df.head(10)
#导入数据
```


```python
df.keys() #查看keys
```




    Index(['省份', '城市', '大区', '商家', '门店编号', '门店', '包厢', '营业状态', '状态维持时间', '未联网原因',
           '机器码', '设备属性', '版本号', '上线日期', '硬件状态', '断网次数', '网络环境', '网络运营商', '4G卡号',
           '4G卡号获取类型', '获取时间', '营业开店时间', '营业结束时间', '门店联系者电话', '空调状态', '当前室温',
           '机器型号', '铭牌号', '接口号', '运营方', '点位合作方式', '最新签到时间', '高点播量歌曲缺歌数', '运营状态',
           '制冷设备'],
          dtype='object')




```python
df['断网次数'].tolist()  #查看可以打印出来的值
```




    [0, 0, 0, 0, 2, 2, 4, 0, 4, 6]




```python
bar = (Bar()
      .add_xaxis(df['机器码'].tolist())
      .add_yaxis('断网次数',df['断网次数'].tolist())
     # .add_yaxis('网络运营商',df['网络运营商'].tolist())
     .set_global_opts(title_opts=opts.TitleOpts(title="运营商", subtitle="断网次数"))
      )
bar.render_notebook()
#按照帮助文档提示，生成图像 http://pyecharts.org/#/zh-cn/quickstart

```
