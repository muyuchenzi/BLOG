直接利用geopandas.GeoDataFrame.crs=
{'proj': 'latlong', 'ellps': 'WGS84', 'datum': 'WGS84', 'no_defs': True}//WGS84坐标系
{'proj': 'utm', 'zone': 31, 'ellps': 'WGS84', 'datum': 'WGS84', 'units': 'm', 'no_defs': True}
//常用的转坐标系用UTM-31
实在是找不到特别好的解决办法，目测是geopandas与pyproj的版本问题。上次升级之后能用，这次不知道哪里出现了问题，家里的可以用。
这个作为一个临时的解决办法。


import geopandas as gpd

gpf=gpd.read_file(r'D:\muyuchenzi\code\current\JustFun\geopandas数据包检验\下载_有路名.shp',encoding='utf-8')

# gpf.crs={'proj': 'latlong', 'ellps': 'WGS84', 'datum': 'WGS84', 'no_defs': True}
# result = gpf.to_crs({'proj': 'utm', 'zone': 31, 'ellps': 'WGS84', 'datum': 'WGS84',
 'units': 'm', 'no_defs': True})
#
# result_buffer_1km=result.buffer(1000)
# gpf.crs={'init':'epsg:4326'}

gpf.crs={'init':'epsg:4326'}
xx=gpf.to_crs({'init':'epsg:4549'})

import pyproj
print(pyproj.__version__)

xx.to_file(r'D:\muyuchenzi\code\current\JustFun\geopandas数据包检验\测试\018.shp',encoding='utf-8')

然后又莫名其妙的好了，pyproj的问题真的是非常非常扯淡，anaconda的版本默认安装的是1.9.6，然后就是出现问题了，然后卸载1.9.6，由于
geopandas的关联包有pyproj，然后应该保存的是1.9.5.1，然后出现一个b'no arguments in initialization list'错误，然后重新更新到
2.2.0版本，然后安装就解决了这个问题，应该是anaconda的安装机制的问题。真的是非常非常扯淡的东西，耽误了我大概很多零碎的时间。