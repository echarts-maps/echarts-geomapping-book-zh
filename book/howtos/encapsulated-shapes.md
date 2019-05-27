# 给和田地区镶上昆玉市

## 地理常识

昆玉市是在2016年中国国务院批准成立的，所以[新疆地图](https://github.com/pyecharts/jupyter-echarts/issues/10)需要更新。

## 小技术挑战

因为和田地区包围了昆玉市，所以用[给天津市补上蓟洲区](add-ji-zhou-qu-to-tianjin)的方式行不通的。怎么办？

## geojson 的解决方案

geojson 的 "MultiPolygon" 支持挖洞。

```
{
  "type": "MultiPolygon",
  "coordinates": [
    [
      {polygon},
      {hole},
      {hole},
      {hole}
    ]
  ]
}
```

解决方案就是把和田地区的 geojson 把昆玉市作为一个洞挖出去，这样用[给天津市补上蓟洲区](add-ji-zhou-qu-to-tianjin)的方式就行得通了。

## 具体细节

1. 先用 geojson.io 把昆玉市画出来
1. 把昆玉市和新疆地图合起来
1. 再给原有的和田地区挖个洞

```
var maker = require("echarts-mapmaker/src/maker");

maker.cut('merged_xinjiang.json', '和田地区', '昆玉市');
```

### 参考

[echarts-china-provinces-js 的处理细节](https://github.com/echarts-maps/echarts-china-provinces-js/blob/master/build/tasks/xinjiang.js)