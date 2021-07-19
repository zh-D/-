《深入浅出 Webpack》

p2~p8：模块化的发展（CommonJS、AMD、ESM。。。）、新框架的出现（三大框架）、新语言（ES6、TypeScript、Flow、SCSS）

以上各种可以提高开发效率的新思想和框架层出不穷。但是它们都有一个共同点：源代码无法直接运行，必须通过转换后才可以正常运行。

p9：构建就是做这件事情，将源代码换成可执行的 Javascript、CSS、HTML 代码，包括如下内容：

- 代码转换：TypeScript-->JavaScript、SCSS-->CSS 等
- 文件优化：压缩 JavaScript、CSS、HTML 代码，压缩合并图片等
- 代码分割：提取多个页面的公共代码，提取首屏不需要执行部分的代码让其异步加载
- 模块合并：在采用模块化的项目里会有很多个模块和文件，需要通过构建功能将模块分类合并成一个文件
- 自动刷新：监听本地源代码的变化，自动重新构建、刷新浏览器
- 代码校验：在代码被提交到仓库前需要校验代码是否符合规范，以及单元测试是否通过
- 自动发布：更新代码后，自动构建出线上发布代码并传输给发布系统

构建其实是工程化、自动化思想在前端开发中的体现。将一系列流程用代码去实现。让代码自动化地执行这一系列复杂的流程。构建为前端开发注入了更大的活力，解放了我们的生产力。

下面来看一下一系列的构建工具，一个历史。

#### Npm Script

Npm Script ( https: //docs.npmjs.com/misc/scripts ）是一个任务执行者。 Npm 是在安装 Node.js 时附带的包管理器， Npm Script 则是 Npm 内置的一个功能，允许在 package.json 文件里面使用 scripts 字段定义任务：

```json
{
  ”scripts ”: {
    ” dev”:”node dev. j s ”,
    ” pub”:”node build. j s ”
  }
}
```

里面的 scripts 字段是一个对象，每个属性对应一段 Shell 脚本，以上代码定义了两个任务：dev 和 pub。其底层实现原理是通过调用 Shell 命令去运行脚本，例如：执行 npm run pub 命令等同于执行 node build.js 命令

Npm Script 的优点是内置，无需安装其它依赖。其缺点是功能太简单，虽然提供了 pre 和 post 两个钩子，但不能方便地管理多个任务之间的依赖。

#### Grunt

p10：

Grunt(https://gruntjs.com) 和 Npm Script 类似，也是一个任务执行者。Grunt 有大量现成的插件封装了常见的任务，也能管理任务之间的依赖关系，自动化地执行依赖任务，每个任务的具体执行代码和依赖关系写在配置文件 Gruntfile.js 里，例如：

```javascript
module.exports = function(grunt) {
// 所有插件的配置信息
grunt .initConfig({
//uglify 插件的配置信息
    uglify: {
        app_task: {
            files: {
                "build/app.min.js":['lib/index.js','lib/test.js']
            }
        }
    },
    //watch 插件的配置信息
    watch: {
        another: {
            files :['lib/*.js'],
        }
    }
});
//告诉 Grunt 我们将使用这些插件
grunt.loadNpmTasks('grunt-contrib-uglify') ;
grunt.loadNpmTasks('grunt-contrib-watch');
// 告诉 Grunt 我们将在终端启动 Grunt 时需要执行哪些任务
grunt.registerTask('dev', ['uglify', 'watch']); 
};
```

在项目根目录下执行命令 grunt dev，就会启动 JavaScript 文件压缩和自动刷新功能

Grunt 的优点是：
- 灵活，他只负责执行我们定义的任务
- 大量的可复用插件封装好了常见的构建任务

Grunt 缺点是集成度不高，要写很多配置后才可以使用，无法做到开箱即用。
Grunt 相当于进化版的 Npm Script，它的诞生其实是为了弥补 Npm Script 的不足。

#### Gulp

Gulp(http://gulpjs.com) 是一个基于流的自动化构建工具，处理可以管理和执行任务，还支持监听文件、读写文件。Gulp 被设计得非常简单，只通过下面五种方法就可以支持几乎所有构建场景：
- 通过 gulp.task 注册一个任务
- 通过 gulp.run 执行任务
- 通过 gulp.watch 监听文件变化
- 通过 gulp.src 读取文件
- 通过 gulp.dest 写文件

Gulp 的最大特点是引入了流的概念，同时提供了一些列常用的插件去处理流。流可以在插件之间传递，大致使用如下：

```javascript
// 引入 Gulp
// 引入插件
// 编译 SCSS 任务
// 监听文件变化
```

Gulp 的优点是好用又不失灵活，既可以单独完成构建，也可以和其它工具搭配使用。其缺点和 Grunt 类似，集成度不高，要写很多配置后才可以用，无法做到开箱即用。

可以将 Gulp 看作 Grunt 的加强版。相对于 Grunt，Grunt 增加了监听文件、读写文件、流式处理的功能。

#### Fis3
Fis3(http://fex.baidu.com/fis3/)是一个来自百度的优秀国产构建工具。相对于 Grunt、Gulp 只提供了基本功能的工具，Fis3 集成了 Web 开发中常用的构建功能，如下所述。

- 读写文件
- 资源定位
- 文件指纹
- 文件编译
- 压缩资源
- 图片合并

可以看出 Fis3 很强大，内置了许多功能，无须做太多配置就能完成大量工作。

Fis3 的优点是集成了各种 Web 开发所需的构建功能，配置简单、开箱即用。其缺点是目前官方已经不再更新和维护，不支持最新版本的 Node

Fis3 是一种专注于 Web 开发的完整解决方案，如果将 Grunt、Gulp 比作汽车的发动机，则可以将 Fis3 比作一辆完整的汽车。

Webpack(https://webpack.js.org)是一个打包模块化 JavaScript 的工具，在 Webpack 里一切文件皆模块，通过 Loader 转换文件，通过 Plugin 注入钩子，最后输出由多个模块组合成的文件。Webpack 专注于构建模块化项目。

一切文件如 JavaScript、CSS、SCSS、图片、模板，对于 Webpack 来说都是一个个模块，这样的好处是能清晰地描述各个模块之间的依赖关系，以方便 Webpack 对模块进行组合和打包。经过 Webpack 的处理，最终会输出浏览器能使用的静态资源。

Webpack 的优点是：

- 专注于处理模块化的项目，能够做到开箱即用、一步到位；
- 可通过 Plugin 扩展，完整好用又不失灵活
- 使用场景不局限于 Web 开发
- 社区庞大活跃，经常引入紧跟时代发展的新特性，能为大多数场景找到已有的开源扩展
- 良好的开发体验

Webpack 的缺点是只能用于采用模块化开发的项目

#### Rollup

Rullup(https://rollupjs.org) 是一个和 Webpack 很类似但专注于 ES6 的模块打包工具。它的亮点在于，能针对 ES6 源码进行 Tree Shaking，以去除那些已经被定义但是没被使用的代码并进行 Scope Hoisting，以减小输出文件的大小和提升运行性能。然而 Rollup 的这些两点随后就被 Webpack 模仿和实现。由于 Rollup 的使用方法和 Webpack 差不多，所以这里就不详细介绍如何使用 Rollup 了，而是详细说明它们的区别：
- Rollup 是在 Webpack 流行后出现的替代品
- Rollup 生态链不够完善，体验不如 Webpack
- Rollup 功能不如 Webpack 完善，但其配置和使用更简单
- Rollup 不支持 Code Splitting，但好处是在打包出来的代码中没有 Webpack 那段模块的加载、执行和缓存的代码。

Rollup 在用于打包 JavaScript 库时比 Webpack 更有优势，因为其打包出来的代码体积更小、更快。但它的功能不够完善，在很多场景下都找不到现成的解决方案。

#### 为什么选择 Webpack

p16

上面介绍的构建工具是按照它们诞生的时间排序的，它们是时代的产物，侧面反映出 Web 开发的发展趋势，如下所示：

- Npm Script 和 Grunt 时代，Web 开发要做的事情变多，流程复杂，自动化思想被引入，用于简化流程
- 在 Gulp 时代，开始出现一些新语言用于提高开发效率，流式处理思想的出现是为了简化文件转换的过程，例如将 ES5 转化为 ES6
- 在 Webpack 时代，由于单页应用的流行，网页的功能和实现代码变得复杂、庞大，Web 开发向模块化改进

这些构建工具都有各自的定位和专注点，他们之间既可以单独完成任务，也可以相互搭配来弥补各自的不足。在了解这些常见的构建工具后，我们需要根据自己的需求去判断应该如何选择和搭配它们才能更好地满足自己的需求。

经过多年的发展，Webpack 已经成为构建工具中的首选，这是有原因的：
- 大多数团队在开发新项目的时候会采用紧跟时代的技术，这些技术几乎都会采用“模块化+新语言+新框架”，Webpack 可以为这些新项目提供一战式的解决方案
- Webpack 有良好的生态链和维护团队，能提供良好的开发体验并保证质量
- Webpack 被全世界大量的 Web 开发者使用和验证，能找到各个层面所需的教程和经验分享。
