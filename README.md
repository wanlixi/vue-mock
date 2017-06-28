# template

> A Vue.js project

## Build Setup

#### 首先把template文件解压到当前的文件下，然后 npm i

``` 
bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

```
### mock.js
```
import Mock from 'mockjs'

Mock.mock('/user/list',{
    // 属性 list 的值是一个数组，其中含有 1 到 10 个元素
    'list|1-10': [{
        // 属性 id 是一个自增数，起始值为 1，每次增 1
        'id|+1': 1,
        'name'	   : '@name',
        'age|1-100': 100,
        'color'	   : '@color'
    }]
})
```
### main.js
```
import axios from 'axios'
import Vue from 'vue'
require('@/services/mock.js')

Vue.prototype.$axios = axios
```

### app.vue
```
<template>
  <div class="hello">
    <p v-for="(item,index) in user.list">
      id: <span>{{item.id}}</span>   
      color: <span>{{item.color}}</span>  
      name: <span>{{item.name}}</span>  
      age: <span>{{item.age}}</span>  
    </p>
  </div>
</template>

<script type="text/babel">
export default {
  data () {
    return {
      user: []
    }
  },
  mounted () {
    this.$axios({
      url: '/user/list',
      method: 'post',
      data: {
        userId: 12
      }
    }).then(res => {
      this.user = res.data
    }).catch(err => {
      // console.log(err)
    })
  },
  methods: {

  }
}
</script>

<style lang="stylus" scoped>

</style>

```
