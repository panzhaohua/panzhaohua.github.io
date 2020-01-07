---
title: pyecharts入门四mysql连接
category: Python基础
date: 2020-01-06
tags: pyecharts
---

```python
import pymysql
import pandas as pd
from pyecharts.charts import Line, Funnel
```


```python
#import pyecharts
#dir(pyecharts.charts)  #检测有哪些类
conn = pymysql.connect(host='192.168.19.30', user='panzhaohua',passwd='******',db='dw')
sql = 'select * from rents'
df = pd.read_sql(sql,conn)
df = df.head(1000)
```


```python
#df  # 显示表格内容
#df['rent_end']
```


```python
inner_un = df['inner_code'].nunique()
#inner_un
inner_list = df['inner_code'].tolist()
#df['box_seq']
box_cou = df.groupby('inner_code').count()['box_seq']
xbox = list(box_cou.keys())
xbox
ybox = box_cou.values.tolist()
#dir(ybox)
            #box_cou
```


```python
#inner_list = df['inner_code'].tolist()
#box_list = df['box_seq'].tolist()


line = (
    Line()
    .add_xaxis(xbox)
    .add_yaxis('出租的柜子数量',ybox,is_smooth=True)
    )
line.render_notebook()
```





<script>
    require.config({
        paths: {
            'echarts':'https://assets.pyecharts.org/assets/echarts.min.js'
        }
    });
</script>

        <div id="9f36d166f044443aac041d1cd4028900" style="width:900px; height:500px;"></div>

<script>
        require(['echarts'], function(echarts) {
                var chart_9f36d166f044443aac041d1cd4028900 = echarts.init(
                    document.getElementById('9f36d166f044443aac041d1cd4028900'), 'white', {renderer: 'canvas'});
                var option_9f36d166f044443aac041d1cd4028900 = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "color": [
        "#c23531",
        "#2f4554",
        "#61a0a8",
        "#d48265",
        "#749f83",
        "#ca8622",
        "#bda29a",
        "#6e7074",
        "#546570",
        "#c4ccd3",
        "#f05b72",
        "#ef5b9c",
        "#f47920",
        "#905a3d",
        "#fab27b",
        "#2a5caa",
        "#444693",
        "#726930",
        "#b2d235",
        "#6d8346",
        "#ac6767",
        "#1d953f",
        "#6950a1",
        "#918597"
    ],
    "series": [
        {
            "type": "line",
            "name": "\u51fa\u79df\u7684\u67dc\u5b50\u6570\u91cf",
            "connectNulls": false,
            "symbolSize": 4,
            "showSymbol": true,
            "smooth": true,
            "step": false,
            "data": [
                [
                    "0001359",
                    180
                ],
                [
                    "0001375",
                    108
                ],
                [
                    "0001421",
                    36
                ],
                [
                    "0021275",
                    108
                ],
                [
                    "0021383",
                    36
                ],
                [
                    "0021391",
                    108
                ],
                [
                    "0021431",
                    31
                ],
                [
                    "0081201",
                    40
                ],
                [
                    "621105",
                    324
                ],
                [
                    "9990001",
                    29
                ]
            ],
            "hoverAnimation": true,
            "label": {
                "show": true,
                "position": "top",
                "margin": 8
            },
            "lineStyle": {
                "width": 1,
                "opacity": 1,
                "curveness": 0,
                "type": "solid"
            },
            "areaStyle": {
                "opacity": 0
            }
        }
    ],
    "legend": [
        {
            "data": [
                "\u51fa\u79df\u7684\u67dc\u5b50\u6570\u91cf"
            ],
            "selected": {
                "\u51fa\u79df\u7684\u67dc\u5b50\u6570\u91cf": true
            }
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "textStyle": {
            "fontSize": 14
        },
        "borderWidth": 0
    },
    "xAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "gridIndex": 0,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "splitLine": {
                "show": false,
                "lineStyle": {
                    "width": 1,
                    "opacity": 1,
                    "curveness": 0,
                    "type": "solid"
                }
            },
            "data": [
                "0001359",
                "0001375",
                "0001421",
                "0021275",
                "0021383",
                "0021391",
                "0021431",
                "0081201",
                "621105",
                "9990001"
            ]
        }
    ],
    "yAxis": [
        {
            "show": true,
            "scale": false,
            "nameLocation": "end",
            "nameGap": 15,
            "gridIndex": 0,
            "inverse": false,
            "offset": 0,
            "splitNumber": 5,
            "minInterval": 0,
            "splitLine": {
                "show": false,
                "lineStyle": {
                    "width": 1,
                    "opacity": 1,
                    "curveness": 0,
                    "type": "solid"
                }
            }
        }
    ]
};
                chart_9f36d166f044443aac041d1cd4028900.setOption(option_9f36d166f044443aac041d1cd4028900);
        });
    </script>
