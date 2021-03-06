# FQC-mongodb

## 客户端安装

```
npm install gqc-mongodb --save
```

## 客户端使用

```
const gqc_mongodb = require("gqc-mongodb");
// 安装到tcp实例上
gqc_mongodb.install(socket);

// 组件使用前必须声明using-App
yield client.useApp("Gaubee", "123456", "QAQ");

// 进行初始化连接，得到DB对象
// [DB](http://mongodb.github.io/node-mongodb-native/2.0/api/MongoClient.html#.connect)
const db = yield client.mongodbClient(["mongodb://localhost:27017/test"]);

// 使用DB实例化出collection对象
// [Collection](http://mongodb.github.io/node-mongodb-native/2.0/api/Collection.html)
const clo = yield db.collection("test_correctly_access_collections");

// 插入，返回Promise对象
var _insert = yield clo.insert({
 name: "Gaubee"
});
console.log(_insert);

// 查询，返回Cursor对象
// [Cusror](http://mongodb.github.io/node-mongodb-native/2.0/api/Cursor.html)
yield clo.find({}).toArray();
yield clo.find({}).limit(2).skip(2).toArray();

yield col.find({
    _id: ["ObjectID", "@", 56d3de33f37222a4521b2012] // BSON的对象在JSON中的表达方式
});

```

### BSON

Mongodb中有以下几种特殊的数据类型：
* Binary
* Code
* Map
* DBRef
* Double
* Long
* MinKey
* MaxKey
* ObjectID
* ObjectId
* Symbol
* Timestamp

使用JSON表达的方式统一的格式：
```js
[ TYPE_NAME , "@" , ...args ]

// == 转化为代码 ==>

mongodb[TYPE_NAME]( ...args )
```


## 服务端安装
```
npm install gqc-mongodb --save --server
```

## 服务端（提供Mongodb数据服务的一端）使用

```
const gqc_mongodb = require("gqc-mongodb");
// 安装到tcp实例上
gqc_mongodb.install(socket);

// 组件使用前必须声明using-App
yield client.useApp("Gaubee", "123456", "QAQ");

// 注册数据服务组件
yield client.mongodbServer();
```