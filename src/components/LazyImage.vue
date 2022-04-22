<template>
  <div class="container">
    <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p><img data-src="../assets/image/1.png" /></p>
   <p><img data-src="../assets/image/1.png" /></p>
   <p><img data-src="../assets/image/1.png" /></p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
   <p>图片懒加载也就是图片的延迟加载</p>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  mounted() {
    //图片懒加载
    // let images = document.documentElement.querySelectorAll("img");
    // let observer = new IntersectionObserver((entries) => {
    //   entries.forEach((entry) => {
    //     if (entry.isIntersecting) {
    //       const image = entry.target;
    //       const data_src = image.getAttribute("data-src");
    //       image.setAttribute("src", data_src);
    //       // 图片被加载后取消观察
    //       observer.unobserve(image);
    //     }
    //   });
    // });
    // images.forEach((image) => {
    //   observer.observe(image);
    // });
    const images = document.querySelectorAll("img");

    // 传给IntersectionObserver的回调函数
    // 在目标元素能看见时触发一次，目标元素看不见了时再触发一次
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
          console.log(entry);
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