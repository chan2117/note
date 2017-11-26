-----------
start的章节中，制作了一个Hello Webpack的小应用。但是webpack的功能不仅仅这些。webpack除了能动态的绑定左右的依赖关系之外，还有不少很酷的亮点，例如：将页面所需要的其他的文件打包。

-----------
首先，修改一下
dist/index.html
```
  <html>
    <head>
-    <title>Getting Started</title>
+    <title>Asset Management</title>
    </head>
    <body>
      <script src="./bundle.js"></script>
    </body>
  </html>
```

* css loader

    要把CSS文件打包进JS中，需要先安装两个包css-loader和style-loader
    ```
    npm install --save-dev style-loader css-loader
    ```
    在配置文件中配置loader
    webpack.config.js
    ```
      const path = require('path');

      module.exports = {
        entry: './src/index.js',
        output: {
          filename: 'bundle.js',
          path: path.resolve(__dirname, 'dist')
        },
    +   module: {
    +     rules: [
    +       {
    +         test: /\.css$/,
    +         use: [
    +           'style-loader',
    +           'css-loader'
    +         ]
    +       }
    +     ]
    +      }
      };
    ```
    接下来，创建一个.css文件style.css，并在应用中引用。
    ```
    webpack-demo
    |- package.json
    |- webpack.config.js
    |- /dist
      |- bundle.js
      |- index.html
    |- /src
  + |- style.css
      |- index.js
    |- /node_modules
    ```
    src/style.css
    ```
    .hello {
        color: red;
    }
    ```
    src/index.js
    ```
    import _ from 'lodash';
    + import './style.css';

    function component() {
        var element = document.createElement('div');

    // Lodash, now imported by this script
        element.innerHTML = _.join(['Hello', 'webpack'], ' ');
    +   element.classList.add('hello');

        return element;
    }

    document.body.appendChild(component());
    ```

    cmd运行在start章节中写好的命令npm run build,等待输出成功,浏览器中打开dist/index.html,如果看到hello webpack 变成了红色，说明css文件打包成功。

---------
* loading images
    
    想将web使用的图片打包起来，也是可以的，我们只需要引入file-loader来帮助就好了。
    老样子
    ```
    npm install --save-dev file-loader
    ```
    修改一下文件：
    webpack.config.js
    ```
    const path = require('path');
  
    module.exports = {
      entry: './src/index.js',
      output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
      },
      module: {
        rules: [
          {
            test: /\.css$/,
            use: [
              'style-loader',
              'css-loader'
            ]
          },
  +       {
  +         test: /\.(png|svg|jpg|gif)$/,
  +         use: [
  +           'file-loader'
  +         ]
  +       }
        ]
      }
    };
    ```
    随便选择一个png图片文件放在src目录下并命名为icon.png(其他的类型的图片也可以，注意文件后缀名称。选择范围是你在webpack.config.js中file-loader的test中声明的格式。)
    ```
    webpack-demo
    |- package.json
    |- webpack.config.js
    |- /dist
      |- bundle.js
      |- index.html
    |- /src
  + |- icon.png
      |- style.css
      |- index.js
    |- /node_modules
    ```
    src/index.js
    ```
      import _ from 'lodash';
      import './style.css';
    + import Icon from './icon.png';

      function component() {
        var element = document.createElement('div');

        // Lodash, now imported by this script
        element.innerHTML = _.join(['Hello', 'webpack'], ' ');
        element.classList.add('hello');

    +   // Add the image to our existing div.
    +   var myIcon = new Image();
    +   myIcon.src = Icon;
    +
    +   element.appendChild(myIcon);

        return element;
      }

      document.body.appendChild(component());
    ```
    src/style.css
    ```
    .hello {
        color: red;
    +   background: url('./icon.png');
    }
    ```
     cmd运行在命令npm run build,浏览器中打开dist/index.html就可以看到你选择的背景图片了。同时在dist中出现一个名字类似与5c999da72346a995e7e2718865d019c8.png的图片。这意味着webpack在src文件夹中找到我们的文件并处理它！
----------

webpack的loader还有很多种，这里不再赘述，使用的方式大致是相同的。
更多loader的教程参照
>[webpack-guides:asset-management](https://webpack.js.org/guides/asset-management/)