<template>
  <div id="wrapper" ref="wrapperRef">
    <div class="content">
      <div class="item" v-for="item in items" :key="item.id">
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
    };
  },
  methods: {},
  mounted() {
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
      this.scroll.on("pullingUp", () => {
        setTimeout(() => {
          this.scroll.finishPullUp();
          console.log('加载剩下的内容');
        }, 1000);
      });
      this.scroll.on("pullingDown", () => {
        console.log("22222");
        setTimeout(() => {
          this.scroll.finishPullDown();
          console.log('下拉刷新加载内容');
        }, 1000);
      });
    });
  },
  computed: {
    items() {
      return Array(100)
        .fill("")
        .map((item, index) => ({ id: index, content: index + "单元" }));
    },
  },
};
</script>

<style>
#wrapper {
  height: 400px;
  overflow: hidden;
  width: 100%;
  text-align: center;
}
.item {
  height: 20px;
  line-height: 20px;
  width: 100%;
}
</style>