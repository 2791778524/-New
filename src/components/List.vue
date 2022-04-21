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
    items: {
      type: Array,
      required: true,
    },
    size: {
      type: Number,
      required: true,
    },
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
    showData() {
      return this.items.slice(this.start, this.end);
    },
    containerHeight() {
      return this.size * this.showNumber + "px";
    },
    barheight() {
      return this.size * this.items.length - 1 + "px";
    },
    listTop() {
        return this.size * this.start + 'px'
    }
  },
  methods: {
    handleScroll() {
      let scrollTop = this.$refs.container.scrollTop;
      this.start = Math.floor(scrollTop / this.size)
      this.end = this.start + this.showNumber
    },
  },
};
</script>

<style>
.container {
  position: relative;
  overflow-y: scroll;
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