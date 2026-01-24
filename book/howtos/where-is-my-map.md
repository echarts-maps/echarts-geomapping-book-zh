# 为什么是空地图？

以斐济地图为例子，我们看到的地图是空的。

<img src="../../image/Fiji.png" alt="where is fiji" width="400"/>

那先看看地图是不是空的。我们先把js解压成geojson，

```
decompress echarts-countries-js/Fiji.js Fiji.geojson
```

然后，打开geojson.io


<img src="../../image/geojson.png" alt="geojson.io" width="400"/>

上传Fiji.geojson，查看一下，

<img src="../../image/Fiji-geojson.png" alt="fiji" width="400"/>

地图上有斐济，那么是什么问题呢？试试用鼠标移动画布，能看到什么吗？

<img src="../../image/Fiji-2.png" alt="where is fiji" width="400"/>

能猜到吗？地图存在，是地图的中心问题。哪怎么办呢？先在gejson.io上找斐济的中心，

<img src="../../image/Fiji-3.png" alt="where is fiji" width="400"/>

然后，geojson.io会告诉你中心的坐标，

<img src="../../image/Fiji-4.png" alt="where is fiji" width="400"/>

再在 echarts 里用**center**参数。

```
斐济: { center: [178.47489094528436, -17.82254817978705]}
```

最后，地图还是小？哪用**zoom**参数调大地图就好了。