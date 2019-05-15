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
##### set比较
```
se = { 11, 22, 33 }
be = { 22, 55 }
se.difference(be) => { 11, 33 }
se.difference_update(be) => { 11, 33 }
```
##### set删除
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
##### set交集
```
se = { 11, 22, 33 }
be = { 22, 55 }
temp1 = se.intersection(be)
temp1 => { 22 }
se = { 11, 22, 33 }
temp2 = se.intersection_update(be)
temp2 => None
se => { 22 }
```
##### set判断
```
se = { 11, 22, 33 }
be = { 22 }
se.isdisjoint(be) => False
se.issubset(be) => False
se.isuperset(be) => True
```
##### set合并
```
se = { 11, 22, 33 }
be = { 22 }
temp1 = se.symmertric_difference(be)
temp1 => { 11, 33 }
se = { 11, 22, 33 }
temp2 = se.symmertric_difference_update(be)
temp2 => None
se = { 11, 33 }
```
##### set并集
```
se = { 11, 22, 33 }
be = { 22, 55 }
temp = se.union(be)
temp => { 11, 22, 33, 55 }
```
##### set更新
```
se = { 11, 22, 33 }
be = { 22, 55 }
se.update(be)
se => { 11, 22, 33, 55 }
se.update([66, 77])
se => { 11, 22, 33, 66, 77 }
```
##### set转换
```
se = set(range(4))
li = list(se) => [0, 1, 2, 3]
tu = tuple(se) => (0, 1, 2, 3) 
st = str(se) => {0, 1, 2, 3}
```

##### python 本地安装

python setup.py install
