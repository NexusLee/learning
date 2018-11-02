#### 1. custom autorun
```
this.myDep = new Tracker.Dependency();

Tracker.autorun((comp) => {

  this.myDep.depend();

  console.log("Something has happened!");

});

this.myDep.changed();
```
