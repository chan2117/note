------

**命令行式管理**

------

前面我们创建的最简单的flask应用，在IDE中直接点击运行PY文件跑起来去浏览器访问的。实际的应用不能这样，应该有个命令行来控制。

请出flask众多扩展中的： [flask-script](http://flask-script.readthedocs.io/en/latest/)
1. 安装
    ```
    pip install flask-script
    ```

2.  官方的示例
    ```
    from flask_script import Manager

    from myapp import app # 你的flask app

    manager = Manager(app)

    @manager.command
    def hello():
        print "hello"

    if __name__ == "__main__":
        manager.run()
    ```

3. 项目中的应用