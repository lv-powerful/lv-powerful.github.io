# 
每次请上传最新更改好的原始原始压缩包就行，除去node_modules压缩包
#
下载压缩包后执行npm install会自动下载项目所需要的node_modules包
#
部署手机端到二级目录下时，修改一下三个文件内容
#
**1.路径./src/router/index.js文件中添加base:'/二级目录名称/'，**
```JavaScript
export default new Router({
  mode:'history',//此处代码去除#
  base:'/web/',//此处添加
  routes: [
    {
      path: '/',
      name: 'index',
      component: index
    }
  ]
})
```
#
**2.路径./config/index.js文件中大约46行处将build对象中assetsPublicPath: '/',改为assetsPublicPath: './',**
```JavaScript
build: {
  // Template for index.html
  index: path.resolve(__dirname, '../dist/index.html'),
  // Paths
  assetsRoot: path.resolve(__dirname, '../dist'),
  assetsSubDirectory: 'static',
  assetsPublicPath: './',//修改此处

  productionSourceMap: true,
  // https://webpack.js.org/configuration/devtool/#production
  devtool: '#source-map',

  // Gzip off by default as many popular static hosts such as
  // Surge or Netlify already gzip all static assets for you.
  // Before setting to `true`, make sure to:
  // npm install --save-dev compression-webpack-plugin
  productionGzip: false,
  productionGzipExtensions: ['js', 'css'],

  // Run the build command with an extra argument to
  // View the bundle analyzer report after build finishes:
  // `npm run build --report`
  // Set to `true` or `false` to always turn it on or off
  bundleAnalyzerReport: process.env.npm_config_report
}
```
#
**3.路径./build/utils.js文件中大约五十行左右添加 publicPath:'../../',**
```JavaScript
if (options.extract) {
  return ExtractTextPlugin.extract({
    use: loaders,
    publicPath:'../../',//添加内容
    fallback: 'vue-style-loader'
  })
} else {
  return ['vue-style-loader'].concat(loaders)
}
```
