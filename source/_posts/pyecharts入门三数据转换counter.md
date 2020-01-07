---
title: pyecharts入门三数据转换counter
category: Python基础
date: 2020-01-03
---

```python
from pyecharts import options as opts
from pyecharts.charts import Bar,Map
import pandas as pd
from collections import Counter
```


```python
df = pd.read_excel('v20191216全量机器mac码  .xlsx')
#df = df.head(10)
```


```python
df
```





```python
type(df["省份"])
```




    pandas.core.series.Series




```python
sf_list=df["省份"].tolist()
#sf_list
```


```python
sf_counter = Counter(sf_list)  
#统计list出现的频率
#sf_counter
```


```python
#list(sf_counter.keys,sf_couner.items)
#sf_counter.keys()
#sf_counter = sf_counter.items()   #使用items符合格式要求
```


```python
sf_xlist = list(sf_counter.keys())
sf_ylist = list(sf_counter.values())
#sf_xlist
```




    ['重庆市',
     '陕西省',
     '新疆维吾尔自治区',
     '广东省',
     '山东省',
     '浙江省',
     '江苏省',
     '江西省',
     '北京市',
     '新疆',
     '河南省',
     '贵州省',
     '天津市',
     '安徽省',
     '福建省',
     '甘肃省',
     '四川省',
     '上海市',
     '黑龙江省',
     '内蒙古',
     '云南省',
     '湖北省',
     '河北省',
     '吉林省',
     '辽宁省',
     '湖南省',
     '山西省',
     '广西',
     '海南省',
     '宁夏',
     '青海省',
     '西藏']




```python
bar = (
    Bar()
    .add_xaxis(sf_xlist)
    .add_yaxis("省份分布",sf_ylist)
    
    )
bar.render_notebook()
```

![列表图片](/img/200103/%E7%9C%81%E4%BB%BD%E5%88%86%E5%B8%83.png)



```python
map = (
    Map()
    .add("省份分布图", sf_counter,"china")
    )
#map.render_notebook()
```

