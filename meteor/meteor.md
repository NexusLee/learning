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

#### 5. meteor 客户端 collection list
```
(Meteor as any).connection._mongo_livedata_collections;
or
(Meteor as any).connection._stores
```
#### 6. meteor 创建客户端 collection 并监听服务端
##### client
```
let sharedState = new MongoObservable.Collection('collectionname');
sharedState.collection.find({}).observe({ //监听一次客服正在输入中
    "added": function(item) {
        // your code
    }
});
```
##### server
```
Meteor.publish('Typing', function(obj) {
    let publication = this;
    publication.added( 'collectionname', 'time', {date: new Date()} );
})
```

