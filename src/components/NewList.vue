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
        //设置展示列表数量的高度
        containerHeight() {
            return this.showNumber * this.size + 'px' 
        },
        //截取要展示的列表start~end
        showData() {
            return this.items.slice(this.start, this.end)
        },
        //设置所有列表的高度撑开
        topHeight() {
            return this.start * this.size + 'px'
        },
        //设置为一列表数量的高度
        barHeight() {
            return this.size * this.items.length + 'px'
        }
    },
    methods:{
        //监听滚动事件
        handleScroll() {
            let scrollTop = this.$refs.containerRef.scrollTop;
            //向上取整start的位置
            this.start = Math.floor(scrollTop / this.size)
            //设置end的位置
            this.end = this.start + this.showNumber;
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