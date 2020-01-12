<template>
  <div class="container clearfix">
    <div class="post-left clearfix">
      <PostAside></PostAside>
    </div>
    <div class="post-right clearfix">
      <PostRight></PostRight>
    </div>
  </div>
</template>

<script>
import PostAside from "@/components/post/postAside.vue";
import PostRight from "@/components/post/postRight.vue";
export default {
  components: {
    PostAside,
    PostRight
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
    // z-index: 666;
    // border: 1px solid #ddd;
    float: left;
  }
  .post-right {
    // position: absolute;
    float: right;
    // top: 0px;
    // left: 260px;
    // width: 700px;
  }
}
//   双伪元素清除浮动
.clearfix::before,
.clearfix::after {
  content: "";
  display: table;
}

.clearfix::after {
  clear: both;
}
</style>