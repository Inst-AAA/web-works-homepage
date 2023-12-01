<template>
  <!--  back-to-top button  -->
  <v-btn
    v-show="showButton"
    fab
    outlined
    small
    color="secondary"
    style="position:fixed; bottom:12px; right: 16px; z-index: 2998; background-color: rgba(255,255,255,0.34)"
    @click="scrollToTop"
  >
    <v-icon size="20px">mdi-arrow-up</v-icon>
  </v-btn>
</template>

<script>

export default {
  data: () => ({
    // back-to-top
    showButton: false,
  }),
  mounted() {
    // 监听页面滚动事件
    window.addEventListener('scroll', this.handleScroll);

    // 初始化时检查是否在页面顶部
    this.checkScrollPosition();
  },
  beforeDestroy() {
    // 移除事件监听器，以防止内存泄漏
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    handleScroll() {
      // 监听滚动事件，检查是否在页面顶部
      this.checkScrollPosition();
    },
    checkScrollPosition() {
      // 判断是否在页面顶部
      this.showButton = window.scrollY > 0;
    },
    scrollToTop() {
      // 按钮按下时回到顶部
      window.scrollTo({
        top: 0,
        behavior: 'smooth', // 使用平滑滚动效果
      });
    },
  },
}
</script>


<style scoped>

</style>