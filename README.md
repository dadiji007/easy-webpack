## 目录树：
- example
    - entry.js
    - message.js
    - name.js
- bundler.js

## 思路：

    - 1、分析依赖：
        webpack分析依赖，通过入口文件开始。webpack会通过入口文件读取内部信息（字符串），将内部信息转化为ast，形成一个数据结构（包含filename、dependencies等）。我们通过传入[文件路径]从而得到这么一个数据结构，而构成这个数据结构的函数在此称为 createAsset()

    - 2、createAsset：（依赖数据结构）
        createAsset()，当传入一个文件路径时，会返回一个数据结构，里面包含：{
            id、filename、dependencies（依赖）、code（模块）
        }，并提交到下一个函数进行遍历依赖 createGraph()

    - 3、createGraph：（依赖图）
        createGraph()，在里面循环遍历（使用createAsset()）每一个文件路径，获得所有的文件依赖(dependencies)，广度遍历后，将返回每一个文件的数据，并将它们集合到一个数组中。最终用浏览器可以运行的方式在 bundle() 函数中进行处理，生成最终的样式。

    - 4、bundle：（处理并返回最终能够在浏览器中执行的匿名函数）
        bundle，在里面将通过forEach()将createGraph()中集合的数组进行依赖关系的处理，返回一个能够处理所有需要打包的js文件能够运行的环境。

* 使用：
   > `$ npm i `
   > `$ node bundler`
   > `$ node bundle`       //hello world!
