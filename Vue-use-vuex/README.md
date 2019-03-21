# 在Vue中使用vuex

@2019-03-18

@(Vue教程)[Vue|vuex|store]

### 目录

* store
  * modules
    * init.js
    * user.js
  * getters.js
  * index.js

### 安装依赖

```bash
npm install -S vuex
```

### 实例化 

**`store/index.js`**

```javascript
import vue from 'vue'
import vuex from 'vuex'
import getters from '@/store/getters'

vue.use(vuex)

const requireFilter = require.context(
  // 指令目录
  '@/store/modules',
  // 不查找子目录
  false,
  // js文件
  /.+\.js$/
)

var modules = {}
// 对每个配匹的文件
requireFilter.keys().forEach(fileName => {
  // 请求指令模块
  const filterConfig = requireFilter(fileName)

  // 获取组件的 PascalCase 命名
  const filterName = fileName
    // 移除开始的 './'
    .replace(/^\.\//, '')
    // 移除文件扩展
    .replace(/\.\w+$/, '')

  modules[filterName] = filterConfig.default || filterConfig
})

const store = new vuex.Store({
  modules: modules,
  getters: getters
})

export default store
```

**`store/getters.js `**

>  getters：vuex的计算属性

```javascript
const getters = {
  token: state => state.a.token,
}

export default getters
```

**`store/modules/init.js`**

> Vuex 允许我们将 store 分割成**模块（module）**。每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块。这样使得应用的单一状态树不会变的臃肿。

```javascript
const init = {
    state: {},
    mutations: {
        INIT_DATA (state, response) {
            // ...
        }
    },
    actions: {
        getInitData ({commit}) {
            commit('INIT_DATA', response)
        }
    }
}
export default init
```

### 主文件引用

```javascript
import store from '@/store'
new Vue({
  el: '#app',
  router,
  store,
  components: { App },
  template: '<App/>'
})
```

### 具体组件调用

state

```javascript
import { mapState } from 'vuex'
```

getters

```javascript
import { mapGetters } from 'vuex'
export default {
  name: 'App',
  computed: {
    ...mapGetters(['direction'])
  }
}
```









