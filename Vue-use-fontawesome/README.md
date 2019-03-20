# 在Vue中使用Fontawesome

@2019-03-20

@(Vue教程)[Vue|icon|fontawesome]

1. 安装fontawesome

   ```
   npm i --save @fortawesome/fontawesome
   npm i --save @fortawesome/vue-fontawesome
   npm i --save @fortawesome/fontawesome-svg-core
   ```

   

2. 安装fontawesome样式依赖

   ```
   npm i --save @fortawesome/fontawesome-free-solid
   npm i --save @fortawesome/fontawesome-free-regular
   npm i --save @fortawesome/fontawesome-free-brands
   ```



3. 配置main.js

   ```javascript
   import fontawesome from '@fortawesome/fontawesome'
   import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
   import solid from '@fortawesome/fontawesome-free-solid'
   import regular from '@fortawesome/fontawesome-free-regular'
   import brands from '@fortawesome/fontawesome-free-brands'
   
   fontawesome.library.add(solid)
   fontawesome.library.add(regular)
   fontawesome.library.add(brands)
   
   Vue.component('font-awesome-icon', FontAwesomeIcon)
   ```

4. 在[官网](https://fontawesome.com/icons)找对应所需的icon

