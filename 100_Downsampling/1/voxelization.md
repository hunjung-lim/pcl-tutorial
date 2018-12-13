
## Voxelization 

본 챕터에서는 다운샘플링 기법중 하나인 voxelizattion 방법에 대하여 다루고 있습니다. 

3D velxel Grid는 `Point의 집합`로 이루어진 대상을 `Voxel의 집합`으로 표현하는 것을 의미합니다. 

> 복셀(voxel) : 3차원 공간에서 정규 격자 단위의 값을 나타낸다. 복셀이라는 용어는 부피 (volume)와 픽셀 (pixel)을 조합한 혼성어 [[wikipedia]](https://ko.wikipedia.org/wiki/%EB%B3%B5%EC%85%80)

자세한 내용은 [Downsampling a PointCloud using a VoxelGrid filter](http://pointclouds.org/documentation/tutorials/voxel_grid.php#voxelgrid)를 참고 하시면 됩니다.  




{:.input_area}
```python
%load_ext watermark
%watermark -d -v -p pcl,numpy
```


{:.output_stream}
```
The watermark extension is already loaded. To reload it, use:
  %reload_ext watermark
2018-11-23 

CPython 3.5.2
IPython 6.4.0

pcl unknown
numpy 1.14.5

```



{:.input_area}
```python
# -*- coding: utf-8 -*-
from __future__ import print_function
import pcl
import numpy as np

import os
os.chdir("/workspace/3D_People_Detection_Tracking") 
```


## Voxelization 정의

입력 
- pcl_data : point cloud
- leaf_size : Vox 크기

출력  
- voxelized point cloud



{:.input_area}
```python
def do_voxel_grid_downssampling(pcl_data,leaf_size):
    '''
    Create a VoxelGrid filter object for a input point cloud
    :param pcl_data: point cloud data subscriber
    :param leaf_size: voxel(or leaf) size
    :return: Voxel grid downsampling on point cloud
    :https://github.com/fouliex/RoboticPerception
    '''
    vox = pcl_data.make_voxel_grid_filter()
    vox.set_leaf_size(leaf_size, leaf_size, leaf_size) # The bigger the leaf size the less information retained
    return  vox.filter()
```


## PCD 파일 읽기



{:.input_area}
```python
cloud = pcl.load("./sample/lobby.pcd") # Deprecated; use pcl.load instead.
print(cloud)
```


{:.output_stream}
```
<PointCloud of 19329 points>

```

## Voxelization 수행



{:.input_area}
```python
LEAF_SIZE = 0.01 #RGB-D센서의 경우 0.01 추천, Lidar의 경우 좀더 큰값 추천 
cloud = do_voxel_grid_downssampling(cloud,LEAF_SIZE)
print(cloud)
```


{:.output_stream}
```
<PointCloud of 19329 points>

```



{:.input_area}
```python
LEAF_SIZE = 0.1 #RGB-D센서의 경우 0.01 추천, Lidar의 경우 좀더 큰값 추천 
cloud = do_voxel_grid_downssampling(cloud,LEAF_SIZE)
print(cloud)
```


{:.output_stream}
```
<PointCloud of 9413 points>

```



{:.input_area}
```python
LEAF_SIZE = 1.0 #RGB-D센서의 경우 0.01 추천, Lidar의 경우 좀더 큰값 추천 
cloud = do_voxel_grid_downssampling(cloud,LEAF_SIZE)
print(cloud)
```


{:.output_stream}
```
<PointCloud of 1171 points>

```



