学习安装oracle数据库
1.安装时候不要使用安装数据库软件并且配置数据库， 这样得到是的数据库字符集与后面的BIEE RCU等不同，导致不能配置。
2.监听可以配置很重要
3.数据库手动添加实例，字符集通常为UTF-8,如果要使用企业管理器请勾选，否则没有企业管理进程（既console）。
4.将oracle的服务设置为手动来是电脑日常运行顺畅
5.基本上只要打开Listener 和 对应的数据库实例（如：OracleServiceORCL）就能够正常的使用oracle数据库了。
 
学习安装BIEE 11.7
1.一般使用简单的BIEE安装，企业版和简易安装的区别在于负载均衡的实现。
2.部分电脑在打补丁失败的时候请使用管理员权限来运行CMD，获得对存贮在C盘的oracle目录来读写。使补丁顺利安装。
3.BIEE RPD模型建立，物理表请使用别名的方式来灵活的运用。通过加入物理表然后配置外键，保存。来方便在逻辑层中建立关联。
4.维度的建立应该是有底层向上来建立的，逆序建立会出错。时间维度的建立和其他的维度的不同，要勾选维度为时间类型，设置好时序关键字。
5.使用catalog归档和取消归档来迁移BIEE中的报表和仪表盘，有权限的要保留权限。
6.仪表盘可以使用页面提示来来获得整个页面的同步刷新。在提示中可以设定表示变量来传递提示器所选定的参数。
7.回写的学习和使用，详细参考超哥的博客。要在RPD中打开字段的回写并取消这个表的高速缓存，在instances中部署好analyticsRes中放好回写模版，BIEE中打开对字段的回写属性和指定回写模版的XML（保存在analyticsRes下的customMessages），配置config下的lightwriteback，并且将analyticsRes在console中部署好，最后在权限管理中赋予当前用户权限，重启可用。
8.BIEE的RPD迁移后，要把变量中的一些静态变量做修改：例如IP
9.smartview的链接是http://localhost:7001/analytics/jbips
10../instances/instance1/config/OracleBIPresentationServicesComponent/coreapplication_obips1/instanceconfig.xml路径下 修改登录语言 直接在<ServerInstance>中添加<Localization><AllowedLanguages>en,zh-CN</AllowedLanguages> </Localization>
11.主页修改在JS/CSS文件中的HOME文件夹中的bieehome.js文件修改即可。
12.菜单栏的修改在JS/CSS文件中的header.js文件中修改即可，不需要重启，清楚浏览器缓存刷新即可。