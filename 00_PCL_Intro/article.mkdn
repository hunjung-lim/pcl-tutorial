
## Python-PCL
- 본 챕터에서는 PCL의 Python버젼인 [Python-PCL](http://strawlab.github.io/python-pcl/)의 기본적인 파일 입력, Numpy변환, 저장 방법에 대하여 정리 하였습니다. 


```python
%load_ext watermark
%watermark -d -v -p pcl,numpy
```

    2018-11-22 
    
    CPython 2.7.12
    IPython 5.8.0
    
    pcl unknown
    numpy 1.15.4



```python
import pcl
import numpy as np

import os
os.chdir("/workspace/3D_People_Detection_Tracking") 
```

## Point cloud 생성

### 배열로 생성


```python
pc_array = np.array([[1, 2, 3], [3, 4, 5]], dtype=np.float32)
print(pc_array)
```

    [[1. 2. 3.]
     [3. 4. 5.]]



```python
#방법 1
pc = pcl.PointCloud(pc_array)
print(pc)
```

    <PointCloud of 2 points>



```python
#방법 2
pc = pcl.PointCloud()
pc.from_array(pc_array)
print(pc)
```

    <PointCloud of 2 points>


### PCD 파일 읽기


```python
pc = pcl.load("./sample/lobby.pcd") # "pc.from_file" Deprecated
print(pc)
```

    <PointCloud of 19329 points>


## 정보 확인


```python
print("포인트 수 : {}".format(pc.size))
```

    포인트 수 : 19329



```python
print ('Loaded ' + str(pc.width * pc.height) + ' data points from test_pcd.pcd with the following fields: ')

for i in range(0, 10):#pc.size):
    print ('x: ' + str(pc[i][0]) + ', y : ' + str(pc[i][1]) + ', z : ' + str(pc[i][2]))

```

    Loaded 19329 data points from test_pcd.pcd with the following fields: 
    x: 5.55542087555, y : 0.753095984459, z : -1.50218582153
    x: 36.1922683716, y : 4.89982938766, z : 0.637501478195
    x: 6.65287637711, y : 0.899506211281, z : -1.54991281033
    x: 23.4230003357, y : 3.16274738312, z : 1.23868751526
    x: 8.19875049591, y : 1.1070561409, z : -1.60813832283
    x: 23.224275589, y : 3.13178706169, z : 2.05025148392
    x: 10.7360458374, y : 1.44585025311, z : -1.71577334404
    x: 23.258348465, y : 3.12811613083, z : 2.88147902489
    x: 15.3596839905, y : 2.06306147575, z : -1.90286803246
    x: 32.7645950317, y : 4.38918924332, z : 6.42568445206


## Numpy로 변환 

- 추후 군집화, 분류, 전처리를 위해서 일반적으로 Numpy로 변환 하여 작업을 수행 


```python
pc_array = pc.to_array()
print("pc Type : {}".format(type(pc)))
print("pc_array Type : {}".format(type(pc_array)))
```

    pc Type : <type 'pcl._pcl.PointCloud'>
    pc_array Type : <type 'numpy.ndarray'>


### Numpy 기반 정보 출력


```python
print("pc_array shape : {}".format(pc_array.shape))
print("pc_array size : {}".format(pc_array.size))
print("pc_array ndim : {}".format(pc_array.ndim))
print("pc_array dtype : {}".format(pc_array.dtype))
print("pc_array nbytes : {} bytes".format(pc_array.nbytes))
```

    pc_array shape : (19329, 3)
    pc_array size : 57987
    pc_array ndim : 2
    pc_array dtype : float32
    pc_array nbytes : 231948 bytes


## pcd로 저장 

### point cloud를 pcd로 저장


```python
# 방법 1
pcl.save(pc, 'pc2pcd.pcd') 
#pcl.save_XYZRGBA(pc, 'pc2pcd.pcd') #RGB-D센서에서 주로 사용, x,y,z좌표 이외 색상 정보 포함 
```


```python
# 방법 2
pc.to_file('pc2pcd.pcd')
```




    0



### numpy를 pcd로 저장


```python
pc_new = pcl.PointCloud()
pc_new.from_array(pc_array)
pc_new.to_file('pc2pcd.pcd')
```




    0


