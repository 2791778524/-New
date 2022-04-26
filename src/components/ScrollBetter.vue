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
        scroll:''
    };
  },
  methods: {},
  mounted() {
    this.$nextTick(() => {
      this.scroll = new BScroll(this.$refs.wrapperRef, {
        scrollY: true,
      });
    });
  },
  computed: {
    items() {
      return Array(1000).fill("").map((item, index) => ({ id: index, content: index + "单元" }));
    },
  },
};
</script>

<style>
#wrapper {
  height: 400px;
  overflow: hidden;
  width: 100%;
}
.item {
  height: 20px;
  line-height: 20px;
}
</style>