### 集合collections
#### OrderedDict
```
from collections import OrderedDict
od = OrderedDict()
od['z'] = 1
od['y'] = 2
od['z'] = 3
OrderedDict([('z', 1), ('y', 2), ('x', 3)])
```
#### namedtuple
```
from collections import namedtuple
Point = namedtuple('Point', ['x','y'])
p = Point(1, 2)
p.x => 1
p.y => 2
```

### 列表list
```
list = [1, 2, 3, 4, 5, 6, 7 ]
```

#### 列表访问
```
list[0] => 1
list[1:5] => [2, 3, 4, 5]
```
#### 列表更新
```
list[6] = 8 => [1,2,3,4,5,6,8] 
list.append(8) => [1,2,3,4,5,6,7,8]
```
#### 列表删除
```
del list[6] => [1,2,3,4,5,6] 
```
