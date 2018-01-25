1.创建数据库认证登录表
```
create table USERS(U_NAME varchar2(100),U_PASSWORD varchar2(100),U_DESCRIPTION varchar2(100));
create table GROUPS(G_NAME varchar2(100),G_DESCRIPTION varchar2(100));
create table GROUPMEMBERS(G_NAME varchar2(100),G_MEMBER varchar2(100));
```
2.对groups表数据填充 一般为三个
```
insert into groups(g_name) values('BIAdministrators');
insert into groups(g_name) values('BIAuthors');
insert into groups(g_name) values('BIConsumers');
```
 
3.创建视图
```
CREATE OR REPLACE VIEW users_vw AS SELECT U_NAME, U_PASSWORD, RPAD(U_NAME, 16, '0') AS GUID ,U_ENABLE FROM users where U_ENABLE = 'Y';
```
 
4.数据源设置 console  
1)点击锁定和编辑-选择左边从菜单的 服务- 选择服务中的 数据源-点击 新建-选择 一般数据源  
2)JDBCNAME:UserGroupDS ;JNDINAME: jdbc/UserGroupDS ;DATEBASE TYPE:oracle  
3)驱动选择：Oracle's Driver (Thin) for Service Connections; Releases:9.0.1 and later  
4)创建JDBC连接 填写连接数据库信息 点击测试连接，测试成功后下一步。  
5)选中Adminserver服务器部署-点击完成-点击左上角的激活应用
 
5.新建用户验证方式 console  
1)点击锁定和编辑-选择左边从菜单的 安全领域-点击 myrealm- 选择 提供程序 -在 验证中 点击新建  来创建新的验证方式  
2)验证方式：NAME:UserGroupDBAuthenticator ; TYPE:SQLAuthenticator;  
3)点击新建的验证方式，选中 配置- 选择 提供程序特定，填写连接资料。DaraSourceName:UserGroupDS;  
4)回到 提供程序-点击默认验证名字 DefaultAuthenticator -选择 配置 -选择 公用 -将空置标记改为 SUFFICIENT  
5)回到 提供程序 -选择 重新排序- 将 UserGroupDBAuthenticator 验证放到第一个  
6)激活所有更改，然后在EM重启整个BI平台（AdminServer）
 
6.设定用户在AdminServer的两个适配器  
1)拷贝两个XML去<BIEE_HOME>/oracle_common/modules/oracle.ovd_11.1.1/templates/
(存在3-adapter_template_usergroup1.xml,3-adapter_template_usergroup2.xml)  
2)cmd进入到<BIEE_HOME>/oracle_common/bin  
3)设定环境变量  
    ```
    SET  ORACLE_HOME=<BIEE_HOME>/Oracle_BI1;SET WL_HOME=<BIEE_HOME>/wlserver_10.3/
    ```
      
4)运行脚本，红色部分要更改，执行后要输入密码  
    ```
    libovdadapterconfig -adapterName userGroupAdapter1 -adapterTemplate adapter_template_usergroup1.xml -host 192.168.200.117 -port 7001 -userName weblogic -domainPath D:\app\obiee\user_projects\domains\bifoundation_domain\ -dataStore DB -root cn=users,dc=oracle,dc=com -contextName default -dataSourceJNDIName jdbc/UserGroupDS
    ```
    ```
    libovdadapterconfig -adapterName userGroupAdapter2 -adapterTemplate adapter_template_usergroup2.xml -host 172.16.191.103 -port 7001 -userName weblogic -domainPath E:\app\obiee\user_projects\domains\bifoundation_domain\ -dataStore DB -root cn=users,dc=oracle,dc=com -contextName default -dataSourceJNDIName jdbc/UserGroupDS
    ```  
5)重启BI
 
7.配置用户级别映射  EM  
1)选中 weblogic域-  选中 bifoundation_domain  - 在右边框体左上角 下拉选 安全性：安全提供方配置  
2)打开折叠 身份存储提供放-点击 配置- 跳转后点击 添加- 属性名:virtualize 值:true  
3)重启