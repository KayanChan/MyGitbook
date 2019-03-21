# 在Vue中使用svg图标

@2019-03-13

@(Vue教程)[Vue|svg|iconfont]

1. 安装插件

   ```bash
   npm i svg-sprite-loader --save
   ```

2. 新建组件`components/SvgIcon.vue`

   ```vue
   <template>
     <svg :class="svgClass" aria-hidden="true">
       <use :xlink:href="iconName"></use>
     </svg>
   </template>
   
   <script>
   export default {
     name: 'svg-icon',
     props: {
       iconClass: {
         type: String,
         required: true
       },
       className: {
         type: String
       }
     },
     computed: {
       iconName () {
         return `#icon-${this.iconClass}`
       },
       svgClass () {
         if (this.className) {
           return 'svg-icon ' + this.className
         } else {
           return 'svg-icon'
         }
       }
     }
   }
   </script>
   
   <style scoped>
   .svg-icon {
     width: 1em;
     height: 1em;
     vertical-align: -0.15em;
     fill: currentColor;
     overflow: hidden;
   }
   </style>
   ```

3. 在`src`文件夹下新建文件夹`icons`，`icons`下新建文件夹`svg`和文件`index.js`

   * svg文件夹存放svg图片

   * index.js注册组件`SvgIcon`并且引入svg图片

   ```javascript
   import Vue from 'vue'
   import SvgIcon from '@/components/SvgIcon.vue'
   
   /*
   require.context("./test", false, /.test.js$/);这行代码就会去 test 文件夹（不包含子目录）
   下面的找所有文件名以 .test.js 结尾的文件能被 require 的文件。更直白的说就是 我们可以通过正则匹配引入相应的文件模块。
   require.context有三个参数：
   directory：说明需要检索的目录
   useSubdirectories：是否检索子目录
   regExp: 匹配文件的正则表达式
    */
   // 全局注册
   Vue.component('svg-icon', SvgIcon)
   
   const requireAll = requireContext => requireContext.keys().map(requireContext)
   const req = require.context('./svg', false, /\.svg$/)
   requireAll(req)
   ```

4. 修改`webpack.base.conf.js`文件，配置loader加载依赖

   ```javascript
   {
     test: /\.svg$/,
     loader: 'svg-sprite-loader',
     include: [resolve('src/icons')],
     options: {
       symbolId: 'icon-[name]'
     }
   }
   ```

5. 在`webpack.base.conf.js`中的`url-oader`配置添加

   ```javascript
   {
     test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
     loader: 'url-loader',
     /* -- 开始：添加此行 -- */
     exclude: [resolve('src/icons')],
     /* -- 结束 -- */
     options: {
       limit: 10000,
       name: utils.assetsPath('img/[name].[hash:7].  [ext]')
     }
   }
   ```

6. 使用`svg文件名`来调用（e.g. form.svg）

   > 注意使用字符串`'form'`

   ```javascript
    <svg-icon  :icon-class="'form'"></svg-icon>
   ```

   

