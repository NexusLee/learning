#### 1. custom autorun
```
this.myDep = new Tracker.Dependency();

Tracker.autorun((comp) => {

  this.myDep.depend();

  console.log("Something has happened!");

});

this.myDep.changed();
```

#### 2. 手动断开连接
```
(Meteor as any).connection.disconnect();
```

#### 3. 重新连接
```
(Meteor as any).connection.reconnect();
```

#### 4. 连接状态
```
(Meteor as any).connection.status();
```

#### 5. meteor client collection list
```
(Meteor as any).connection._mongo_livedata_collections;
or
(Meteor as any).connection._stores
```
