# 第一章 架构与历史

查询表的相关信息

~~~powershell
show table status like 'order_detail' \G;
*************************** 1. row ***************************
           Name: order_detail  表名
         Engine: InnoDB 引擎类型
        Version: 10 
     Row_format: Dynamic  行的格式
           Rows: 2 表中行数
 Avg_row_length: 8192 平均每行包含的字节数
    Data_length: 16384 表数据大小
Max_data_length: 0 表数据最大容量 和存储引擎相关
   Index_length: 16384  索引大小
      Data_free: 0 表示已分配但目前没有使用的空间。这部分空间包括之前删除的行和后续被insert利用到的空间
 Auto_increment: NULL 下一个自增的值
    Create_time: 2020-04-19 12:47:46 表的创建时间
    Update_time: NULL 更新时间
     Check_time: NULL 最后一次检查表的时间
      Collation: utf8mb4_general_ci 默认的字符集合字符排序规则
       Checksum: NULL 启用表示整个表的实时校验和
 Create_options: 创建表时的指定的其它选项
        Comment: 订单详情表 表的额外信息

~~~

