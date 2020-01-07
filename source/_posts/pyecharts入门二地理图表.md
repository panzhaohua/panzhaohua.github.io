---
title: pyecharts入门二地理图表
category: Python基础
date: 2020-01-02
---
pyecharts入门二地理图表
```python
from pyecharts import options as opts
from pyecharts.charts import Bar,Map
import pandas as pd
#导入模块
df = pd.read_excel('v20191216全量机器mac码  .xlsx')
df = df.head(10)
#导入数据
```


```python
df.keys()
```




    Index(['省份', '城市', '大区', '商家', '门店编号', '门店', '包厢', '营业状态', '状态维持时间', '未联网原因',
           '机器码', '设备属性', '版本号', '上线日期', '硬件状态', '断网次数', '网络环境', '网络运营商', '4G卡号',
           '4G卡号获取类型', '获取时间', '营业开店时间', '营业结束时间', '门店联系者电话', '空调状态', '当前室温',
           '机器型号', '铭牌号', '接口号', '运营方', '点位合作方式', '最新签到时间', '高点播量歌曲缺歌数', '运营状态',
           '制冷设备'],
          dtype='object')




```python
#数值连续型
c = (
    Map()
    .add("全国分布",[('湖南','23'),('湖北', '210')],
         "china")
    #.set_series_opts(label_opts=opts.LabelOpts(is_show=False))  #不显示省份标签
    .set_global_opts(
        title_opts=opts.TitleOpts(title="商家分布"),
        visualmap_opts=opts.VisualMapOpts(max_=200)          
                    )
    )
c.render_notebook()
```



```python
#数值分段型
c = (
    Map()
    .add("全国分布",[('湖南','23'),('湖北', '190')],
         "china")
    .set_series_opts(label_opts=opts.LabelOpts(is_show=False))
    .set_global_opts(
        title_opts=opts.TitleOpts(title="商家分布"),
        visualmap_opts=opts.VisualMapOpts(max_=200,is_piecewise=True)          
                    )
    )
c.render_notebook()
```





```python
#世界地图
c = (
    Map()
    .add("世界分布",[('China','23'),('United States', '190')],
         "world")
    .set_series_opts(label_opts=opts.LabelOpts(is_show=False))
    .set_global_opts(
        title_opts=opts.TitleOpts(title="商家分布"),
        visualmap_opts=opts.VisualMapOpts(max_=200,is_piecewise=True)          
                    )
    )
c.render_notebook()
```








```python
#湖南地图
c = (
    Map()
    .add("湖南省分布",[('长沙市','23'),('湘潭市', '190'),('株洲市', '110')],
         "湖南")
    .set_series_opts(label_opts=opts.LabelOpts(is_show=False))
    .set_global_opts(
        title_opts=opts.TitleOpts(title="商家分布"),
        visualmap_opts=opts.VisualMapOpts(max_=200,is_piecewise=True)          
                    )
    )
c.render_notebook()
```




```python
from pyecharts import options as opts
from pyecharts.charts import Geo
from pyecharts.globals import ChartType, SymbolType
```


```python

#地理坐标热力地图
c = (
    Geo()
    .add_schema(maptype="湖南")
    .add(
        "geo",
        [('常德市','123'),('邵阳市', '190'),('永洲市', '141')],
        #type_=ChartType.EFFECT_SCATTER,  #散点图   
        type_=ChartType.HEATMAP,         #热力图   
        )
    #.set_series_opts(label_opts=opts.LabelOpts(is_show=False))
    .set_global_opts(
        title_opts=opts.TitleOpts(title="热力图分布"),
        visualmap_opts=opts.VisualMapOpts(max_=200,is_piecewise=True)  #分段
        #visualmap_opts=opts.VisualMapOpts()   
                    )
    )
c.render_notebook()
```



```python

#地理坐标线
c = (
    Geo()
    .add_schema(
        maptype="湖南",  #选择区域
        itemstyle_opts=opts.ItemStyleOpts(color="#ffffff", border_color="#ff0000"),  #底部颜色
    )
    .add(
        "geo",
        [('常德市','123'),('邵阳市', '190'), ('永洲市', '199'),('长沙市', '36')],
        type_=ChartType.EFFECT_SCATTER,  #散点图   
        #type_=ChartType.HEATMAP,         #热力图   
        color="green",
        )
    .add(
        "geo",
        [("常德市", "邵阳市"), ("邵阳市", "长沙市"), ("长沙市", "郴州市"), ("长沙市", "永州市")],
            type_=ChartType.LINES,
            effect_opts=opts.EffectOpts(
                symbol=SymbolType.ARROW, symbol_size=15, color="blue"
            ),
            linestyle_opts=opts.LineStyleOpts(curve=0.6),
        )
    #.set_series_opts(label_opts=opts.LabelOpts(is_show=False))
    .set_global_opts(
        title_opts=opts.TitleOpts(title="地理坐标线"),
        visualmap_opts=opts.VisualMapOpts(max_=200,is_piecewise=True)  #分段
        #visualmap_opts=opts.VisualMapOpts()   
                    )
    )
c.render_notebook()
```
