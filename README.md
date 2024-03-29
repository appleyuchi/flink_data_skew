目前没有完成

本Repository主要参考美团的Spark数据倾斜方案以及其他网络资料,<br>
在Flink集群上,<br>
模拟各种可能出现的数据倾斜场景,对上述资料中提出的解决方案分别给出完整的实现.




|场景|解决方式|Java工程链接|Scala工程链接|参考文献|
|---|---|---|---|---|
|利用hive进行预处理(倾斜的key)|-|-|-|[1]
|过滤少数导致倾斜的key<br>分开计算||||[2]
|设置并行度|直接设置|[设置并行度.txt](设置并行度.txt)|设置并行度.txt](设置并行度.txt)|[3]|
|自定义分区|
|部分key导致倾斜|key-salting<br>(盐化:给key前面加随机数)|




导致倾斜的key可以是:<br>
①该key对应的数据特别少,导致某个task过早执行完<br>
②该key对应的数据特别多,导致某个task过晚执行完<br>

注:
①broadcast具有局限性,不能应对超过1G的变量(Spark中是这样的,Flink中暂时没有查询到上限)<br>
②例子中只是dataset,对于datastream类型的场景改下变量类型即可



Reference:<br>
[1][Spark性能优化指南——高级篇](https://tech.meituan.com/2016/05/12/spark-tuning-pro.html)<br>
[2][Spark如何处理数据倾斜](https://blog.csdn.net/kaede1209/article/details/81145560)
[3][Flink设置并行度的几种方式](http://www.mamicode.com/info-detail-2957062.html)




### 甘特图 [<a href="https://mermaid-js.github.io/mermaid/#/gantt">文档</a> - <a href="https://mermaid.live/edit#base64:eyJjb2RlIjoiZ2FudHRcbnNlY3Rpb24gU2VjdGlvblxuQ29tcGxldGVkIDpkb25lLCAgICBkZXMxLCAyMDE0LTAxLTA2LDIwMTQtMDEtMDhcbkFjdGl2ZSAgICAgICAgOmFjdGl2ZSwgIGRlczIsIDIwMTQtMDEtMDcsIDNkXG5QYXJhbGxlbCAxICAgOiAgICAgICAgIGRlczMsIGFmdGVyIGRlczEsIDFkXG5QYXJhbGxlbCAyICAgOiAgICAgICAgIGRlczQsIGFmdGVyIGRlczEsIDFkXG5QYXJhbGxlbCAzICAgOiAgICAgICAgIGRlczUsIGFmdGVyIGRlczMsIDFkXG5QYXJhbGxlbCA0ICAgOiAgICAgICAgIGRlczYsIGFmdGVyIGRlczQsIDFkIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifX0">live editor</a>]

```
gantt
    section Section
    Completed :done,    des1, 2014-01-06,2014-01-08
    Active        :active,  des2, 2014-01-07, 3d
    Parallel 1   :         des3, after des1, 1d
    Parallel 2   :         des4, after des1, 1d
    Parallel 3   :         des5, after des3, 1d
    Parallel 4   :         des6, after des4, 1d
```
```mermaid
gantt
    section Section
    Completed :done,    des1, 2014-01-06,2014-01-08
    Active        :active,  des2, 2014-01-07, 3d
    Parallel 1   :         des3, after des1, 1d
    Parallel 2   :         des4, after des1, 1d
    Parallel 3   :         des5, after des3, 1d
    Parallel 4   :         des6, after des4, 1d
```
