# 配置字段

配置字段分为三类:

* `内置配置`: `hiipack`内置的一些配置
* `基础配置`: `webpack`所需要的一些配置
* `扩展配置`: 需要扩展的一些配置，这些配置字段不覆盖`内置配置`，而是合并（**只有对象或者数组类型的配置才合并，其他基本类型字段还是覆盖\*** `自定义配置`: 用户自定义插件或者其他的一些配置

## 内置配置

## 基础配置

基础配置包括:

* `library`: 需要单独打包的模块, 这些模块打包到单独的模块, 便于浏览器缓存
* `babel`: `babel`相关配置
* `entry`: 具体的业务代码入口文件
* `alias`: 模块目录别名，可以简化模块引入的路径，避免复杂的相对路径
* `statics`: 静态文件，静态文件不会被处理，直接复制到编译后的目录中
* `autotest`: 自动化测试相关配置\(这里配置的依赖也不需要自己安装，hiipack会自动安装\), 目前只支持`mocha`

具体使用例子：

## 扩展配置

除了上面的基本配置之外，`hiipack`还支持一些额外的配置来实现一些其他的特性，比如`loaders`可以添加处理其他类型文件的能力，而不需要更新`hiipack`本身。

一个具体的场景：`hiipack`默认不支持`mustache`模板的编译，而我们要在项目中使用`mustache`, 我们可以自己配置`mustache-loader`来支持，**而且我们不需要在前端项目中安装**`mustache-loader`**, 也不需要更新**`hiipack`, 只要配置了`loaders`, `hiipack`内部会自动安装相应的内容。

扩展配置包括:

* `loaders`: 项目需要使用的额外的`loader`\(loader相关的内容可以查看[webpack的文档](https://webpack.github.io/docs/loaders.html)\)，这些`loader`不在`hiipack`原生支持的范围之内。**原生支持的不需要在这里配置**。
* `其他`: 其他的`plugin`或者`loader`需要的配置，直接写到`hii.config.js`中

具体使用例子:

// hii.config.js module.exports = { //... extend: { module: { loaders: [{ test: /\.(mustache|html)$/, loader: 'mustache' }, { 'markdown-loader': function(markdownLoader, markdownLoaderPath) { return { test: /\.(markdown|md)$/, loader: 'html!markdown' } } 'other-loader': { test: /\.md$/, loader: 'html!ohter' } }] }, plugins: [ function() { console.log('custom plugin 1'); }, { 'date-format': function(dateFormat, pkgPath) { console.log('callback2: data-format,', dateFormat, pkgPath); return function() { console.log('custom plugin 2, date =>', dateFormat('yyyy-MM/dd hh||mm//ss.SSS', new Date())); } }, 'underscore float-math': function(_, math, _path, mathPath) { console.log('callback3: data-utils,', _, math, _path, mathPath); return function() { console.log('custom plugin 3', 0.3 - 0.2, math.sub(0.3, 0.2), _.isEmpty([1, 2, 3]), _path, mathPath); } } }], }, vue: { loaders: { js: 'babel-loader?presets[]=' + __hiipack__.resolve('babel-preset-es2015-loose') + '&plugins[]=' + __hiipack__.resolve('babel-plugin-transform-runtime') + '&comments=false' } } }

