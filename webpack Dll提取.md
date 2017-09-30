## webpack dll 公共包提取
> - 项目中经常包含很多不常更改的库，每次打包的时候都非常慢，这里讲项目中用到的类库提取成dll.js，只用打包一次，后面就引用这个就行了，这样可以大幅提高打包速度。
> - 通常结合DllReferencePlugin，DllPlugin来达到提取dll,优化打包速度的目的；DllPlugin来执行提取操作，DllReferencePlugin来告诉webpack哪些类已经打包过啦，你不用再管啦。
> - 这里基于的是vue-cli的配置做的更改

## 操作流程
#### 1. 在build文件夹新增webpack.dll.js文件
```js
const path = require('path')
const webpack = require('webpack')
const ParallelUglifyPlugin = require('webpack-parallel-uglify-plugin')

module.exports = {
    entry: {
        vendor: [
            //   'q',
            //   'axios',
            'newlife',
            //   'vue/dist/vue.common.js',
            'vue-router',
            'vuex',
            'babel-polyfill'
        ]
    },
    output: {
        path: path.resolve(__dirname, '../static/js'),
        filename: '[name].dll.js',
        library: '[name]_library'
    },
    module: {
        loaders: [
            {
                test: /\.vue$/,
                loader: 'vue'
            },
            {
                test: /\.js$/,
                loader: 'babel-loader',
                exclude: /node_modules\/(?!(autotrack|dom-utils))/
            }
        ]
    },
    plugins: [
        new webpack.DllPlugin({
            path: path.join(__dirname, '.', '[name]-manifest.json'),
            libraryTarget: 'commonjs2',
            name: '[name]_library',
        }),
        new ParallelUglifyPlugin({
            cacheDir: '.cache/',
            uglifyJS: {
                output: {
                    comments: false,
                    beautify: false
                },
                compress: {
                    warnings: false,
                    drop_console: true
                }
            }
        }),
    ]
}
```
Tips: 
* vendor里面的库名，最好写上那些不常更改的库，经常更改的就没必要写在里面了，因为这个里面的每次更改的话，还是要重新打包dll的。
* 这里用到了一个ParallelUglifyPlugin的库，建议使用它来替代UglifyJsPlugin，它会缓存打包信息，第一次打包会和正常一样，但后面再打包就会大大提高打包速度。

#### 2. 更改webpack.base.js内容
```js
// 这里添加个提高打包速度的一个小技巧，在modeule/rulse里面的loader属性里面都添加上include字段，指明查找范围，提高webpack打包时搜索效率 如下
{
    test: /\.js$/,
    // loader: 'babel-loader',
    loader: 'babel-loader?cacheDirectory=true',     // 添加babel缓存
    exclude: /node_modules/,
    include: [resolve('src'), resolve('test')]
},
{
    test: /\.(woff2?|eot|ttf|otf)(\?.*)?$/,
    loader: 'url-loader',
    include: [resolve('src/scss/fonts')],           // 指明字体字体图标查找范围
    options: {
        limit: 10000,
        name: utils.assetsPath('fonts/[name].[hash:7].[ext]'),
        publicPath: '../../'                        // 解决打包后字体图标文件路径问题
    }
}

// config里添加如下plugin内容
plugins: [
    new webpack.DllReferencePlugin({
        context: path.resolve(__dirname, '..'),
        manifest: require('./vendor-manifest.json')
    })
]
```

#### 3. 更改根目录下index.html模板文件，在js部分添加（注意顺序）
```html
<script  src="<%= webpackConfig.output.publicPath %>static/js/vendor.dll.js"></script>
```

