使用BIEE的时候，有很多的ORACLE的标识，在项目实施或者自己使用的时候不是很友好，所以做一些样式上的调整和个性化。

* 1.在替换了BI页面的标题和图标后要更改抬头的颜色和平台名称需要去修改master.css和commo.css：
```
标题和图标间距：
common.css . HeaderBrandName :left 55PX 
抬头颜色：
第一层   master.css.MasterBrandingArea:background-color
第二层   master.css.MasterGlobalLayer:background-color
        master.css.MasterGlobalLayer:border
        master.css.masterPrimaryLayer：background - color
        master.css.masterPrimaryLayer：border 
```
* 2. 在登陆框左边添加图片：
在login.css中更改class名为boxcontent的格式，如下
```
.boxcontent{
padding:45px 55px 45px 319px; 
width:225px;
text-align:left;
font-size:8pt;
background-image:url(/analytics/res-RQJ7n89ACsw/s_Skyros/master/login_bg2.png);
background-repeat:no-repeat;
box-shadow:10px 10px 5px #888888;
border:1px solid #EEEEEE;
margin:0 auto;
border-radius:3px;
position:relative;}
```
> 注释：
    1. Padding 319px 可按照实际情况调整，319px=登陆框本身所需left-padding 55px + 图片的宽度；
    2. 需将图片放入指定文件夹。

* 3.将仪表盘过滤器的应用文字改成查询：
viewmessages.XML中的<WebMessage name="kmsgEVCPromptApply"><HTML>查询</HTML></WebMessage>将仪表盘的应用改成查询。
(viewmessages的路径..\Oracle_BI1\bifoundation\web\msgdb\l_zh-CN\)

* 4.取消饼图在没有数据的时候的显示'刷新'两个字：
viewmessages.XML  中的<WebMessage name="kmsgEVCLinkRefresh"> '刷新'替换为空格。

* 5.OBIEE11g中如何通过修改配置文件修改版权信息 utilmessages.xml

* 6.OBIEE11g中如何通过修改网页标签页 productmessages.xml 文件下的<WebMessage name="kmsgProductPortal">

* 7.登录窗口语言种类：
./instances/instance1/config/OracleBIPresentationServicesComponent/coreapplication_obips1/instanceconfig.xml路径下，修改登录语言，直接在<ServerInstance>中添加<Localization><AllowedLanguages>en,zh-CN</AllowedLanguages> </Localization>

* 8.新增下拉菜单栏：
step1:覆盖domains目录下的临时文件。
<OBIEE_HOME>\user_projects\domains\bifoundation_domain\servers\AdminServer\tmp\_WL_user\analytics_11.1.1\silp1v\war\res\b_mozilla
拷贝原有的k.push()函数进行修改，增加自定义的链接。
拷贝原有的saw.header.NavBar.prototype.onDisplayzhangcMenu=function(c,b)做出相应的修改，为链接增加下拉菜单。
step2:修改<OBIEE_HOME>\Oracle_BI1\bifoundation\web\msgdb\common下的saw.headerXML配置文件，为新增的链接和下拉菜单增加ID。
step3:修改<OBIEE_HOME>\Oracle_BI1\bifoundation\web\msgdb\l_zh-CN\messages\uicmsgs下的saw.headerXML配置文件，为新增的链接和下拉菜单增加中文名用于显示。


* 9.启用HTML5渲染图形：
编辑<OBIEE_HOME>\instances\instance2\config\OracleBIPresentationServicesComponent\coreapplication_obips1 下的instanceconfig.xml，在<\views>中增加

```
<Charts>
    <DefaultWebImageType>html5</DefaultWebImageType>
</Charts>
```
重启服务后即可启用HTML5渲染图形。

* 10.平台LOGO图片替换：
<OBIEE_HOME>\user_projects\domains\bifoundation_domain\servers\AdminServer\tmp\_WL_user\analytics_11.1.1\silp1v\war\res\s_Skyros\master下的
oracle_logo.png
toolbarseparatordarktheme.png
等文件进行客户化。
备注：
修改BrandName 的 CSS 以适应LOGO：
在更改LOGO图片后，先在浏览器中将文字的浮动调整到合适，再去
<OBIEE_HOME>\user_projects\domains\bifoundation_domain\servers\AdminServer\tmp\_WL_user\analytics_11.1.1\silp1v\war\res\s_Skyros\b_mozilla_4 目录下的common.css中查找.HeaderBrandName修改Class。
登录界面由于需要修改HTML文件，不利于客户化，因此采用在CSS中使用!improtant强制覆盖CSS实现。
修改<OBIEE_HOME>\user_projects\domains\bifoundation_domain\servers\AdminServer\tmp\_WL_user\analytics_11.1.1\silp1v\war\res\sk_Skyros\login 下的 login.css，给.appname 这个class增加修改后的偏移。
```
    top: 8px !important;
    left: 30px !important;
```

* 11.客户化、图片、CSS路径：
<OBIEE_HOME>\user_projects\domains\bifoundation_domain\servers\AdminServer\tmp\_WL_user\analytics_11.1.1\silp1v\war\res
可以存放一些个性化的图标放在这个文件夹下面然后在BIEE的平台中使用。

* 12.URL地址替换
更换fmw-welcome,删除原有应用重新部署。 OBIEE\ oracle_common\ modules\ oracle. jrf_11. 1. 1\ fmw-welcome. ear。就可以不使用7001:/analytics来访问了。

* 13.无数据字符替换
BIEE11\Oracle_BI1\bifoundation\web\msgdb\l_zh-CN\viewmessages.XML中的<WebMessage name="kmsgEVCNoRowsFilters"> 替换为'你选择的条件没有生成任何数据'。


