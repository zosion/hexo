---
title: MongoDB
date: 2018-08-30 11:24:40
tags: Learning
comments: true
toc: true
---
#

## 什么是MongoDB

* /usr/local/Cellar/mongodb/4.0.1/bin » ./mongo

MongoDB 是由C++语言编写的，是一个基于分布式文件存储的开源数据库系统。
在高负载的情况下，添加更多的节点，可以保证服务器性能。
MongoDB 旨在为WEB应用提供可扩展的高性能数据存储解决方案。
MongoDB 将数据存储为一个文档，数据结构由键值(key=>value)对组成。MongoDB 文档类似于 JSON 对象。字段值可以包含其他文档，数组及文档数组。
<!-- more -->

### 主要特点

* MongoDB 是一个面向文档存储的数据库，操作起来比较简单和容易。
* 你可以在MongoDB记录中设置任何属性的索引 (如：FirstName="Sameer",Address="8 Gandhi Road")来实现更快的排序。
* 你可以通过本地或者网络创建数据镜像，这使得MongoDB有更强的扩展性。
* 如果负载的增加（需要更多的存储空间和更强的处理能力） ，它可以分布在计算机网络中的其他节点上这就是所谓的分片。
* Mongo支持丰富的查询表达式。查询指令使用JSON形式的标记，可轻易查询文档中内嵌的对象及数组。
* MongoDb 使用update()命令可以实现替换完成的文档（数据）或者一些指定的数据字段 。
* Mongodb中的Map/reduce主要是用来对数据进行批量处理和聚合操作。
* Map和Reduce。Map函数调用emit(key,value)遍历集合中所有的记录，将key与value传给Reduce函数进行处理。
* Map函数和Reduce函数是使用Javascript编写的，并可以通过db.runCommand或mapreduce命令来执行MapReduce操作。
* GridFS是MongoDB中的一个内置功能，可以用于存放大量小文件。
* MongoDB允许在服务端执行脚本，可以用Javascript编写某个函数，直接在服务端执行，也可以把函数的定义存储在服务端，下次直接调用即可。
* MongoDB支持各种编程语言:RUBY，PYTHON，JAVA，C++，PHP，C#等多种语言。

### 概念解析

|SQL术语/概念|MongoDB术语/概念|解释/说明|
|:-|:-|:-|
|database|database|数据库|
|table|collection|数据库表/集合|
|row|document|数据记录行/文档|
|column|field|数据字段/域|
|index|index|索引|
|table joins||表连接,MongoDB不支持|
|primary key|primary key|主键,MongoDB自动将_id字段设置为主键|

### 数据库

* 一个mongodb中可以建立多个数据库。
* MongoDB的默认数据库为"db"，该数据库存储在data目录中。
* MongoDB的单个实例可以容纳多个独立的数据库，每一个都有自己的集合和权限，不同的数据库也放置在不同的文件中。

> "show dbs" 命令可以显示所有数据的列表。
> 执行 "db" 命令可以显示当前数据库对象或集合。
> 运行"use"命令，可以连接到一个指定的数据库。

数据库也通过名字来标识。数据库名可以是满足以下条件的任意UTF-8字符串。

* 不能是空字符串（"")。
* 不得含有' '（空格)、.、$、/、\和\0 (空字符)。
* 应全部小写。
* 最多64字节。

有一些数据库名是保留的，可以直接访问这些有特殊作用的数据库。

* admin： 从权限的角度来看，这是"root"数据库。要是将一个用户添加到这个数据库，这个用户自动继承所有数据库的权限。一些特定的服务器端命令也只能从这个数据库运行，比如列出所有的数据库或者关闭服务器。
* local: 这个数据永远不会被复制，可以用来存储限于本地单台服务器的任意集合
* config: 当Mongo用于分片设置时，config数据库在内部使用，用于保存分片的相关信息。

### 文档

**文档**是一组键值(**key-value**)对(即 **BSON** )。MongoDB 的文档不需要设置相同的字段，并且相同的字段不需要相同的数据类型，这与关系型数据库有很大的区别，也是 MongoDB 非常突出的特点。
一个简单的文档例子如下：
> {"site":"www.runoob.com", "name":"菜鸟教程"}

需要注意的是：

1. 文档中的键/值对是 **有序** 的。
2. 文档中的值不仅可以是在双引号里面的字符串，还可以是其他几种数据类型（甚至可以是整个嵌入的文档)。
3. MongoDB区分 **类型** 和 **大小写**。
4. MongoDB的文档 **不能有重复的键**。
5. 文档的键是 **字符串**。除了少数例外情况，键可以使用任意UTF-8字符。

文档键命名规范:

* 键不能含有\0 (空字符)。这个字符用来表示键的结尾。
* .和$有特别的意义，只有在特定环境下才能使用。
* 以下划线"_"开头的键是保留的(不是严格要求的)。

### 集合

**集合**就是 MongoDB 文档组，类似于 RDBMS （关系数据库管理系统：Relational Database Management System)中的表格。
集合存在于数据库中，集合没有固定的结构，这意味着你在对集合可以插入不同格式和类型的数据，但通常情况下我们插入集合的数据都会有一定的关联性。
比如，我们可以将以下不同数据结构的文档插入到集合中:
> {"site":"www.baidu.com"}
> {"site":"www.google.com","name":"Google"}
> {"site":"www.runoob.com","name":"菜鸟教程","num":5}

当第一个文档插入时，集合就会被创建。

#### 合法的集合名

* 集合名不能是空字符串""。
* 集合名不能含有\0字符（空字符)，这个字符表示集合名的结尾。
* 集合名不能以"system."开头，这是为系统集合保留的前缀。
* 用户创建的集合名字不能含有保留字符。有些驱动程序的确支持在集合名里面包含，这是因为某些系统生成的集合中包含该字符。除非你要访问这种系统创建的集合，否则千万不要在名字里出现$。

如下实例：
> db.col.findOne()

#### capped collections

Capped collections 就是固定大小的collection。
它有很高的性能以及队列过期的特性(过期按照插入的顺序). 有点和 "RRD" 概念类似。
Capped collections是高性能自动的维护对象的插入顺序。它非常适合类似记录日志的功能 和标准的collection不同，你必须要显式的创建一个capped collection， 指定一个collection的大小，单位是字节。collection的数据存储空间值提前分配的。
要注意的是指定的存储大小包含了数据库的头信息。
> db.createCollection("mycoll", {capped:true, size:100000})

* 在capped collection中，你能添加新的对象。
* 能进行更新，然而，对象不会增加存储空间。如果增加，更新就会失败 。
* 数据库不允许进行删除。使用drop()方法删除collection所有的行。
* 注意: 删除之后，你必须显式的重新创建这个collection。
* 在32bit机器中，capped collection最大存储为1e9( 1X109)个字节。

### 元数据

数据库的信息是存储在集合中。它们使用了系统的命名空间：
> dbname.system.*

在MongoDB数据库中名字空间 dbname.system.* 是包含多种系统信息的特殊集合(Collection)，如下:

|集合命名空间|描述|
|:-|:-|
|dbname.system.namespaces|列出所有名字空间。|
|dbname.system.indexes|列出所有索引。|
|dbname.system.profile|包含数据库概要(profile)信息。|
|dbname.system.users|列出所有可访问数据库的用户。|
|dbname.local.sources|包含复制对端（slave）的服务器信息和状态。|

对于修改系统集合中的对象有如下限制。
在{{system.indexes}}插入数据，可以创建索引。但除此之外该表信息是不可变的(特殊的drop index命令将自动更新相关信息)。
{{system.users}}是可修改的。 {{system.profile}}是可删除的。

### MongoDB 数据类型

|数据类型|描述|
|:-|:-|
|String|字符串。存储数据常用的数据类型。在 MongoDB 中，UTF-8 编码的字符串才是合法的。|
|Integer|整型数值。用于存储数值。根据你所采用的服务器，可分为 32 位或 64 位。|
|Boolean|布尔值。用于存储布尔值（真/假）。|
|Double|双精度浮点值。用于存储浮点值。|
|Min/Max keys|将一个值与 BSON（二进制的 JSON）元素的最低值和最高值相对比。|
|Array|用于将数组或列表或多个值存储为一个键。|
|Timestamp|时间戳。记录文档修改或添加的具体时间。|
|Object|用于内嵌文档。|
|Null|用于创建空值。|
|Symbol|符号。该数据类型基本上等同于字符串类型，但不同的是，它一般用于采用特殊符号类型的语言。|
|Date|日期时间。用 UNIX 时间格式来存储当前日期或时间。你可以指定自己的日期时间：创建Date 对象，传入年月日信息。|
|Object ID|对象 ID。用于创建文档的 ID。|
|Binary Data|二进制数据。用于存储二进制数据。|
|Code|代码类型。用于在文档中存储 JavaScript 代码。|
|Regular expression|正则表达式类型。用于存储正则表达式。|

## 连接数据库

启动 MongoDB 服务
> 只需要在 MongoDB 安装目录的 bin 目录下执行 mongodb 即可。

标准 URI 连接语法：
> mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]

* mongodb:// 这是固定的格式，必须要指定。
* username:password@ 可选项，如果设置，在连接数据库服务器之后，驱动都会尝试登陆这个数据库
* host1 必须的指定至少一个host, host1 是这个URI唯一要填写的。它指定了要连接服务器的地址。如果要连接复制集，请指定多个主机地址。
* portX 可选的指定端口，如果不填，默认为27017
* /database 如果指定username:password@，连接并验证登陆指定数据库。若不指定，默认打开 test 数据库。
* ?options 是连接选项。如果不使用/database，则前面需要加上/。所有连接选项都是键值对name=value，键值对之间通过&或;（分号）隔开

标准的连接格式包含了多个选项(options)

|选项|描述|
|:-|:-|
|replicaSet=name|验证replica set的名称。 Impliesconnect=replicaSet.|
|slaveOk=true/false|true:在connect=direct模式下，驱动会连接第一台机器，即使这台服务器不是主。在connect=replicaSet模式下，驱动会发送所有的写请求到主并且把读取操作分布在其他从服务器。false: 在 connect=direct模式下，驱动会自动找寻主服务器. 在connect=replicaSet 模式下，驱动仅仅连接主服务器，并且所有的读写命令都连接到主服务器。|
|safe=true/false|true: 在执行更新操作之后，驱动都会发送getLastError命令来确保更新成功。(还要参考 wtimeoutMS).false: 在每次更新之后，驱动不会发送getLastError来确保更新成功。|
|w=n|驱动添加 { w : n } 到getLastError命令. 应用于safe=true。|
|wtimeoutMS=ms|驱动添加 { wtimeout : ms } 到 getlasterror 命令. 应用于 safe=true.|
|fsync=true/false|true: 驱动添加 { fsync : true } 到 getlasterror 命令.应用于 safe=true.false: 驱动不会添加到getLastError命令中。|
|journal=true/false|如果设置为 true, 同步到 journal (在提交到数据库前写入到实体中). 应用于 safe=true|
|connectTimeoutMS=ms|可以打开连接的时间。|
|socketTimeoutMS=ms|发送和接受sockets的时间。|

## 数据库操作

### 创建数据库

如果数据库不存在，则创建数据库，否则切换到指定数据库。
> use DATABASE_NAME
  >> 注意: 在 MongoDB 中，集合只有在内容插入后才会创建! 就是说，创建集合(数据表)后要再插入一个文档(记录)，集合才会真正创建

### 删除数据库

删除当前数据库，默认为 test
> b.dropDatabase()

## 集合操作

### 创建集合

> db.createCollection(name, options)

参数说明：

* name: 要创建的集合名称
* options: 可选参数, 指定有关内存大小及索引的选项

|字段|类型|描述|
|:-|:-|:-|
|capped|布尔|（可选）如果为 true，则创建固定集合。固定集合是指有着固定大小的集合，当达到最大值时，它会自动覆盖最早的文档。**当该值为 true 时，必须指定 size 参数。**|
|autoIndexId|布尔|（可选）如为 true，自动在 _id 字段创建索引。默认为 false。|
|size|数值|可选）为固定集合指定一个最大值（以字节计）。**如果 capped 为 true，也需要指定该字段。**|
|max|数值|（可选）指定固定集合中包含文档的最大数量。|

### 删除集合

> db.collection.drop()
**返回值:**如果成功删除选定集合，则 drop() 方法返回 true，否则返回 false。

## 文档操作

文档的数据结构和JSON基本一样。
所有存储在集合中的数据都是BSON格式。
BSON是一种类json的一种二进制形式的存储格式,简称Binary JSON。

### 插入文档

MongoDB 使用 insert() 或 save() 方法向集合中插入文档
> db.COLLECTION_NAME.insert(document)

查看已插入文档
> db.COLLECTION_NAME.find()

插入文档你也可以使用 **db.COLLECTION_NAME.save(document)** 命令。如果不指定 _id 字段 save() 方法类似于 insert() 方法。如果指定 _id 字段，则会更新该 _id 的数据。

3.2 版本后还有以下几种语法可用于插入文档:

* db.collection.insertOne():向指定集合中插入一条文档数据
* db.collection.insertMany():向指定集合中插入多条文档数据

### 更新文档

#### update()

MongoDB 使用 **update()** 和 **save()** 方法来更新集合中的文档
update() 方法用于更新已存在的文档

```javascript
db.collection.update(
   <query>,
   <update>,
   {
     upsert: <boolean>,
     multi: <boolean>,
     writeConcern: <document>
   }
)
```

参数说明：

* **query** : update的查询条件，类似sql update查询内where后面的。
* **update** : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
* **upsert** : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
* **multi** : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
* **writeConcern** :可选，抛出异常的级别。
  * WriteConcern.NONE:没有异常抛出
  * WriteConcern.NORMAL:仅抛出网络错误异常，没有服务器错误异常
  * WriteConcern.SAFE:抛出网络错误异常、服务器错误异常；并等待服务器完成写操作。
  * WriteConcern.MAJORITY: 抛出网络错误异常、服务器错误异常；并等待一个主服务器完成写操作。
  * WriteConcern.FSYNC_SAFE: 抛出网络错误异常、服务器错误异常；写操作等待服务器将数据刷新到磁盘。
  * WriteConcern.JOURNAL_SAFE:抛出网络错误异常、服务器错误异常；写操作等待服务器提交到磁盘的日志文件。
  * WriteConcern.REPLICAS_SAFE:抛出网络错误异常、服务器错误异常；等待至少2台服务器完成写操作。

实例：

```javascript
>db.col.insert({
  title: 'MongoDB 教程',
  description: 'MongoDB 是一个 Nosql 数据库',
  by: '菜鸟教程',
  url: 'http://www.runoob.com',
  tags: ['mongodb', 'database', 'NoSQL'],
  likes: 100
})

// 接着我们通过 update() 方法来更新标题(title):
>db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })   # 输出信息
> db.col.find().pretty()
{
  "_id" : ObjectId("56064f89ade2f21f36b03136"),
  "title" : "MongoDB",
  "description" : "MongoDB 是一个 Nosql 数据库",
  "by" : "菜鸟教程",
  "url" : "http://www.runoob.com",
  "tags" : [
          "mongodb",
          "database",
          "NoSQL"
  ],
  "likes" : 100
}
```

以上语句只会修改第一条发现的文档，如果你要修改多条相同的文档，则需要设置 multi 参数为 true。
`>db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}},{multi:true})`

在3.2版本开始，MongoDB提供以下更新集合文档的方法：

* db.collection.updateOne() 向指定集合更新单个文档
* db.collection.updateMany() 向指定集合更新多个文档

#### save()

save() 方法通过传入的文档来替换已有文档

```javascript
db.collection.save(
   <document>,
   {
     writeConcern: <document>
   }
)
```

参数说明：

* **document** : 文档数据。
* **writeConcern** :可选，抛出异常的级别。

实例

```javascript
// 替换 _id 为 56064f89ade2f21f36b03136 的文档数据
>db.col.save({
  "_id" : ObjectId("56064f89ade2f21f36b03136"),
  "title" : "MongoDB",
  "description" : "MongoDB 是一个 Nosql 数据库",
  "by" : "Runoob",
  "url" : "http://www.runoob.com",
  "tags" : [
          "mongodb",
          "NoSQL"
  ],
  "likes" : 110
})

>db.col.find().pretty()
{
  "_id" : ObjectId("56064f89ade2f21f36b03136"),
  "title" : "MongoDB",
  "description" : "MongoDB 是一个 Nosql 数据库",
  "by" : "Runoob",
  "url" : "http://www.runoob.com",
  "tags" : [
          "mongodb",
          "NoSQL"
  ],
  "likes" : 110
}
```

### 删除文档

删除集合下全部文档：
`db.inventory.deleteMany({})`
删除 status 等于 A 的全部文档：
`db.inventory.deleteMany({ status : "A" })`
删除 status 等于 D 的一个文档：
`db.inventory.deleteOne( { status: "D" } )`

### 查询文档

find() 方法以非结构化的方式来显示所有文档
> db.collection.find(query, projection)

pretty() 方法以格式化的方式来显示所有文档。
> db.collection.find().pretty()

limit()方法接受一个数字参数，该参数指定从MongoDB中读取的记录条数。
> db.collection.find().limit(NUMBER)

使用skip()方法来跳过指定数量的数据，skip方法同样接受一个数字参数作为跳过的记录条数。
> db.collection.find().limit(NUMBER).skip(NUMBER)

sort() 方法对数据进行排序，sort() 方法可以通过参数指定排序的字段，并使用 1 和 -1 来指定排序的方式，其中 1 为升序排列，而 -1 是用于降序排列。
> db.collection.find().sort({KEY:1})

注意：**skip(), limilt(), sort()三个放在一起执行的时候，执行的顺序是先 sort(), 然后是 skip()，最后是显示的 limit()。**

* query ：可选，使用查询操作符指定查询条件
* projection ：可选，使用投影操作符指定返回的键。查询时返回文档中所有键值， 只需省略该参数即可（默认省略）。

若不指定 projection，则默认返回所有键，指定 projection 格式如下，有两种模式
> db.collection.find(query, {title: 1, by: 1}) // inclusion模式 指定返回的键，不返回其他键
> db.collection.find(query, {title: 0, by: 0}) // exclusion模式 指定不返回的键,返回其他键

_id 键默认返回，需要主动指定 _id:0 才会隐藏
两种模式不可混用（因为这样的话无法推断其他键是否应返回）
> db.collection.find(query, {title: 1, by: 0}) // 错误

只能全1或全0，除了在inclusion模式时可以指定_id为0
>db.collection.find(query, {_id:0, title: 1, by: 1}) // 正确

若不想指定查询条件参数 query 可以 用 {} 代替，但是需要指定 projection 参数：
> querydb.collection.find({}, {title: 1})

#### Where 语句

|操作|格式|范例|
|:-|:-|:-|
|小于|`{<key>:{$lt:<value>}}`|db.col.find({"likes":{$lt:50}}).pretty()|
|小于或等于|`{<key>:{$lte:<value>}}`|db.col.find({"likes":{$lte:50}}).pretty()|
|大于|`{<key>:{$gt:<value>}}`|db.col.find({"likes":{$gt:50}}).pretty()|
|大于或等于|`{<key>:{$gte:<value>}}`|db.col.find({"likes":{$gte:50}}).pretty()|
|等于|`{<key>:<value>}`|db.col.find({"by":"菜鸟教程"}).pretty()|
|不等于|`{<key>:{$ne:<value>}}`|db.col.find({"likes":{$ne:50}}).pretty()|

#### AND 条件

> db.col.find({key1:value1, key2:value2}).pretty()

#### OR 条件

```javascript
db.col.find(
   {
      $or: [
         {key1: value1}, {key2:value2}
      ]
   }
).pretty()
```

#### 模糊查询

> db.col.find({title:/^教$/}) //使用正则匹配

## 索引

索引是特殊的数据结构，索引存储在一个易于遍历读取的数据集合中，索引是对数据库表中一列或多列的值进行排序的一种结构

### createIndex() 方法

> db.collection.createIndex(keys, options)

* Key 值为你要创建的索引字段，1 为指定按升序创建索引，-1 为指定按降序创建索引

createIndex() 方法中你也可以设置使用多个字段创建索引（关系型数据库中称作复合索引）。
> db.collection.createIndex({"title":1,"description":-1})

options 可选参数列表如下：

|Parameter|Type|Description|
|:-|:-|:-|
|background|Boolean|建索引过程会阻塞其它数据库操作，background可指定以后台方式创建索引，即增加 "background" 可选参数。 "background" 默认值为false。|
|unique|Boolean|建立的索引是否唯一。指定为true创建唯一索引。默认值为false.|
|name|string|索引的名称。如果未指定，MongoDB的通过连接索引的字段名和排序顺序生成一个索引名称。|
|sparse|Boolean|对文档中不存在的字段数据不启用索引；这个参数需要特别注意，如果设置为true的话，在索引字段中不会查询出不包含对应字段的文档.。默认值为 false.|
|expireAfterSeconds|integer|指定一个以秒为单位的数值，完成 TTL设定，设定集合的生存时间。|
|v|index version|索引的版本号。默认的索引版本取决于mongod创建索引时运行的版本。|
|weights|document|索引权重值，数值在 1 到 99,999 之间，表示该索引相对于其他索引字段的得分权重。|
|default_language|string|对于文本索引，该参数决定了停用词及词干和词器的规则的列表。 默认为英语|
|language_override|string|对于文本索引，该参数指定了包含在文档中的字段名，语言覆盖默认的language，默认值为 language.|

> db.collection.createIndex({open: 1, close: 1}, {background: true})

## 聚合

MongoDB中聚合(aggregate)主要用于处理数据(诸如统计平均值,求和等)，并返回计算后的数据结果。有点类似sql语句中的 count(*)。

### aggregate() 方法

> db.collection.aggregate(AGGREGATE_OPERATION)

|表达式|描述|实例|
|:-|:-|:-|
|$sum|计算总和。|`db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : "$likes"}}}])`|
|$avg|计算平均值|`db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$avg : "$likes"}}}])`|
|$min|获取集合中所有文档对应值得最小值。|`db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$min : "$likes"}}}])`|
|$max|获取集合中所有文档对应值得最大值。|`db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$max : "$likes"}}}])`|
|$push|在结果文档中插入值到一个数组中。|`db.mycol.aggregate([{$group : {_id : "$by_user", url : {$push: "$url"}}}])`|
|$addToSet|在结果文档中插入值到一个数组中，但不创建副本。|`db.mycol.aggregate([{$group : {_id : "$by_user", url : {$addToSet : "$url"}}}])`|
|$first|根据资源文档的排序获取第一个文档数据。|`db.mycol.aggregate([{$group : {_id : "$by_user", first_url : {$first : "$url"}}}])`|
|$last|根据资源文档的排序获取最后一个文档数据|`db.mycol.aggregate([{$group : {_id : "$by_user", last_url : {$last : "$url"}}}])`|

### 管道的概念

管道在Unix和Linux中一般用于将当前命令的输出结果作为下一个命令的参数。
MongoDB的聚合管道将MongoDB文档在一个管道处理完毕后将结果传递给下一个管道处理。管道操作是可以重复的。
表达式：处理输入文档并输出。表达式是无状态的，只能用于计算当前聚合管道的文档，不能处理其它的文档。
这里我们介绍一下聚合框架中常用的几个操作：

* $project：修改输入文档的结构。可以用来重命名、增加或删除域，也可以用于创建计算结果以及嵌套文档。
* $match：用于过滤数据，只输出符合条件的文档。$match使用MongoDB的标准查询操作。
* $limit：用来限制MongoDB聚合管道返回的文档数。
* $skip：在聚合管道中跳过指定数量的文档，并返回余下的文档。
* $unwind：将文档中的某一个数组类型字段拆分成多条，每条包含数组中的一个值。
* $group：将集合中的文档分组，可用于统计结果。
* $sort：将输入文档排序后输出。
* $geoNear：输出接近某一地理位置的有序文档。

## 复制（副本集）

MongoDB复制是将数据同步在多个服务器的过程。
复制提供了数据的冗余备份，并在多个服务器上存储数据副本，提高了数据的可用性， 并可以保证数据的安全性。
复制还允许您从硬件故障和服务中断中恢复数据。

### 复制原理

mongodb的复制至少需要两个节点。其中一个是主节点，负责处理客户端请求，其余的都是从节点，负责复制主节点上的数据。
mongodb各个节点常见的搭配方式为：一主一从、一主多从。
主节点记录在其上的所有操作oplog，从节点定期轮询主节点获取这些操作，然后对自己的数据副本执行这些操作，从而保证从节点的数据与主节点一致

#### 副本集特征：

* N 个节点的集群
* 任何节点可作为主节点
* 所有写入操作都在主节点上
* 自动故障转移
* 自动恢复

### 副本集设置

> mongod --port "PORT" --dbpath "YOUR_DB_DATA_PATH" --replSet "REPLICA_SET_INSTANCE_NAME"

### 副本集添加成员

> rs.add(HOST_NAME:PORT)

## 分片

在Mongodb里面存在另一种集群，就是分片技术,可以满足MongoDB数据量大量增长的需求。
当MongoDB存储海量的数据时，一台机器可能不足以存储数据，也可能不足以提供可接受的读写吞吐量。这时，我们就可以通过在多台机器上分割数据，使得数据库系统能存储和处理更多的数据。

为什么使用分片:

* 复制所有的写入操作到主节点
* 延迟的敏感数据会在主节点查询
* 单个副本集限制在12个节点
* 当请求量巨大时会出现内存不足。
* 本地磁盘不足
* 垂直扩展价格昂贵

## 备份(mongodump)与恢复(mongorestore)

### 数据备份

在Mongodb中我们使用mongodump命令来备份MongoDB数据。该命令可以导出所有数据到指定目录中。
mongodump命令可以通过参数指定导出的数据量级转存的服务器。

> mongodump -h dbhost -d dbname -o dbdirectory

* -h：MongDB所在服务器地址，例如：127.0.0.1，当然也可以指定端口号：127.0.0.1:27017
* -d：需要备份的数据库实例，例如：test
* -o：备份的数据存放位置，例如：c:\data\dump，当然该目录需要提前建立，在备份完成后，系统自动在dump目录下建立一个test目录，这个目录里面存放该数据库实例的备份数据。

mongodump 命令可选参数列表如下所示：

|语法|描述|实例|
|:-|:-|:-|
|mongodump --host HOST_NAME --port PORT_NUMBER|该命令将备份所有MongoDB数据|`mongodump --host runoob.com --port 27017`|
|mongodump --dbpath DB_PATH --out BACKUP_DIRECTORY||`mongodump --dbpath /data/db/ --out /data/backup/`|
|mongodump --collection COLLECTION --db DB_NAME|该命令将备份指定数据库的集合。|`mongodump --collection mycol --db test`|

### 数据恢复

mongodb使用 mongorestore 命令来恢复备份的数据。
> mongorestore -h `<hostname><:port>` -d dbname `<path>`

* --host <:port>, -h <:port>：MongoDB所在服务器地址，默认为： localhost:27017
* --db , -d ：需要恢复的数据库实例，例如：test，当然这个名称也可以和备份时候的不一样，比如test2
* --drop：恢复的时候，先删除当前数据，然后恢复备份的数据。就是说，恢复后，备份后添加修改的数据都会被删除，慎用哦！
* `<path>`：mongorestore 最后的一个参数，设置备份数据所在位置，例如：c:\data\dump\test。你不能同时指定 `<path>` 和 --dir 选项，--dir也可以设置备份目录。
* --dir：指定备份的目录。你不能同时指定 `<path>` 和 --dir 选项。

## 监控

在你已经安装部署并允许MongoDB服务后，你必须要了解MongoDB的运行情况，并查看MongoDB的性能。这样在大流量得情况下可以很好的应对并保证MongoDB正常运作。
MongoDB中提供了mongostat 和 mongotop 两个命令来监控MongoDB的运行情况。

### mongostat 命令

mongostat是mongodb自带的状态检测工具，在命令行下使用。它会间隔固定时间获取mongodb的当前运行状态，并输出。如果你发现数据库突然变慢或者有其他问题的话，你第一手的操作就考虑采用mongostat来查看mongo的状态。
启动你的Mongod服务，进入到你安装的MongoDB目录下的bin目录， 然后输入mongostat命令，如下所示：
> /usr/local/Cellar/mongodb/4.0.1/bin>mongostat

### mongotop 命令

mongotop也是mongodb下的一个内置工具，mongotop提供了一个方法，用来跟踪一个MongoDB的实例，查看哪些大量的时间花费在读取和写入数据。 mongotop提供每个集合的水平的统计数据。默认情况下，mongotop返回值的每一秒。
启动你的Mongod服务，进入到你安装的MongoDB目录下的bin目录， 然后输入mongotop命令，如下所示：
> /usr/local/Cellar/mongodb/4.0.1/bin>mongotop

## Node.js 连接 MongoDB

> npm install mongodb

### 创建数据库N

```javascript
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/runoob";

MongoClient.connect(url, function(err, db) {
  if (err) throw err;
  console.log("数据库已创建!");
  db.close();
});
```

### 创建集合 createCollection()

```javascript
var MongoClient = require('mongodb').MongoClient;
var url = 'mongodb://localhost:27017/runoob';
MongoClient.connect(url, function (err, db) {
    if (err) throw err;
    console.log('数据库已创建');
    var dbase = db.db("runoob");
    dbase.createCollection('site', function (err, res) {
        if (err) throw err;
        console.log("创建集合!");
        db.close();
    });
});
```

### 数据库操作( CURD )

与 MySQL 不同的是 MongoDB 会自动创建数据库和集合，所以使用前我们不需要手动去创建。

#### 插入数据 insertOne()/insertMany()

```javascript
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";

MongoClient.connect(url, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    var myobj = { name: "菜鸟教程", url: "www.runoob" };
    dbo.collection("site").insertOne(myobj, function(err, res) {
        if (err) throw err;
        console.log("文档插入成功");
        db.close();
    });
});

ar MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";

MongoClient.connect(url, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    var myobj =  [
        { name: '菜鸟工具', url: 'https://c.runoob.com', type: 'cn'},
        { name: 'Google', url: 'https://www.google.com', type: 'en'},
        { name: 'Facebook', url: 'https://www.google.com', type: 'en'}
       ];
    dbo.collection("site").insertMany(myobj, function(err, res) {
        if (err) throw err;
        console.log("插入的文档数量为: " + res.insertedCount);
        db.close();
    });
});
```

#### 查询数据

find() 可以返回匹配条件的所有数据。 如果未指定条件，find() 返回集合中的所有数据。

```javascript
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";

MongoClient.connect(url, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
     var whereStr = {"name":'菜鸟教程'};  // 查询条件
    dbo.collection("site").find(whereStr).toArray(function(err, result) {
        if (err) throw err;
        console.log(result);
        db.close();
    });
});
```

#### 更新数据 updateOne()/updateMany()

```javascript
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";

MongoClient.connect(url, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    var whereStr = {"name":'菜鸟教程'};  // 查询条件
    var updateStr = {$set: { "url" : "https://www.runoob.com" }};
    dbo.collection("site").updateOne(whereStr, updateStr, function(err, res) {
        if (err) throw err;
        console.log("文档更新成功");
        db.close();
    });
});

var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";

MongoClient.connect(url, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    var whereStr = {"type":'en'};  // 查询条件
    var updateStr = {$set: { "url" : "https://www.runoob.com" }};
    dbo.collection("site").updateMany(whereStr, updateStr, function(err, res) {
        if (err) throw err;
         console.log(res.result.nModified + " 条文档被更新");
        db.close();
    });
});
```

#### 删除数据 deleteOne()/deleteMany()

```javascript
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";

MongoClient.connect(url, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    var whereStr = { type: "en" };  // 查询条件
    dbo.collection("site").deleteMany(whereStr, function(err, obj) {
        if (err) throw err;
        console.log(obj.result.n + " 条文档被删除");
        db.close();
    });
});
```

#### 排序

sort() 方法，该方法接受一个参数，规定是升序(1)还是降序(-1)。

```javascript
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";

MongoClient.connect(url, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    var mysort = { type: 1 };
    dbo.collection("site").find().sort(mysort).toArray(function(err, result) {
        if (err) throw err;
        console.log(result);
        db.close();
    });
});
```

#### 查询分页

设置指定的返回条数可以使用 limit() 方法，该方法只接受一个参数，指定了返回的条数。
如果要指定跳过的条数，可以使用 skip() 方法。

```javascript
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";

MongoClient.connect(url, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    dbo.collection("site").find().limit(2).toArray(function(err, result) {
        if (err) throw err;
        console.log(result);
        db.close();
  });
});

var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";

MongoClient.connect(url, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    dbo.collection("site").find().skip(2).limit(2).toArray(function(err, result) {
        if (err) throw err;
        console.log(result);
        db.close();
  });
});
```

#### 连接操作

mongoDB 不是一个关系型数据库，但我们可以使用 **$lookup** 来实现左连接。
例如我们有两个集合数据分别为：

集合1：orders
> `[{ _id: 1, product_id: 154, status: 1 }]`

集合2：products
> `[{ _id: 154, name: '笔记本电脑' },{ _id: 155, name: '耳机' },{ _id: 156, name: '台式电脑' }]`

```javascript
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://127.0.0.1:27017/";

MongoClient.connect(url, function(err, db) {
  if (err) throw err;
  var dbo = db.db("runoob");
  dbo.collection('orders').aggregate([
    { $lookup:
       {
         from: 'products',            // 右集合
         localField: 'product_id',    // 左集合 join 字段
         foreignField: '_id',         // 右集合 join 字段
         as: 'orderdetails'           // 新生成字段（类型array）
       }
     }
    ]).toArray(function(err, res) {
    if (err) throw err;
    console.log(JSON.stringify(res));
    db.close();
  });
});
```

#### 删除集合drop()

```javascript
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";

MongoClient.connect(url, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    // 删除 test 集合
    dbo.collection("test").drop(function(err, delOK) {  // 执行成功 delOK 返回 true，否则返回 false
        if (err) throw err;
        if (delOK) console.log("集合已删除");
        db.close();
    });
});
```