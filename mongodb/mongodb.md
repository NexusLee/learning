## mongodb

#### 字符串批量替换
```
db.XLChatUser.find({"Icon" : /vbooking/}).forEach(
    function(item){   	
      	item.Icon = item.Icon.replace('vbooking.net', 'iflying.com')
      	db.XLChatUser.save(item);
    }
)
```
```
db.Poster.find({"PicUrl.Url" : /vbooking/}).forEach(
    function(item){   
      	print(item.PicUrl) 
      	var tmp = item.PicUrl;
      	tmp.forEach(function(item1) { 
      		item1.Url = item1.Url.replace('vbooking.net', 'iflying.com')      	    	
      	})  	     	
      	db.Poster.save(item);
    }
)
```
```
db.XLChatRoom.find({ "UserInfos.Icon": /vbooking/ }).forEach(
    function(item){    
        var tmp = item.UserInfos;
        tmp.forEach(function(item1) { 
            if(item1.Icon && item1.Icon !== null) {
            item1.Icon = item1.Icon.replace('vbooking.net', 'iflying.com')
            }
        })  
    db.XLChatRoom.save(item);
})

db.XLChatRoom.find({ "GroupIcon": /vbooking/ }).forEach(
    function(item){   
        if(item.GroupIcon && item.GroupIcon !== null){ 
            item.GroupIcon = item.GroupIcon.replace('vbooking.net', 'iflying.com')
            db.XLChatRoom.save(item);       
    }
})
```
```
db.XLChatMessageRecord.find({ $or: [ {"Sender.Icon": /vbooking/}, {"Recver.Icon": /vbooking/} ]  }).forEach(
    function(item){    
        if(item.Recver.Icon && item.Recver.Icon !== null){
          item.Recver.Icon = item.Recver.Icon.replace('vbooking.net', 'iflying.com')
        }
        if(item.Sender.Icon && item.Sender.Icon !== null){
          item.Sender.Icon = item.Sender.Icon.replace('vbooking.net', 'iflying.com')
        }
    db.XLChatMessageRecord.save(item);         
})
```

#### 查看查询执行状态
```
db.test.find()..explain('executionStats')
```
