# 查询基础

# 1.相关的基础语句和属性

#### 选择数据库

USE myemployees;

#### 查询所有

select * from employees;

#### 查询常量/字符串

SELECT 100;
SELECT 'john';

#### 查询函数

SELECT VERSION();

#### 起别名

SELECT last_name AS 姓,first_name as 名 FROM
employees;
-- 其中as可以用空格代替，起的别名有关键词时用单引号

#### 去重关键字DISTINCT 

案例查询所有员工标号
SELECT department_id FROM employees;#查询结果有重复值

SELECT DISTINCT department_id FROM employees;#加上distict

####  +号的作用，并显示为姓名 作用：

#案例 查询员工名和姓连接成一个字段
SELECT CONCAT('a','b','c') AS 结果;#字符连接函数，将两个字段的值连接在一起

SELECT CONCAT( last_name,first_name) AS 姓名 FROM employees;

#### 显示表的结构

DESC departments;

#### 条件查询即where查询

USE myemployees;
SELECT
employees.first_name
FROM
employees
WHERE
employees.salary> 5000

#### 模糊查询

like 一般和通配符一起使用：'%x%'，
													%表示任意多个字符，包括零个字符
													_xiahuaxian biaoshidangezifu 
													若使用了关键字可以用哪个转义字符‘\’
between and
注意事项；包含临界值
					可以提高整洁度
					临界值有顺序

LIKe的使用
SELECT * FROM employees where last_name  LIKE '%a%';

SELECT * FROM employees where last_name  LIKE '__n_%';
#查询员工中第二个字符为下划线的的字符
SELECT * FROM employees where last_name  LIKE '_\_%';

####  BETWEEN and的使用

 SELECT * FROM employees where employee_id between
 100 AND 120 ;

####  关键字in的使用

使用in提高语句的简洁度，in列表值得类型必须一致兼容

--  示例查询员工的公众编号是IT_PROGE,AD_VP,AD_PRES
SELECT last_name,job_id FROM employees WHERE job_id in('IT_PROGE','AD_VP','AD_PRES');

#### is null | is not null的使用

is null
-- 示例查询没有奖金的员工和奖金

```sql
SELECT last_name,commission_pct FROM employees WHERE commission_pct is NULL;
SELECT last_name,commission_pct FROM employees WHERE commission_pct is not
 NULL;
```

#下面这种方式报错

#下面这种方式报错

```sql
ISNULL(commission_pct,0),
employees.commission_pct
FROM
employees
```

#### 一些小的例子

查询员工号为176的员工的姓名和部门号和年薪
SELECT
employees.first_name,
employees.salary*12 AS 年薪,
employees.department_id
FROM
employees
WHERE
employees.employee_id = 176;

查询没有奖金，且工资小于18000的salary，last_name
SELECT salary,last_name FROM employees WHERE salary<18000 AND commission_pct is NULL;

SELECT
employees.employee_id,
employees.first_name,
employees.last_name,
employees.email,
employees.phone_number,
employees.job_id,
employees.salary,
employees.commission_pct,
employees.manager_id,
employees.department_id,
employees.hiredate
FROM
employees
WHERE
employees.job_id <> 'IT' OR
employees.salary = 12000;

DESC departments;

# 2.排序查询

### 概念

排序查询 关键词为 order by coumlum (ASC|DESC) 

默认为ASC 升序递减。默认递增

ORDER BY 子句中可以支持单个字段，多个字段，表达式，函数，别名
	一般放在查询语句的最后面除了limit语句

### 示例

```
use myemployees;
SELECT * FROM employees;
```

具体示例如下

```
SELECT * FROM employees ORDER BY salary DESC;
```

示例2 查询部门编号大于90的员工信息，按入职时间的先后进行
SELECT * FROM employees 
WHERE department_id>=90
ORDER BY hiredate;

案例三 按表达式排序 按年薪的高低显示员工信息和年薪

别名年薪也可以放在 ORDER BY 后面

```sql
SELECT *,salary*12*(1+IFNULL(commission_pct,0)) 年薪 FROM employees 
ORDER BY salary*12*(1+IFNULL(commission_pct,0));
```

可以这样写上面这句话

```
SELECT *,salary*12*(1+IFNULL(commission_pct,0)) 年薪 FROM employees 
ORDER BY 年薪;
```

案例四 按函数排名，示例按自己长度排名

```
SELECT LENGTH(last_name) 字节长度,last_name,salary from
employees
ORDER BY LENGTH(last_name) DESC;
```

案例五 多条件排序  示例 查员工信息  先按工资升序 然后按 员工编号降序
左到有，优先级高到底。

```
select * FROM employees
ORDER BY salary ASC,employee_id DESC;
```

# 3.常见函数

类似于java的方法，将一组逻辑语句封装在方法体中。
调用：SELECT 函数名（实参） （from 表）

函数可以嵌套。

## 分类

单行和分组（即 聚函数，统计函数）函数

### 一、字符函数

1.LENGTH(str); 判断字符的字节数个数。

2.CONCAT(str1,str2,...) 字符号连接函数

3.UPPER(str)和lower 转换大小写。 

4.SUBSTR(str FROM pos FOR len) 对某个字段从某个索引开始截取多长(索引从1开始，并长度为可选项);
  SUBSTRING(str FROM pos FOR len) 
	
5.INSTR(str,substr) 表示substr的首字母在str中的位置 前者必须是后者的子集 否则返回零。

6.TRIM([remstr FROM] str) 默认去掉字符串前后的空格，方括号内的前者可规定要去掉的字符

7.LPAD(str,len,padstr) 和 RPAD(str,len,padstr) 用指定的字符实现左右填充到制定的长度。

8.REPLACE(str,from_str,to_str) 第一个参数为操作数，第二个为需要替换的字符，第三个拿来替换的字符
*/

#### 各字符函数案例

##### CONCAT

案例：姓名中首字符大写，其他字符小写，其他字符小写然后用_拼接显示起来

SELECT CONCAT(LOWER(SUBSTR(first_name FROM 1 FOR 1)),'_',SUBSTR(first_name FROM 2)) 姓名 FROM employees;

##### #INSTR(str,substr)案例

SELECT INSTR('123456789','57') 输出; 

##### #TRIM 示例

SELECT LENGTH(trim('   1234   ')) 输出;
SELECT TRIM('a' FROM 'a123a') 输出;

##### #rpad

SELECT RPAD('123',6,'#') 输出;

##### REPLACE(str,from_str,to_str)
SELECT REPLACE('12223','2','1') 输出;

### 二、数学函数

##### round 四舍五入

select round(-1.5);

##### #CEIL(X）向上取整，返回》=改参数的最大整数

##### #FLOOR(X) 向下取整，返回小于改参数的最大整数

##### #TRUNCATE(X,D) 截断 后面的参数是几就留几个小数，其他不要

SELECT TRUNCATE(1.4214,1);

##### #mod取余

##### #日期函数

#NOW() 返回日期时间+时间

##### #curdate 返回当前系统的日期，不包含时间

USE myemployees;

##### 可以获取指定的部分的年月日，时分秒

SELECT YEAR(NOW()) 年;
 SELECT YEAR('1995-5-5') 年;
 SELECT YEAR(hiredate) 年 FROM employees;

#### 将日期格式转换成指定格式

SELECT STR_TO_DATE('1993-2-2','%Y-%m-%d');

####  将日期准换位成字符

 SELECT DATE_FORMAT('1993-2-2','%Y年%m月%d日');

 #使用 查询日期为1992-4-3的员工信息
 SELECT * FROM employees WHERE hiredate='1992-4-3';

 SELECT * FROM employees WHERE hiredate=STR_TO_DATE('1992.4.3','%Y-%m-%d');

 #查询you奖金的员工的名字和入职日期（xx月/xx日/ xx年）

  SELECT last_name,DATE_FORMAT(hiredate,'%m月/%d/日 %y年') FROM employees WHERE commission_pct IS NOT NULL;

###  三、其他函数

 SELECT VERSION();
 SELECT DATABASE();
 SELECT USER();

### 四、流程控制函数
#### if函数

```sql
SELECT IF(10>5,'da','xiao');

SELECT IF(expr1,expr2,expr3)
SELECT last_name,commission_pct,IF(commission_pct IS NULL,'hehe','haha') 备注 FROM employees;
```



####  #使用一类似于switch

```sql
 CASE case_value
	WHEN when_value THEN
		statement_list
	ELSE
		statement_list
	END CASE;
```

#案例，查询部门号为30,40,50的员工的工资，分别为  1.1倍1.2,1.3,其他正常显示

```sql
SELECT salary 原始工资,department_id,
CASE department_id
	WHEN 30 THEN salary*1.1
	WHEN 40 THEN salary*1.2
	WHEN 50 THEN salary*1.3
	ELSE salary END AS 新工资 FROM employees; 
```



#### #使用二，类似于多重if的使用，与上面一的区别为没有case_value

 

```sql
CASE 
 WHEN when_value THEN statement_list
 WHEN when_value THEN statement_list
 WHEN when_value THEN statement_list
	ELSE statement_list
END CASE;
```

#案例

```sql
select last_name,salary,CASE 
	WHEN salary>20000 THEN
		'A'
		WHEN salary>15000 THEN
		'b'
		WHEN salary>10000 THEN
		'c'
	ELSE
		'd'
END FROM employees;
```


