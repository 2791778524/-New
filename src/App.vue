<template>
  <div id="app">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <!-- <List :items="items" :size="60" :showNumber="10"/> -->
    <!-- <new-list :items="items" :size="60" :showNumber="10"/> -->
    <!-- <LazyImage></LazyImage> -->
    <ScrollBetter />
  </div>
</template>

<script>
// import List from './components/List.vue'
// import NewList from './components/NewList.vue'
// import LazyImage from './components/LazyImage.vue'
import ScrollBetter from "./components/ScrollBetter.vue";
export default {
  name: "App",
  components: {
    // List,
    // NewList,
    // LazyImage,
    ScrollBetter,
  },
  computed: {
    items() {
      return Array(10000)
        .fill("")
        .map((item, index) => ({
          id: index,
          content: "列表内容" + index,
        }));
    },
    items2() {
      return Array(10000)
        .fill("")
        .map((item, index) => ({
          id: index,
          content: "列表内容二" + index,
        }));
    },
    item3() {
      return Array(1000)
        .fill("")
        .map((item, index) => ({
          id: index,
          content: "列表内容三" + index,
        }));
    },
  },
};
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
