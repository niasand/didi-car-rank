# Didi Car Rank


## 背景与原理

端午节回村里，发小问买个车跑滴滴应该选什么车。在发小眼里，跟互联网相关的，我应该都懂……但是，我也就是滴滴伪司机，2015年注册以来就跑过一单。滴滴加油倒是经常用！于是从`滴滴车主 APP ` 的`滴滴加油`页面抓了一点数据，根据滴滴公开的各个加油站实时订单以及滴滴司机回头客数据，帮基友选了个丰田卡罗拉。

这也引发了自己对 `数据` 消除不确定性，提高分析和判断命中率的思考：[什么车最适合跑滴滴——数据化思维小记](https://liudanking.com/beautiful-life/%E4%BB%80%E4%B9%88%E8%BD%A6%E6%9C%80%E9%80%82%E5%90%88%E8%B7%91%E6%BB%B4%E6%BB%B4-%E6%95%B0%E6%8D%AE%E5%8C%96%E6%80%9D%E7%BB%B4%E5%B0%8F%E8%AE%B0/)。因此把这个小玩具开源出来，希望可以帮到老司机们选到合适的车，开启滴滴老司机约跑（pào）的美好生活！

## 方案结构

![](https://ws1.sinaimg.cn/large/44cd29dagy1fsl6jrylxzj20gd0ddjs4.jpg)

## 使用

* 在电脑上安装 `didi-car-rank`:

```
go get github.com/liudanking/didi-car-rank
```

* 在电脑上运行 `didi-car-rank`:

```
didi-car-rank collect_data -d data
```


* 在手机上安装并信任[CA证书](https://github.com/liudanking/didi-car-rank/blob/master/cert/cert.pem)
* 设置手机代理，iPhone为例：`设置->无线局域网->小叹号->配置代理->手动`:

<img src="https://ws1.sinaimg.cn/mw690/44cd29dagy1fsl6c3jgwtj20yi1pcdmm.jpg" width='320' />

* 手机上打开 `滴滴车主 APP `, 找到`滴滴加油`，点进去，然后随便移动一下位置。对于一个城市来说，基本两分钟就把滴滴加油站滑完，数据也就采集得超不多了。
* 在电脑上运行 `didi-car-rank analysis -d data -city 成都市 -top 20`, 查看滴滴司机心中的神车有哪些：

![](https://ws1.sinaimg.cn/mw690/44cd29dagy1fsl690qr73j20bb0nj77q.jpg)

```

车型订单数量排名:
+------+--------------+------------+
| 排名 |     车型     | 实时订单数 |
+------+--------------+------------+
|    1 | 大众新捷达   |         52 |
|    2 | 斯柯达明锐   |         50 |
|    3 | 大众宝来     |         46 |
|    4 | 大众朗逸     |         42 |
|    5 | 丰田卡罗拉   |         39 |
|    6 | 起亚K3       |         35 |
|    7 | 马自达CX-5   |         30 |
|    8 | 大众速腾     |         29 |
|    9 | 大众新桑塔纳 |         28 |
|   10 | 日产轩逸     |         27 |
|   11 | 标致301      |         24 |
|   12 | 现代瑞纳     |         24 |
|   13 | 福特福克斯   |         23 |
|   14 | 哈弗H6       |         22 |
|   15 | 标致408      |         22 |
|   16 | 雪铁龙爱丽舍 |         21 |
|   17 | 雪佛兰爱唯欧 |         21 |
|   18 | 别克英朗     |         20 |
|   19 | 斯柯达昕锐   |         19 |
|   20 | 大众帕萨特   |         19 |
+------+--------------+------------+

车型加油积分排名:
+------+--------------+----------+----------+
| 排名 |     车型     | 加油积分 | 平均积分 |
+------+--------------+----------+----------+
|    1 | 丰田卡罗拉   |     1613 |    41.36 |
|    2 | 大众朗逸     |     1504 |    35.81 |
|    3 | 斯柯达明锐   |     1452 |    29.04 |
|    4 | 大众宝来     |     1283 |    27.89 |
|    5 | 日产轩逸     |     1232 |    45.63 |
|    6 | 大众速腾     |     1222 |    42.14 |
|    7 | 大众新捷达   |     1146 |    22.04 |
|    8 | 长安逸动     |     1002 |    58.94 |
|    9 | 起亚K3       |      870 |    24.86 |
|   10 | 别克英朗     |      846 |    42.30 |
|   11 | 大众新桑塔纳 |      743 |    26.54 |
|   12 | 现代朗动     |      720 |    42.35 |
|   13 | 丰田凯美瑞   |      719 |    79.89 |
|   14 | 日产天籁     |      694 |    49.57 |
|   15 | 标致301      |      671 |    27.96 |
|   16 | 雪铁龙爱丽舍 |      653 |    31.10 |
|   17 | 福特福克斯   |      570 |    24.78 |
|   18 | 现代瑞纳     |      568 |    23.67 |
|   19 | 别克凯越     |      544 |    45.33 |
|   20 | 斯柯达昕锐   |      527 |    27.74 |
+------+--------------+----------+----------+
```
* Enjoy!


## 其他

[data](https://github.com/liudanking/didi-car-rank/tree/master/data) 目录中预置了北上广深、杭州、成都的数据。如果你只是想看一下分析结果，可以直接用这些数据执行 `didi-car-rank analysis -d data -city 成都市 -top 20`.

如果你收集了其他城市的数据，我们也欢迎你把数据PR过来。