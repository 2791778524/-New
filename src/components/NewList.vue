<template>
<!-- 虚拟列表实现 -->
  <div class="container" :style="{height: containerHeight}" @scroll="handleScroll" ref='containerRef'>
      <div class="list"
      :style="{top: topHeight}">
          <div v-for="item in showData" :key="item.id">{{item.content}}</div>
      </div>
      <div class="bar" :style="{height :barHeight}"></div>
  </div>
</template>

<script>
export default {
    props:{
        items: {
            type:Array,
            required: true
        },
        size: {
            type: Number,
            required: true
        },
        showNumber: {
            type: Number,
            required: true
        }
    },
    data() {
        return{
            start: 0,
            end: this.showNumber,
        }
    },
    computed:{
        containerHeight() {
            return this.showNumber * this.size + 'px' 
        },
        showData() {
            return this.items.slice(this.start, this.end)
        },
        topHeight() {
            return this.start * this.size + 'px'
        },
        barHeight() {
            return this.size * this.items.length + 'px'
        }
    },
    methods:{
        handleScroll() {
            let scrollTop = this.$refs.containerRef.scrollTop;
            this.start = Math.floor(scrollTop / this.size)
            this.end = this.start + this.showNumber
            console.log(this.start, this.end);
        }
    }
}
</script>

<style scoped>
.container {
    position: relative;
    text-align: center;
    overflow-y: scroll;
    background: rgb(150, 195, 232);
}
.list{
    position: absolute;
    top: 0;
    width: 100%;
}
</style>