# 使用台湾政府资料开放平台的地图

承[瑞士地图的制作](switzerland.md)，大家应该已经装了[GDAL](../tools/gdal.md)

1. 首先把[地图包](https://data.gov.tw/dataset/7441)下载下来。
1. 下载之后，解压缩
1. 使用 `og2ogr` 命令，转换地图格式，

   ```
   ogr2ogr -f GeoJSON taiwan.geojson TOWN_MOI_1100415.shp
   ```

4 然后我们可以先看一下地图数据全不全

   <img src="../../image/taiwan-preview.png" alt="taiwan preview" width="400"/>

## 在 echarts 里显示，还需做什么处理

1. 下载的地图没有市县分级。所以需要根据他们市县名来组合一下。

```
import os
import json

database = defaultdict(list)

with open('taiwan.json', 'r') as f:
    features = json.load(f)

for feature in features['features']:
    town_id = feature['properties']['TOWNID']
    county_name = feature['properties']['COUNTYNAME']
    feature['properties']['name'] = feature['properties']['TOWNNAME']
    database[county_name].append(feature)

for county_name in database:
    geojson = {
        "type": "FeatureCollection",
        "features": database[county_name]
    }
    with open(f'{county_name}.geojson', 'w') as f:
        print(f'Writing {county_name}...')
        json.dump(geojson, f)
        print('Done')
```

2 这样我们就生成了市县的地图。

   <img src="../../image/taibei.png" alt="taiwan preview" width="300"/>

3 要是需要就生成了市县下一级的地图呢，我写这么一个脚本：

```
import os
import json

try:
    os.mkdir('taiwan')
except FileExistsError:
    pass

for feature in features['features']:
    town_name = feature['properties']['TOWNNAME']
    county_name = feature['properties']['COUNTYNAME']
    try:
        os.mkdir('taiwan/' + county_name)
    except FileExistsError:
        pass
    geojson = {
        "type": "FeatureCollection",
        "features": [feature]
    }
    with open(f'taiwan/{county_name}/{town_name}.geojson', 'w') as f:
        print(f'Writing {county_name}/{town_name}...')
        json.dump(geojson, f)
        print('Done')
```

4 这样我们可以看看下级地图：

<img src="../../image/taiwan_district.png" alt="taiwan preview" width="500"/>

## UTF8 encoding

echarts 是可以读geojson的。要是放在网站，就需要把文件变小，你可以用mapmaker compress 命令。当然，我也有做好现成的图，您可以看github上的台湾地图。

写到最后，您可以请我一杯咖啡，让我知道我写的这本秘籍真正帮助到了您。

<img src="../../image/tips.jpg" alt="drawing" width="300"/>
