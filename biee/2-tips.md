1.BIEE打补丁不能锁定产品目录：
部分电脑在打补丁失败的时候请使用管理员权限来运行CMD，获得对存贮在C盘的oracle目录来读写。使补丁顺利安装。

2.物理层别名的使用：
BIEE RPD模型建立，物理表请使用别名的方式来灵活的运用。通过加入物理表然后配置外键，保存。来方便在逻辑层中建立关联。

3.时间维度创建：
维度的建立应该是有底层向上来建立的，逆序建立会出错。时间维度的建立和其他的维度的不同，要勾选维度为时间类型，设置好时序关键字。

4.迁移平台时候：
使用catalog归档和取消归档来迁移BIEE中的报表和仪表盘，有权限的要保留权限。

5.设置仪表盘提示为真可以达到仪表盘内JS可以每次都刷新：
仪表盘可以使用页面提示来来获得整个页面的同步刷新。在提示中可以设定表示变量来传递提示器所选定的参数。

6.catalog/system/mtkgcache/sawguidstate问题，导致BIEE崩溃不能启动：
新建一个catalog然后将sawguidstate和sawguidstate.atr替换后重启BIEE后正常

7.在日志中查询物理语句：
从管理-管理会话-对应的日志中看到所要的SQL。(要开启足够高的日志等级)

8.BIEE清楚缓存： 
在BI管理中(RPD工具)：管理-管理会话-关闭所有游标
EVALUATE_SUPPORT_LEVEL 这个要在NQSConfig.INI 中修改并重启后才能使用EVALUATE()函数.
在管理-权限中有对直连数据库的权限设置，根据适应的范围调整，基本上选择认证用户即可使用。

10.BIEE启动失败的时候，检查RCU用户在数据库是不是过期了：
BIEE的错误是ora-28000的时候，查看BIEE 用户是否过期了select * from dba_users where username in ('DEV_MDS','DEV_BIPLATFORM'); 解锁，激活用户alter user dev_mds identified by 原来密码 account unlock;用户密码生命周期由默认变成无限制alter profile default limit PASSWORD_LIFE_TIME unlimited;

11.RPD编辑：
RPD是可以用复制黏贴来构建的。物理称，逻辑层，表示层，可以黏贴出来用文本来改的。

12.日期触发：
BI医院产品中数据库的日期格式触发器要注意大写问题。

13.单表不需要和其他维度关联的时候：
当导入RPD中只有一个表没有关联表的时候，可以做两个别名来自身关联自己通过检测.

14.
BIEE11.9中RPD中一些字符集导致列不能兼容主题的错误。前端错误提示：
![](image/1.png)
查询日志文件instances\instance1\diagnostics\logs\OracleBIServerComponent\coreapplication_obis1下的nqserver.log验证错误
instances\instance2\config\OracleBIServerComponent\coreapplication_obis1下的NQSConfig.INI来解决
```
Localization/Internationalization parameters.
LOCALE = "english-usa"; 
SORT_ORDER_LOCALE = "english-usa"; 
SORT_TYPE = "binary"; 
```
的english-usa修改为Chinese-simplified   