#### 插入数据：INSERT INTO 语句 ####

**1.插入所有字段：**    
    
	INSERT INTO 表名 VALUES（字段1值，字段2值...）

**2. 插入指定字段：**
    
	INSERT INTO 表名(字段1，字段2...) VALUES (字段1值，字段2值...)

**3. 插入多行数据：**

	INSERT INTO 表名 VALUES(字段1值，字段2值..),(字段1值，字段2值..)

#### 删除数据：DELETE ####

**1. 删除某行数据：**

	DELETE FROM 表名 WHERE 字段名=值（条件）

**2. 删除整个表的数据：**

清空数据表内容，不释放空间，即：下次插入表数据，自动递增值的字段依然接着删除数据继续增加

	DELETE FROM 表名
	或 DELETE * FROM 表名

#### 清空表数据：TRUNCATE ####

TRUNCATE 清空表数据，释放空间，即：下次插入表数据，自动递增值的字段重新开始）

	TRUNCATE TABLE 表名

#### 修改数据：UPDATE ####

**1. 更改某行数据的某个字段：**

	UPDATE 表名 SET 字段名 = 新值 WHERE 字段名 = 值（条件）

**2. 更改某行数据的多个字段：**

	UPDATE 表名 SET 字段1 = 新值,字段2 = 新值 WHERE 字段名 =值（条件）

#### 查询数据：SELECT ####

**1. 查询所有列：**

	SELECT * FROM 表名

**2. 查询某一列：**

	SELECT 字段1,字段2 FROM 表名

**3. 根据条件查询数据：**

	SELECT * FROM 表名 WHERE 字段 运算符 值

在 WHERE 语句中使用的运算符：

| 运算符 | 描述 | 备注 |
| :-----| :---- | :---- |
| = | 等于 |  |
| <> 或 != | 不等于 |  |
| > | 大于 |  |
| < | 小于 |  |
| >= | 大于等于 |  |
| <= | 小于等于 |  |
| BETWEEN | 在某个范围内 | BETWEEN 10 and 50（≥10且≤50） |
| IN | 在某集合内 | IN (3763,1057) （3763或1057） |
| LIKE | 搜索某种模式 | % 通配任意字符，_通配单一字符 |
| NOT 或 ! | 逻辑非 | NOT IN 不在某个合集内 |
| OR 或 &#124 | 逻辑或 | 使用多个OR或AND时，使用括号以免计算出错 |
| AND或 && | 逻辑与 |  |

**4. 去重查询：**

DISTINCT 用于返回不同的值，去掉重复的值

	SELECT DISTINCT 字段名 FROM 表名

**5. 查询结果排序显示：ORDER BY**

默认升序，降序则使用 DESC
	
- 升序

	`SELECT * FROM 表名 ORDER BY 字段名`

- 多个字段排序时，用逗号，隔开

	`SELECT * FROM 表名 ORDER BY 字段1,字段2`

- 降序

	`SELECT * FROM 表名 ORDER BY 字段 DESC`

- 升序降序混合使用

	`SELECT * FROM 表名 ORDER BY 字段1 DESC,字段2 ASC`

**6. 统计查询：**

- COUNT() 计算行数

	`SELECT COUNT(*) FROM 表名`

- AVG() 求平均函数

	`SELECT AVG(字段名) FROM 表名`

- SUM() 求总和

	`SELECT SUM(字段名) FROM 表名`

- MIN() 求最小

	`SELECT MIN(字段名) FROM 表名`

- MAX() 求最大

	`SELECT MAX(字段名) FROM 表名`

- 分组查询 GROUP BY

	`SELECT SUM(字段) FROM 表名 GROUP BY 分组字段`

实例：SELECT subscription_id,SUM(pay_price) FROM orders GROUP BY subscription_id

注：查询每种类型的订阅价格总和

转自：[https://www.jianshu.com/p/8796188a79ef](https://www.jianshu.com/p/8796188a79ef)
