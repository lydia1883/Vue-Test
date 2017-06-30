

<template>
  <div class="test">
    <h1>{{ testVal }}</h1>
    <h1 id="app">{{ message }}</h1>
    <h2>Essential Links</h2>
    <ul>
      <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://gitter.im/vuejs/vue" target="_blank">Gitter Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
      <br>
      <li><a href="http://vuejs-templates.github.io/webpack/" target="_blank">Docs for This Template</a></li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
    </ul>
    <div>
      <span v-bind:title="curTime"> 
          鼠标悬停几秒钟查看此处动态绑定的提示信息！
      </span>
    </div>
    <div id="app-3">
      <p v-if="seen">现在你看到我了</p>
    </div>

    <div id="app-4">
      <ol>
        <li v-for="todo in todos" :key="todo.id">
          {{ todo.text }}
        </li>
      </ol>
    </div>

    <div id="app-5">
      <p>{{ message }}</p>
      <button v-on:click="reverseMessage">逆转消息</button>
    </div>

    <div id="app-6">
      <p>{{ message }}</p>
      <input v-model="message">
    </div>

    <a v-bind:href="url">google</a>
    <a v-on:click="doSomething">点击事件</a>

    <a :href="url">缩写 google</a>
    <a @click="doSomething">点击事件</a>

    <div>
      <p>Original message: "{{ message }}"</p>
      <p>Computed reversed message: "{{ reversedMessage }}"</p>
     
      <p>Now: "{{ now() }}"</p>
    </div>
    <div id="demo">{{ fullName }}</div>


    <div id="watch-example">
      <p>
        Ask a yes/no question:
        <input v-model="question">
      </p>
      <p>{{ answer }}</p>
    </div>
    

    <div class="static"
     v-bind:class="{ active: isActive, 'text-danger': hasError }">
    </div>

    <div v-bind:class="classObject"></div>
  </div>
  
</template>


<script>

import axios from 'axios'
var _ = require('lodash')

let appTest = {
  name: 'test',
  created: function () {
    this.doTest()
  },
  computed: {
    reversedMessage: function () {
      // `this` points to the vm instance
      return this.message.split('').reverse().join('')
    },
    fullName: function () {
      return this.firstName + ' ' + this.lastName
    },
    classObject: function () {
      return {
        active: this.isActive && !this.error,
        'text-danger': this.error && this.error.type === 'fatal'
      }
    }
  },
  methods: {
    now: function () {
      return this.date
    },
    getAnswer: _.debounce(
      function () {
        var self = this
        if (this.question.indexOf('?') === -1) {
          self.answer = 'Questions usually contain a question mark. ;-)'
          return
        }
        self.answer = 'Thinking...'
        axios.get('https://yesno.wtf/api').then(function (response) {
          self.answer = _.capitalize(response.data.answer)
        })
        .catch(function (error) {
          self.answer = 'Error! Could not reach the API. ' + error
        })
      }
    )
  },
  watch: {
    question: function (newQuestion) {
      this.answer = 'Waiting for you stop typing...'
      this.getAnswer()
    }
  },
  data: () => {
    return {
      testVal: 'Welcome to My Vue.js App',
      message: 'Hello Vue!',
      curTime: '页面加载于 ' + new Date(),
      seen: true,
      date: Date.now(),
      firstName: 'Foo',
      lastName: 'Bar',
      question: '',
      answer: 'I cannot give you an answer until you ask a question!',
      isActive: true,
      error: null,
      hasError: false,
      url: 'https://www.google.com',
      todos: [
        { text: '学习 JavaScript' },
        { text: '学习 Vue' },
        { text: '整个牛项目' }
      ],
      reverseMessage: () => {
        this.message = this.message.split('').reverse().join('')
      },
      doSomething: () => {
        this.message = '练习VUE'
      },
      doTest: function () {
        this.message = '测试今天的东西'
      }
    }
  }
}

export default appTest
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #44b983;
}
</style>

