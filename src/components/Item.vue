<template>
  <div class="item">
    <div>
        <el-button>默认按钮</el-button>
        <el-button type="primary">主要按钮</el-button>
        <el-button type="text">文字按钮</el-button>
    </div>
    <div id="app-7">
        <ol>
            <!-- 现在我们为每个todo-item提供待办项对象    -->
            <!-- 待办项对象是变量，即其内容可以是动态的 -->
            <TodoItem v-for="item in groceryList" v-bind:todo="item" v-bind:like="'我们'+like" :key="item.id"></TodoItem>
        </ol>
    </div>
  </div>
</template>

<script>

import TodoItem from './Todo-item'
export default {
  name: 'item',
  components: { TodoItem },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      like: '这是测试的数据',
      groceryList: [
        { text: '蔬菜' },
        { text: '奶酪' },
        { text: '随便其他什么人吃的东西' }
      ]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ol {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
