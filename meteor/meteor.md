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
