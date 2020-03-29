# 分组查询 

## 1.分组函数

### 1.1分组函数分类

  sum求和、max min count（计算个数） 

各个函数支持的参数类型
sum avg一般处理数值类型

```sql
SELECT SUM(salary) FROM employees;
SELECT round(avg(salary)) FROM employees;
SELECT max(salary) FROM employees;
SELECT min(salary) FROM employees;
SELECT count(salary) FROM employees;
SELECT SUM(salary) FROM employees;
```



## 2.分组语法：

​	select 分组函数，列（要求出现在group by的后面）
​	from 表 【where 筛选条件】 分组的列表
​	【order by 子句】

注意： 
查询列表必须特殊，要求是分组函数和group by 后出现的字段

## 3.分组函数特点

### 	3.1、分组查询中的筛选条件分为两类

​								数据源                位置                 关键字
​		分组前筛选	原始表             GROUP BY子句的前面   		WHERE
​		分组后的筛选 分组后的结果集    GROUP BY子句的后面面     HAVING
​		分组函数做条件肯定放在having子句中
​		能用分组前筛选的就优先考虑分组前筛选

###   3.2、GROUP BY

 ROUP BY子句支持单个字段分组，多个字段分组（多字段之间用逗号隔开没有顺序要求），表达式或者函数（这两个用的比较少）

注 分组函数都忽略null

### 	3.3、也可以添加排序值（排序放在整个分组查询的最后）

### 3.4下面的语句也可以看出具体的关键词的先后顺序

```sql
SELECT AVG(salary),department_id,job_id FROM employees GROUP BY department_id,job_id HAVING AVG(salary)>10000 ORDER BY AVG(salary) DESC
```



## 4.各个案例

### 案例一 查询每个工种的最高工资

```sql
SELECT max(salary),job_id FROM employees GROUP BY job_id
```



### 查询邮箱中包含a字符的，每个人部门的平均工资

```sql
SELECT max(salary),department_id FROM employees WHERE email like '%a%' GROUP BY department_id;
```



### 添加分组后的再进行筛选需要用到having函数

```sql
SELECT max(salary),department_id FROM employees WHERE email like '%a%' GROUP BY department_id HAVING department_id>90;

SELECT max(salary),department_id FROM employees WHERE email like '%a%' GROUP BY department_id HAVING max(salary)>10000;
```



### 按表达式或者函数分组

#案例：按员工的姓名长度分组，查询每一组的员工个数，筛选员工个数>5的有哪些

```sql
SELECT count(*),LENGTH(last_name) len_name FROM employees GROUP BY LENGTH(last_name)

SELECT count(*),LENGTH(last_name) len_name FROM employees GROUP BY LENGTH(last_name) HAVING COUNT(*)>5
```



### 安多各字段分组

#案例 查询每个部门每个工种的员工的平均工资

SELECT AVG(salary),department_id,job_id FROM employees GROUP BY department_id,job_id #两个id一致的才会被分到同一个组

### 添加排序

```sql
SELECT AVG(salary),department_id,job_id FROM employees GROUP BY department_id,job_id HAVING AVG(salary)>10000 ORDER BY AVG(salary) DESC
```



# 连接查询

## （sql192标准）

## 1.分类

### 	1.1按年代分类

​		sql192分类：只支持内连接
​		sql199标准：内连接 这个重点

​								外连接

​										左外连接 和右外连接

### 	1.2按功能分类：

​	内连接
​		等值连接
​		非等值连接
​		自连接
​	外连接
​		左外连接
​		右外连接
​		全连接
​	交叉连结

### 1.3等值连接的特点

​	多表的等值连接的结果为多表的交集部分
​	n表的连接，至少需要n-1个连接条件
​	多表的顺序没有要求
​	一般需要为表起别名
​	可以搭配所有的查询子句
*/

#等值连接 非等值连接 自连接
select name ,boyName from boys,beauty

两个表的联合查询 where后面要有有效的连接条件
select name ,boyName from boys,beauty where boys.id=beauty.boyfriend_id

## 2.等值连接

### 查询员工名。工种号，工种名  from 后面的顺序无关

```sql
select e.last_name,e.job_id,j.job_title
FROM employees e,jobs j
WHERE e.job_id=j.job_id
```



### 可以添加筛选

查询有奖金的员工的姓名和部门名

```sql
select last_name,department_name,e.commission_pct
FROM employees e,departments d
WHERE e.department_id=d.department_id AND e.commission_pct is NOT NULL
```



### 可以添加分组

查询有奖金的每个部门的部门名和部门的领导编号和该部门的最低工资

```sql
SELECT min(salary),department_name,d.manager_id
FROM employees e,departments d
WHERE d.department_id=e.department_id and commission_pct is not NULL
GROUP BY department_name,d.manager_id
```

每个部门的部门名和部门的领导编号和该部门的工资,递减排序

```sql
SELECT AVG(salary),department_id,job_id 
FROM employees
GROUP BY department_id,job_id 
HAVING AVG(salary)>10000 
ORDER BY AVG(salary) DESC
```



### 三表连接

员工名 部门名 所在地的城市

```sql
SELECT last_name,department_name,city
FROM employees e,departments d,locations l
WHERE e.department_id=d.department_id 
and d.location_id=l.location_id
and city like 's%' ORDER BY department_name DESC
```



## 3.非等值连接

#查询员工的

```sql
SELECT salary,grade_level
from employees e,job_grades g
where salary BETWEEN g.lowest_sal and g.highest_sal
```



## 4.自连接：约等于等值连接 不过是自己连接自己

## 5.sql199 标准



###   5.1 语法

select 查询列表 from 表名 别名 

【连接类型】 join 表2 别名 

on连接条件 

where  【筛选条件】 

group by  分组

 having 筛选条件 

order by  排序列表 

### 5.2 连接类型

内连接☆：inner

外连接

​	左外：left☆ 【out】

​	右外：right☆【out】

​	全外：full【out】

交叉连接  cross

### 5.3 内连接（等值，非等值，自连接）

#### 等值连接

#案例一 查询员工的名字 部门名

```mysql
select last_name,department_name
FROM employees e
INNER JOIN departments d
on e.department_id = d.department_id
```

#加条件查询名字中包含e的员工的姓名和工种名

```mysql
SELECT last_name,job_title
FROM employees e
INNER JOIN jobs j
on e.job_id = j.job_id
WHERE e.last_name LIKE '%a%'
```

#添加粉祝贺筛选
#查询部门个数大于3的城市名和部门个数

```mysql
SELECT city,count(*) 部门个数
FROM departments d
inner join locations l
WHERE d.location_id = l.location_id
GROUP BY city
having count(*)>=1
```

#添加排序
#查询部门个数大于3的城市名和部门个数降序排列

```mysql
SELECT city,count(*) 部门个数
FROM departments d
inner join locations l
WHERE d.location_id = l.location_id
GROUP BY city
having count(*)>=1
ORDER BY count(*) DESC
```

#三表连接
#查询员工名 部门名 工种名 并按部门名降序

```mysql
SELECT department_name,job_title,last_name
FROM employees e
INNER JOIN departments d on d.department_id = e.department_id
INNER JOIN jobs j on e.job_id = j.job_id
ORDER BY department_name desc
```

### 5.4自连接和非等值连接通上个标准

非等值连接

![image-20200316204705088](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200316204705088.png)

自连接

![image-20200316204833622](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200316204833622.png)

### 5.5外连接---左右连接

#### 特点:

外连接用于一个表中有另一个表中没有的记录
	1.外连接的查询结果为主表中的所有记录
		如果从表中有记录和他匹配，则显示匹配的值
		如果从表中没有和他匹配的，则显示null
		外连接的查询结果=内连接结果+主表中有而从表中没有的记录
	2.左外连接 left左边的表为主表
		右外连接 right 右边的是主表
	3.左外和右外交换两个表的顺序，可以实现同样的效果
	4.全外连接=内连接+表一有的表二没有的+表二有的表一没有的

#### 左连接

```sql
select b.name,bo.* 
from beauty b
LEFT OUTER JOIN boys bo
on b.boyfriend_id = bo.id
WHERE bo.id is not null
```

#### 全连接

mysql不支持

```sql
select b.*,bo.* 
from beauty b
FULL OUTER JOIN boys bo
on b.boyfriend_id = bo.id

```

#### 交叉连结  等同于笛卡尔积

```sql
select b.*,bo.* 
from beauty b
CROSS JOIN boys bo
```

# 子查询

## 1.定义

- 出现在其他语句内部的select语句，称为子
  查询或内查询
- 内部嵌套其他select语句的查询，称为外查询或主
  查询  

示例

```sql
select first_name from employees where
department_id in(
select department_id from departments
where location_id=1700
)
```



## 2.分类

​	select后面
​			仅支持标量子查询
​		from后面
​			支持表子查询
​		where或having后面：这个用的最多
​			标量子查询
​			列子查询
​			行子查询

​			exists后面的相关子查询

​			表子查询

案结果集的行列数的不同
	标量子查询（结果集只有一行一列
	列子查询（结果集只有一列多行
	行子查询（一行多列
	表子查询（多行多列

## 3.特点

   标量子查询 一半搭配着单行操作符使用
	![image-20200320182515137](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200320182515137.png)
	列子查询，一般搭配着多行操作符使用

![image-20200320183032217](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200320183032217.png)

## 4.各类查询的介绍

### where或者having后面

​		标量子查询示例

```sql
SELECT last_name
FROM employees
WHERE salary >
(SELECT salary
FROM employees
WHERE last_name = 'Abel')
```

列子查询

```sql
SELECT employee_id, last_name, job_id, salary
FROM employees
WHERE salary < ANY
(SELECT salary
FROM employees
WHERE job_id = 'IT_PROG')
AND job_id <> 'IT_PROG';
```

### select后面的

```sql
#查询每个部门的员工个数
SELECT d.*,(
SELECT COUNT(*)
from employees e
where e.department_id=d.department_id
) 个数
FROM departments d
```

![image-20200320183333445](C:\Users\Huo\AppData\Roaming\Typora\typora-user-images\image-20200320183333445.png)

### from后面的

用的比较少

### exists后面的

语法 exists（完整的查询语句）

结果只有1或者0

```sql
SELECT EXISTS(SELECT employee_id FROM employees where salary
=1000)
```



## 5.注意事项

- 子查询要包含在括号内。
-  将子查询放在比较条件的右侧。
-  单行操作符对应单行子查询，多行操作符对应
  多行子查询。  
- 子查询 (内查询) 在主查询之前一次执行完成。
- 子查询的结果被主查询(外查询)使用 。 
- 非法使用子查询报错，例如多行子查询使用单行比较符

```sql
SELECT employee_id, last_name
FROM employees
WHERE salary =
(SELECT MIN(salary)
FROM employees
GROUP BY department_id);
```

- 子查询空值时子查询不会返回任何行

# 分页查询

## 1.应用场景

当要显示的数据，一页显示不全，需要分页提交sql请求

## 2.语法

```sql
from表
	连接类型
	on
	where
	groudby
	haing
	ORDER BY
	limit offset，size
```

## 3.注意事项

offset要显示的条目的起始索引（起始索引从零开始
size要显示的条目个数

	特点
		limit放在查询语句的最后
		公式
			要显示的页数 page，每页显示的条目数size
			
			select 查询列表
			from 表
			limit （page-1）*size ，size
4.举例

```sql
select * from employees limit 0,5
```

# 联合查询

## 1.概念

union 联合  合并：将多条查询语句的结果合并成一个结果

## 2.语法

```sql
查询语句1
UNION
查询语句2
UNION
。。。
```

## 3.应用场景

要查询的结果来自于多个表，且夺标之间没有直接的连接关系，但查询的信息一致时

## 4.特点及要求

- 要求多条查询语句的查询列数要一致

- 要求多条查询语句的的查询的每一列的类型和顺序最好一致	

- union关键字默认去重，如果使用union all 可以包含重复项

  ```sql
  select * from employees where email like '%a%' or department_id>90;
  对应的联合查询
  select * from employees where email like '%a%'
  UNION
  select * from employees where department_id>90
  ```

  





















































































