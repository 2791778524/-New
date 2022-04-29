<template>
  <div id="wrapper" ref="wrapperRef">
    <div class="content" ref="contentRef">
      <div class="item" v-for="item in dataInfo" :key="item.id">
        {{ item.content }}
      </div>
    </div>
  </div>
</template>

<script>
import BScroll from "better-scroll";
export default {
  data() {
    return {
      scroll: "",
      dataInfo: [],
      showNumber: 15,
      start: 0,
      end: 0,
    };
  },
  methods: {},
  mounted() {
    this.end = this.showNumber;
    this.dataInfo = this.items.slice(this.start, this.end);
    this.$nextTick(() => {
      this.scroll = new BScroll(this.$refs.wrapperRef, {
        scrollY: true,
        pullUpLoad: {
          threshold: -30,
        },
        pullDownRefresh: {
          // 下拉距离超过30px触发pullingDown事件
          threshold: 30,
          // 回弹停留在距离顶部20px的位置
          stop: 20,
        },
      });
      //上拉加载
      this.scroll.on("pullingUp", () => {
        if (this.end < this.items.length) {
          setTimeout(() => {
            this.start = this.end;
            this.end = this.start + this.showNumber;
            this.dataInfo = this.items.slice(this.start, this.end);
            console.log(this.start, this.end, this.dataInfo);
            console.log(this.start, this.end, this.dataInfo);
            console.log("加载成功");
            this.scroll.finishPullUp();
          }, 1000);
        } else {
          console.log("我已经给不了你更多了");
          this.scroll.finishPullUp();
          return;
        }
      });
      //下拉刷新
      this.scroll.on("pullingDown", () => {
        if (this.start > 0) {
          setTimeout(() => {
            this.end = this.start;
            this.start = this.end - this.showNumber;
            this.dataInfo = this.items.slice(this.start, this.end);
            console.log(this.end, this.start, this.dataInfo);
            console.log(this.end, this.start, this.dataInfo);
            this.scroll.finishPullDown();
            console.log("下拉刷新加载内容");
          }, 1000);
        } else {
          console.log("到顶了");
          this.scroll.finishPullDown(); 
          return;
        }
      });
    });
  },
  computed: {
    items() {
      return Array(66)
        .fill("")
        .map((item, index) => ({ id: index, content: index + "单元" }));
    },
  },
};
</script>

<style>
#wrapper {
  height: 450px;
  overflow: hidden;
  width: 100%;
  text-align: center;
}
.item {
  height: 50px;
  line-height: 50px;
  width: 100%;
}
</style>