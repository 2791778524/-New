<template>
  <div class="container">
    <p><img data-src="../assets/image/1.png" /></p>
    <p><img data-src="../assets/image/1.png" /></p>
    <p><img data-src="../assets/image/1.png" /></p>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  mounted() {
    //图片懒加载
    let images = document.documentElement.querySelectorAll("img");
    let observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          const image = entry.target;
          const data_src = image.getAttribute("data-src");
          image.setAttribute("src", data_src);
          // 图片被加载后取消观察
          observer.unobserve(image);
        }
      });
    });
    images.forEach((image) => {
      observer.observe(image);
    });
  },
};
</script>

<style>
</style>