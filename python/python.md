### 一、collections
##### OrderedDict
```
from collections import OrderedDict
od = OrderedDict()
od['z'] = 1
od['y'] = 2
od['z'] = 3
OrderedDict([('z', 1), ('y', 2), ('x', 3)])
```
##### namedtuple
```
from collections import namedtuple
Point = namedtuple('Point', ['x','y'])
p = Point(1, 2)
p.x => 1
p.y => 2
```

### 二、list
```
list = [1, 2, 3, 4, 5, 6, 7 ]
```

##### list访问
```
list[0] => 1
list[1:5] => [2, 3, 4, 5]
```
##### list更新
```
list[6] = 8 => [1,2,3,4,5,6,8] 
list.append(8) => [1,2,3,4,5,6,7,8]
```
##### list删除
```
del list[6] => [1,2,3,4,5,6] 
```
### 三、set
##### set创建
```
s = set()
s = { 11, 22, 33, 44 }
```
```
s = set('boy')
s = set(['a', 'b', 'c'])
s = set({'key1': 'value1', 'key2': 'value2'})
s = { 'boy', 'girl' }
s = { ('a', 'b', 'c') }
```
```
se = { 11, 22, 33 }
be = { 22, 55 }
se.difference(be) => { 11, 33 }
se.difference_update(be) => { 11, 33 }
```
```
se = { 11, 22, 33 }
se.discard(11)
se.discard(44) => No Error
```
```
se = { 11, 22, 33 }
se.remove(11)
se.remove(44) => Error
```
```
se = { 11, 22, 33 }
temp = se.pop() => 33
```
