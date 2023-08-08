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

      
