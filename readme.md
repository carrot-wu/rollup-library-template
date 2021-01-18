
## 个人通用库编写rollup模板

## 开发事项

当前插件支持以下功能:
1. typescript编写支持
2. 自动添加路径别名的使用
3. eslint + prettier
4. babel根据预设浏览器版本或者node版本进行代码自动polyfill
5. 自带压缩以及支持多模块化打包


### babel配置

babel直接用的是`@babel/preset-env`(可续可能会切换到更适合通用库开发的`@@babel/plugin-transform-runtime`,两者间的不同具体可以看babel官网)。

babel配置只需要关注在.browserslistrc上即可，可根据具体的开发库类型，兼容特定的浏览器版本或者node版本即可。

### external的使用(类似于peerDependencies)

一般来说，rollup会把项目中引入的依赖都打包进库中，但是许多情况下一些包是不需要打包进来的，类似于开发react组件但是没必要把react打包进组件库一样。

这时候只需要在`rollup.config.js`配置中配置相关的external配置即可

### 路径别名的使用
路径别名的使用引用的是官方的`@rollup/plugin-alias`,相关配置在`rollup.config.js`跟着官网配置配置即可。

对于ts而言，还需要在`tsconfig.extend.json`下进行路径别名的映射，不然ts会无法识别而报ts错误。
