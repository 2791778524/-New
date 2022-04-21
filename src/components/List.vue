<template>
  <div
    class="container"
    :style="{ height: containerHeight }"
    @scroll="handleScroll"
    ref="container"
  >
    <div class="list"
    :style="{top: listTop}">
      <div
        v-for="item in showData"
        :key="item.id"
        :style="{ height: size + 'px' }"
      >
        {{ item.content }}
      </div>
    </div>
    <div class="bar" :style="{ height: barheight }"></div>
  </div>
</template>

<script>
export default {
  props: {
      //所有列表
    items: {
      type: Array,
      required: true,
    },
    //每列的高度
    size: {
      type: Number,
      required: true,
    },
    //显示几条数据
    showNumber: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      start: 0,
      end: this.showNumber,
    };
  },
  computed: {
    //截取要展示的列表start~end
    showData() {
      return this.items.slice(this.start, this.end);
    },
    //设置展示列表数量的高度
    containerHeight() {
      return this.size * this.showNumber + "px";
    },
    //设置所有列表的宽度撑开
    barheight() {
      return this.size * this.items.length - 1 + "px";
    },
    //设置为一列表数量的高度
    listTop() {
        return this.size * this.start + 'px';
    }
  },
  methods: {
    handleScroll() {
      let scrollTop = this.$refs.container.scrollTop;
      //向上取整start的位置
      this.start = Math.floor(scrollTop / this.size)
      this.end = this.start + this.showNumber;
    },
  },
};
</script>

<style>
.container {
  position: relative;
  overflow-y: auto;
  background: rgb(150, 195, 232);
  font-size: 20px;
  font-weight: bold;
  line-height: 60px;
}
.list {
  position: absolute;
  top: 0;
  width: 100%;
}
</style>