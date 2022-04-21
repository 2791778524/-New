<template>
  <div id="app">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <List :items="items" :size="60" :showNumber="10"/>
  </div>
</template>

<script>
import List from './components/List.vue'
export default {
  name: 'App',
  components: {
    List
  },
  computed:{
    items() {
      return Array(10000).fill('').map((item, index)=>({
        id: index,
        content: '列表内容' + index
      }))
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
