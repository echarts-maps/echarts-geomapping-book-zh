# mapmaker

## 简介

[echarts-mapmaker](https://github.com/echarts-maps/echarts-mapmaker) 的前身是
[echarts-map-tool](https://github.com/ecomfe/echarts-map-tool)。mapmaker 是给 echarts 地图开发人员设计的命令，
而 echarts-map-tool 是以网页形式存在的地图定制器。

## 主要功能

### 压缩 geojson

echarts 可以接受标准的 geojson 进行画图。同时 echarts 团队有自己独特的压缩格式，用万国码编码 geojson (UTF8 encoded geojson)。这种
压缩方式是会一定丢失精度，但精度是可调的。这种编码现今只有 echarts 支持。类似的格式有[Topojson](https://github.com/topojson/topojson)，
由数据可视化的沙皇 [Mike Bostock](https://github.com/mbostock) 创立的，并有一系列的衍生工具。二者虽然同时存在，但都想解决同一个
问题：给标准 geojson 的文件减肥。在互联网时代，下载量越小，用户看到地图的时间越快，提升用户体验。
[举个例子](https://github.com/echarts-maps/echarts-united-kingdom-js)，标准的英国 2017 投票地图接近 188 MB，

用 mapmaker 做万国码编码之后，地图的缩小到 9.9 MB, 缩小 20 倍。

## 解压 geojson

前面提到了， 用万国码编码 geojson 是 echarts 团队有自己独特的压缩格式。所以，需要得到标准的 geojson 的画，就需要 mapmaker 做解压。

## 简单的地图编辑：合并，拆分

mapmaker 可以把一个独立的地图合并到另一个地图里。另外，有些地图有多个多边形，比如北京有很多区，朝阳区，海淀区等。mapmaker 可以把这样一个地图内部的区全部独立出来。
