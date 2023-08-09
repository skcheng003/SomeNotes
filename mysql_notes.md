## Learning mysql

1.   mysql 有服务器程序和客户端程序

2.   Linux下启动和登录mysql

     ```bash
     service mysql start
     service mysql status
     service mysql stop
     mysql -u cheng -p
     ```

3.   mysql默认监听3306端口

4.   mysql8.0 删除查询缓存

5.   mysql server负责：连接管理、查询缓存、语法解析、查询优化

6.   存储引擎：负责数据的存储和提取，向上对mysql server提供统一的api

7.   设置启动选项

     ```bash
     mysqld --default-storage-engine=MyISAM
     ```

8.   -v 和 --version

9.   查看mysql系统环境变量

     ```sql
     show variables like 'default%'
     show variables like 'max_connections'
     ```

10.   系统变量区分Global和Session，方便多个用户同时设置不同环境变量（不设置 GLOBAL | SESSION 的话默认设置SESSION），客户端连接进来后，mysql为每个客户端连接维护一组session环境变量

      ```sql
      set session default_storage_engine = MyISAM;
      set global max_connections = 200;
      ```

11.   状态变量，由服务器自动生成，显示服务器程序运行状况，区分GLOBAL和SESSION两个作用范围

      ```sql
      show status like 'Threads_connected'
      ```

12.   InnoDB中页的默认大小是16KB，是管理存储空间的基本单位

13.   InnoDB 四种存储格式：Compact，Redundant，Dynamic，Compressed

14.   Compact 格式：变长字段长度列表（逆序） + NULL值列表（逆序） + 记录头信息（40bits） +  column1 val, column2 val, ...

15.   行溢出：原纪录处只会保留一部分数据，然后用20个字节存储溢出页的地址和字节数，溢出页用链表连接起来

16.   Dynamic 格式：和Compact类似，不同点在于，溢出时会把所有字节存储在其他页面

17.   Record Header：

      + delete_mask：是否被删除
      + min_rec_mask：B+树的每层非叶子结点中的最小记录
      + n_owned
      + heap_no：当前record在当前page中的位置，比较主键（两条伪纪录：最小record：Infimum，最大record：Supremum，heap_no is 0 and 1, respectively ）
      + record_type：record type，普通记录0，B+树非叶节点纪录1，最小纪录2，最大纪录3
      + next_record：当前record data到下一条record data的offset，one way linked list，Infimum record -> user record(primary key smallest) -> ... -> user record(primary key biggest) -> Supermum record
      + next_record 数据的变化可以实现删除操作，InnoDB引擎负责维护单链表
      + next_record 指针的位置，向左读是record header，向右读是record data
      + next_record 也可以把已删除的record链接成垃圾链表













