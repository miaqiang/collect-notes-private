webpack是一个模块打包工具，你可以使用webpack管理你的模块依赖，并编译输出模块们所需的静态文件。它能够很好的管理、打包web开发中所用到的HTML、JavaScript、css以及各种静态文件（图片，字体等），让开发过程更加高效。对于不同类型的资源，webpack有对应的模块加载器。webpack模块打包器会分析模块间的依赖关系，最后生成了优化且合并后的静态资源。

webpack的两大特色：
    
    code splitting（可以自动完成）
    loader 可以处理各种类型的静态文件，并且支持串联操作

webpack是以commonJS的形式来书写脚本的，但对于AMD/CMD的支持也很全面，方便旧项目进行代码迁移。

webpack具有requireJS和browserify的功能，但仍有很多自己的新特性：
    
    1. 对CommonJS、AMD、ES6的语法做了兼容
    2. 对js、css、图片等资源文件都支持打包
    3. 串联式模块加载器以及插件机制，让其具有更好的灵活性和扩展性，例如提供对CoffeeScript、ES6的支持
    4. 有独立的配置文件 webpack.config.js
    5. 可以将代码切割成不同的chunk，实现按需加载，降低了初始化时间
    6. 支持sourceUrls和SourceMap，易于调试
    7. 具有强大的Plugin接口，大多是内部插件，使用起来比较灵活
    8. webpack使用异步IO并具有多级缓存，这是的webpack很快且在增量编译上更加快。