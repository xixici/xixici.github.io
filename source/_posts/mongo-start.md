---
title: mongo自我书写
date: 2019-02-15 21:46:39
tags: mongo
categories: 学习笔记
---
# MongoDB简介

MongoDB 是由C++语言编写的，是一个基于分布式文件存储的开源数据库系统。
在高负载的情况下，添加更多的节点，可以保证服务器性能。
MongoDB 旨在为WEB应用提供可扩展的高性能数据存储解决方案。
MongoDB 将数据存储为一个文档，数据结构由键值(key=>value)对组成。MongoDB 文档类似于 JSON 对象。字段值可以包含其他文档，数组及文档数组。
<!--more-->
# MongoDB概念
与关系型数据库的区别在于 
- 表 -> 集合
- 行 -> 文档
- 列 -> 域
同时不支持连接查询

SQL术语/概念 |	MongoDB术语/概念 |	解释/说明
database |	database |	数据库
table	 | collection |	数据库表/集合
row |	document |	数据记录行/文档
column	| field |	数据字段/域
index	| index |	索引
table  joins |	 	表连接,MongoDB不支持
primary key |	primary key |	主键,MongoDB自动将_id字段设置为主键

# MongoDB增删改查

## MongoDB插入文档
MongoDB 使用 insert() 或 save() 方法向集合中插入文档，语法如下：
- db.COLLECTION_NAME.insert(document)

## MongoDB更新文档
update() 方法用于更新已存在的文档。语法格式如下：
```
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
query : update的查询条件，类似sql update查询内where后面的。

update : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的

upsert : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。

multi : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。

writeConcern :可选，抛出异常的级别。

## MongoDB 删除文档
remove() 方法的基本语法格式如下所示：
```
db.collection.remove(
   <query>,
   <justOne>
)
如果你的 MongoDB 是 2.6 版本以后的，语法格式如下：
db.collection.remove(
   <query>,
   {
     justOne: <boolean>,
     writeConcern: <document>
   }
)
```

参数说明：
query :（可选）删除的文档的条件。
justOne : （可选）如果设为 true 或 1，则只删除一个文档。

writeConcern :（可选）抛出异常的级别。

## MongoDB查询文档
MongoDB 查询数据的语法格式如下：
- db.collection.find(query, projection)
query ：可选，使用查询操作符指定查询条件
projection ：可选，使用投影操作符指定返回的键。查询时返回文档中所有键值， 只需省略该参数即可（默认省略）。
如果你需要以易读的方式来读取数据，可以使用 pretty() 方法，语法格式如下：
- db.col.find().pretty()
pretty() 方法以格式化的方式来显示所有文档。

# MongoDB操作符

MongoDB中条件操作符有：
```
$gt -------- greater than  >

$gte --------- gt equal  >=

$lt -------- less than  <

$lte --------- lt equal  <=

$ne ----------- not equal  !=

$eq  --------  equal  =

$type 
```

$type操作符是基于BSON类型来检索集合中匹配的数据类型，并返回结果。
MongoDB 中可以使用的类型如下表所示：
```
类型	数字	备注
Double	1	 
String	2	 
Object	3	 
Array	4	 
Binary data	5	 
Undefined	6	已废弃。
Object id	7	 
Boolean	8	 
Date	9	 
Null	10	 
Regular Expression	11	 
JavaScript	13	 
Symbol	14	 
JavaScript (with scope)	15	 
32-bit integer	16	 
Timestamp	17	 
64-bit integer	18	 
Min key	255	Query with -1.
Max key	127	 
```

# MongoDB基本方法
## MongoDB Limit() 方法
如果你需要在MongoDB中读取指定数量的数据记录，可以使用MongoDB的Limit方法，limit()方法接受一个数字参数，该参数指定从MongoDB中读取的记录条数。
语法
limit()方法基本语法如下所示：
- db.COLLECTION_NAME.find().limit(NUMBER)

## MongoDB Skip() 方法
我们除了可以使用limit()方法来读取指定数量的数据外，还可以使用skip()方法来跳过指定数量的数据，skip方法同样接受一个数字参数作为跳过的记录条数。
语法
skip() 方法脚本语法格式如下：
- db.COLLECTION_NAME.find().limit(NUMBER).skip(NUMBER)
想要读取从 10 条记录后 100 条记录，相当于 sql 中limit (10,100)。
- db.COLLECTION_NAME.find().skip(10).limit(100)

## MongoDB sort()方法
在MongoDB中使用使用sort()方法对数据进行排序，sort()方法可以通过参数指定排序的字段，并使用 1 和 -1 来指定排序的方式，其中 1 为升序排列，而-1是用于降序排列。
语法
sort()方法基本语法如下所示：
- db.COLLECTION_NAME.find().sort({KEY:1})

## ensureIndex() 方法
MongoDB使用 ensureIndex() 方法来创建索引。
语法
ensureIndex()方法基本语法格式如下所示：
- db.COLLECTION_NAME.ensureIndex({KEY:1})
语法中 Key 值为你要创建的索引字段，1为指定按升序创建索引，如果你想按降序来创建索引指定为-1即可。

## aggregate() 方法
MongoDB中聚合的方法使用aggregate()。
语法
aggregate() 方法的基本语法格式如下所示：
>db.COLLECTION_NAME.aggregate(AGGREGATE_OPERATION)
---------
表达式	|	描述	|		实例
$sum	|		计算总和。	|		db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : "$likes"}}}])
$avg		|	计算平均值		|	db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$avg : "$likes"}}}])
$min		|	获取集合中所有文档对应值得最小值。	|		db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$min : "$likes"}}}])
$max		|	获取集合中所有文档对应值得最大值。	|		db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$max : "$likes"}}}])
$push		|	在结果文档中插入值到一个数组中。		|	db.mycol.aggregate([{$group : {_id : "$by_user", url : {$push: "$url"}}}])
$addToSet		|	在结果文档中插入值到一个数组中，但不创建副本。		|	db.mycol.aggregate([{$group : {_id : "$by_user", url : {$addToSet : "$url"}}}])
$first		|	根据资源文档的排序获取第一个文档数据。	|		db.mycol.aggregate([{$group : {_id : "$by_user", first_url : {$first : "$url"}}}])
$last		|	根据资源文档的排序获取最后一个文档数据		|	db.mycol.aggregate([{$group : {_id : "$by_user", last_url : {$last : "$url"}}}])
----------

```
db.getCollection('testCollection').aggregate([{$group : {label : "$label", num_tutorial : {$sum : 1}}}])
```
对label聚合,查询各个label条数

## mongo导入CSV文件
mongoimport -h 172.20.3.10:27017 --db fourClassify --collection allTrainCollection --type csv --headerline --file D:/all_train_data.csv


## mongo导出CSV文件
mongoexport -h 172.20.3.10:27017 --db fourClassify --collection testCollection --type=csv --fieldFile D:/fieldFile.txt --out D:/1.csv
