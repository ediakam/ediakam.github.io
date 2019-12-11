**1）find/findOne**

	db.tablename.find("key":"value") //返回所有符合的结果
	db.tablename.findOne("key":"value") //返回符合结果的第一个

**2）.pretty()**

	db.tablename.find({"key":"value"}).pretty()

找到表中的数据含有这个key value的所有元素并且对其格式化(没有pretty在linux显示的是一连串) findOne自带这个功能

3）查询所有用户id为1000001的数据，_id索引字段不显示（0表示不显示，1表示显示，默认显示）：

	db.user_info.find({"customerId" : 1000001},{"_id" : 0}).pretty();

4）显示表的所有索引：

	db.tablename.getIndexes()  

MongoDB：linux基本操作：[https://www.cnblogs.com/adamans/articles/9111110.html](https://www.cnblogs.com/adamans/articles/9111110.html])

MongoDb 命令查询所有数据库列表：[https://blog.csdn.net/u010305706/article/details/48129131](https://blog.csdn.net/u010305706/article/details/48129131)

windows连接MongoDB工具：NoSQL Manager for MongoDB