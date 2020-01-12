<template>
  <div class="postRight clearfix">
    <el-input v-model="input" placeholder="请输入想去的地方，比如：'广州'" class="search">
      <i class="el-icon-search" slot="suffix"></i>
    </el-input>
    <div class="tui_jian clearfix">
      <dl>
        <dt>推荐：</dt>
        <dd>
          <a href="#">广州</a>
        </dd>
        <dd>
          <a href="#">上海</a>
        </dd>
        <dd>
          <a href="#">北京</a>
        </dd>
      </dl>
    </div>
    <div class="gong_lue clearfix">
      <div class="left">推荐攻略</div>
      <div class="right">
        <el-button type="primary" icon="el-icon-edit">写游记</el-button>
      </div>
    </div>
    <div class="articleList clearfix">
      <ArticleBlock v-for="(item,index) in articleList" :key="index" :articleList="item"></ArticleBlock>
    </div>
  </div>
</template>

<script>
import ArticleBlock from "@/components/post/ArticleBlock.vue";
export default {
  components: {
    ArticleBlock
  },
  data() {
    return {
      input: "",
      articleList:[]
    };
  },
  mounted() {
    this.$axios({
      url: "/posts"
    }).then(res => {
    //   console.log(res);
      this.articleList =res.data.data;
      // console.log(this.articleList)
    });
  }
};
</script>

<style lang="less" scoped>
.postRight {
  margin-left: 40px;
  width: 700px;
  .search {
    width: 100%;
    box-sizing: border-box;
    height: 40px;
    line-height: 40px;
    border: 3px solid orange;
  }
  /deep/.el-input__inner {
    height: 100%;
    line-height: 100%;
    width: 100%;
    border: none;
    padding: 0px 10px;
    box-sizing: border-box;
    // background: red;
  }
  .tui_jian {
    padding: 10px 0px;
    font-size: 12px;
    dt {
      float: left;
      color: #666;
    }
    dd {
      float: left;
      margin-left: 10px;
      color: #666;
    }
  }
  .gong_lue .left {
    float: left;
    font-weight: 400;
    font-size: 18px;
    color: orange;
    border-bottom: 1px solid orange;
    padding: 0 0 10px 0;
    height: 40px;
    line-height: 40px;
  }
  .gong_lue .right {
    float: right;
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