## 1.初始化项目
### 1.1 初始化项目
```
npm init -y
npm install webpack webpack-dev-server --save-dev
```
### 1.2创建webpack配置文件  webpack.config.js
```
module.exports = {
 entry:'./app/index.js',//指定入口文件
 output:{
     path:'./build',//指定打包后的文件存放目录
     filename:'bundle.js'//指定打包后的文件名
 }
}
```
### 1.3创建脚本
```
  "scripts": {
+    "build": "webpack",
+    "dev":"webpack-dev-server"
  },
```
### 1.4 打包文件
```
npm run build
```
### 1.5 启动开发服务器
```
npm run dev
```

## 2.支持es6
### 2.1安装依赖包
```
npm install babel-core babel-loader babel-preset-es2015 --save-dev
```

### 2.2 修改webpack.config.js
```
module:{
        loaders:[
            {
                test:/\.js$/,
                loader:'babel'
            }
        ]

    }
```

### 2.3 配置 .babelrc
```
    {
      "presets":["es2015"]
    }
```
## 3.webpack-dev-server
当运行`npm run dev`的时候，会先进行打包，打包到build目录下。
会启动一个express的http服务器，以build目录作为静态文件根目录 html-webpack-plugin 用来读取app目录下的index.html文件，然后向里面插入打包生成后的bundle.js文件，再保存到build目录 open-browser-webpack-plugin 当打包完成后，服务器启动成功后，自动打开浏览器运行我们的项目
### 3.1 安装
```
npm install html-webpack-plugin open-browser-webpack-plugin --save-dev
```
### 3.2 修改webpack.config.js文件

```
var HtmlWebpackPlugin = require('html-webpack-plugin');
    var OpenBrowserWebpackPlugin = require('open-browser-webpack-plugin');

     devServer:{
         //指定静态文件根目录
         contentBase:'./build',
         port:8080,
         inline:true //当源代码变化后自动重新打包并通知浏览器刷新
     },

    plugins:[
         new HtmlWebpackPlugin({template:'./app/index.html'}),
         new OpenBrowserWebpackPlugin({url:'http://localhost:8080'})
    ]
```
