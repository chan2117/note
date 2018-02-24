----

**文件目录的情况**

----
项目文件的分布结构主要有两个模式:功能式和分区式。

1. 功能式

    功能式架构就用代码在应用中作用来区分。例如：所有模板放到同一个文件夹中，静态文件放在另一个文件夹中，而视图放在第三个文件夹中。
    ```
    yourapp/
        __init__.py
        static/
        templates/
            home/
            control_panel/
            admin/
        views/
            __init__.py
            home.py
            control_panel.py
            admin.py
        models.py
    ```
    这样，一个文件夹包含所有该功能的所有文件，应用内的各种小的页面或者应用就不再区分。
2. 分区式
    和功能式的区分就是，文件的划分是以代码的应用独立性来划分的。在一个文件夹，包含着自己这个子应用的模版、静态文件、视图等文件。例如：网站的业务操作模块的所有模版、静态文件、视图等在一起，而后台管理的所有文件夹在另一个文件夹中。
    ```
    yourapp/
        __init__.py
        admin/
            __init__.py
            views.py
            static/
            templates/
        home/
            __init__.py
            views.py
            static/
            templates/
        control_panel/
            __init__.py
            views.py
            static/
            templates/
        models.py
    ```

文件结构的不同，是存放的逻辑不同。对于应用本身不会有很大的影响，主要取决于应用中的各个模块之间的联系是否紧密，管理的逻辑是否更贴合实际，更加便利。当应用内模块联系精密，功能式架构的可能更合适一些。如果每个模块之间的独立性很强，仅仅共享少许的模型和配置文件，那么分区式是更好的选择。