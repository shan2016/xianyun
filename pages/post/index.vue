<template>
  <div class="container">
    <div class="post-left">
      <PostAside></PostAside>
    </div>
    <div class="post-right"></div>
  </div>
</template>

<script>
import PostAside from "@/components/post/postAside.vue";
export default {
  components: {
    PostAside
  },
  data() {
    return {};
  }
};
</script>

<style scoped lang="less">
.container {
  width: 1000px;
  margin: 20px auto;
  position: relative;
  .post-left {
    width: 260px;
    // border: 1px solid #ddd;
  }
}
</style>