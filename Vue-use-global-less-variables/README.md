# 在Vue中使用全局less变量

### 场景

由于Vue单文件组建内，less变量不能共享；

若每个文件都要@import一遍，文件路径发生变化就需要全部引入该文件的页面修改一遍；

**期望一次全局引入，所有VUE页面均自动引入**



### 实现

1. 安装依赖

   ```bash
   npm install sass-resources-loader --save-dev
   ```

   

2. 配置模块

   * 方法一：在`build/utils.js`的`generateLoaders`方法中调整

     ```javascript
     // 原来的
     less: generateLoaders('less'),
     
     // 调整，全局引入 base.less 和 mixin.less
     less: generateLoaders('less').concat({
         loader: 'sass-resources-loader',
         options: {
             resources: [
                 path.resolve(__dirname, '../src/style/base.less'),
                 path.resolve(__dirname, '../src/style/mixin.less')
             ]
         }
     }),
     ```

     

   * 方法二：在`build/utils.js`中添加方法`lessResourceLoader`,接着在`generateLoaders`方法中调整

     ```javascript
     // 添加方法
     function lessResourceLoader() {
         var loaders = [
           cssLoader,
           'less-loader',
           {
             loader: 'sass-resources-loader',
             options: {
               resources: [
                     path.resolve(__dirname, '../src/style/base.less'),
                     path.resolve(__dirname, '../src/style/mixin.less')
               ]
             }
           }
         ];
         if (options.extract) {
           return ExtractTextPlugin.extract({
             use: loaders,
             fallback: 'vue-style-loader'
           })
         } else {
           return ['vue-style-loader'].concat(loaders)
         }
     }
     // 调整配置
     // 原来的
     less: generateLoaders('less'),
     
     // 调用新添加的方法
     less: lessResourceLoader(),
     ```



3. `npm run dev`重新启动