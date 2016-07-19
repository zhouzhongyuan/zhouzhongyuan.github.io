#Mongodb常用命令
##Hello,mongo
```bash
cd mongodb安装位置/bin
```
```bash
./mongo
```
```bash
show dbs
```

##结构
````bash
|--db
|----collection
|------------data
````
###data的CRUD
#### C
```bash
db.releases.insert({"appId" : "com.bokesoft.zijiang", "Name" : "紫江", "UUID" : "7921b97f-c7c2-461b-8cc6-bab66f514324"})
```
#### R(ead)
```bash
db.releases.find({Name:'国资委'})

```
#### U(pdate)
```bash
db.releases.update({Name:'国资委'},{$set:{Name:'移动办公'}})
```
#### D(elete)
```bash
db.releases.remove({Name:'国资委'})
```



###collection的CRUD
#### C
```bash
db.createCollection('mobileprovisions', { appId: 'string',
                              Name: 'string',
                              UUID: 'string'} )
```
#### R(ead)
```bash

```
#### U(pdate)
```bash
```
#### D
```
db.releases.drop()
```


1. help: db.helpC()
1. dbs： show dbs
1. CREATE DB : use DATABASE_NAME
1. 进入数据库：use **
1. collections： show collections

          db.mobileprovisions.find("Name":{$not:/^c*/}) //查找Name 不是以c开头的

update:  

INSERT
```mongodb
({appPackageName:"com.bokesoft.app",appPlatform:"android"})

copy collections(tables)

db.<collection_name>.find().forEach(function(d){ db.getSiblingDB('<new_database>')['<collection_name>'].insert(d); });
```

CREATE Collection:
db.createCollection('mobileprovisions', { appId: 'string',
                              Name: 'string',
                              UUID: 'string'} )
                              
##More
[Why does mongoose always add an s to the end of my collection name](http://stackoverflow.com/questions/10547118/why-does-mongoose-always-add-an-s-to-the-end-of-my-collection-name)

https://docs.mongodb.org/getting-started/shell/update/
https://docs.mongodb.org/manual/core/crud-introduction/
https://docs.mongodb.org/manual/core/query-optimization/
https://docs.mongodb.org/manual/reference/method/db.collection.remove/
https://docs.mongodb.org/manual/reference/operator/query/