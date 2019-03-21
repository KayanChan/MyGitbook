# 在Vue中使用less

@2019-03-13

@(Vue教程)[Vue|Less]

1. 安装依赖

   ```bash
   npm install less less-loader --save
   ```

2. 修改`webpack.base.conf.js`文件，配置loader加载依赖，让其支持外部的less

   在原来的代码上添加：

```javascript
{
  test: /\.less$/,
  loader: "style-loader!css-loader!less-loader"
}
```

3. 使用的时候在`style`标签里加上`lang=”less”`里面就可以写less的代码

   ```vue
   <style lang="less" scoped>...</style>
   ```

   > 加上 scoped 为只在此作用域 有效

   或者`import`引入全局less文件

   ```vue
   @import './index.less'
   ```

   

