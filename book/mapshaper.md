# mapshaper

## 简介

[mapshaper](https://github.com/mbloch/mapshaper) 是
[Matthew Bloch](https://github.com/mbloch) 用 node.js 写的。这个
工具可以编辑 Shapefile, GeoJSON, TopoJSON, CSV 等地图格式。

在 echarts 地图编辑的过程中，她主要用来消除地图内部边界线。

## 安装

```
npm install -g mapshaper
```

## 命令形式

```
mapshaper your_shape_with_internal_borders.geojson -dissolve2 -o your_shape_contoure.geojson
```
