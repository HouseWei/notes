## NodeJS

### 一、后端的规范与思想

#### 1、分层

1. Web层（接受和发送Http请求的，封装；web层/controller层）

2. 业务逻辑层（服务层，XXXService）

   LoginController（接收参数，判断是否非法，传给服务层）

   LoginService（获取这个用户的密码，进行比较）

3. DAO层（data access object）：

   DataBase（DB）：存数据

   业务： 对 对象进行操作

   如果要存储： 对象 转为 数据

   如果要读取： 数据 转为 对象

4. 持久层： 存在磁盘上

   文件，数据库

   

   每层的命名：

   web层：LoginController（接收参数，判断是否非法，传给服务层）

   服务层：LoginService（获取这个用户的密码，进行比较）

   DAO层：LoginDAO（从数据库获取数据，并转换为对象）

   Domain：User