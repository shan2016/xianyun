<template>
  <div class="clearfix">
    <div class="single1 clearfix" v-if="articleList.images.length>2">
      <p class="title" style="padding: 10px 0px;font-size:18px;">{{articleList.title}}</p>
      <p class="summary">{{articleList.summary}}</p>
      <div class="imgs clearfix">
        <div class="img_small" v-for="(item,index) in images" :key="index">
          <img :src="item" alt />
        </div>
      </div>
      <p class="info">
        <i class="el-icon-location-outline"></i>
        <span>{{articleList.cityName}}</span>
        by
        <img
          :src="'http://localhost:1337'+articleList.account.defaultAvatar"
          alt
          class="tou_xiang"
        />
        {{articleList.account.nickname}}
        <i class="el-icon-view"></i>
        <span>{{articleList.watch}}</span>
        <span v-if="articleList.like===null">0赞</span>
        <span v-else>{{articleList.like}}赞</span>
      </p>
    </div>
    <div class="single2 clearfix" v-else-if="articleList.images.length===0">
      <div class="right">
        <p class="title" style="padding: 10px 0px;font-size:18px;">{{articleList.title}}</p>
        <p class="summary">{{articleList.summary}}</p>
        <p class="info">
          <i class="el-icon-location-outline"></i>
          <span>{{articleList.cityName}}</span>
          by
          <img
            :src="'http://localhost:1337'+articleList.account.defaultAvatar"
            alt
            class="tou_xiang"
          />
          {{articleList.account.nickname}}
          <i class="el-icon-view"></i>
          <span>{{articleList.watch}}</span>
          <span v-if="articleList.like===null">0赞</span>
          <span v-else>{{articleList.like}}赞</span>
        </p>
      </div>
    </div>
    <div class="single3 clearfix" v-else>
      <div class="imgs clearfix">
        <img :src="images[0]" alt />
      </div>
      <div class="right">
        <p class="title" style="padding: 10px 0px;font-size:18px;">{{articleList.title}}</p>
        <p class="summary">{{articleList.summary}}</p>
        <p class="info">
          <i class="el-icon-location-outline"></i>
          <span>{{articleList.cityName}}</span>
          by
          <img
            :src="'http://localhost:1337'+articleList.account.defaultAvatar"
            alt
            class="tou_xiang"
          />
          {{articleList.account.nickname}}
          <i class="el-icon-view"></i>
          <span>{{articleList.watch}}</span>
          <span v-if="articleList.like===null">0赞</span>
          <span v-else>{{articleList.like}}赞</span>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    articleList: {
      type: Object,
      default: {}
    }
  },
  data() {
    return {
      images: []
    };
  },
  mounted() {
    console.log(this.articleList);
    this.images = this.articleList.images;
    if (this.images.length > 3) {
      this.images = this.images.slice(0, 3);
    }
  }
};
</script>

<style lang="less" scoped>
.img_small {
  width: 220px;
  height: 150px;
  float: left;
  margin-right: 20px;
  img {
    height: 100%;
    width: 100%;
  }
}
.img_small:nth-child(3) {
  margin-right: 0px;
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
.summary {
  margin-bottom: 15px;
  line-height: 1.5;
  font-size: 14px;
  height: 63px;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 3;
}
.tou_xiang {
  width: 16px;
  height: 16px;
}
.single3 {
  .imgs {
    float: left;
    width: 220px;
    height: 150px;
    img {
      height: 100%;
      width: 100%;
    }
  }
  .right {
    float: left;
    width: 470px;
    margin-left: 10px;
    .title {
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }
  }
}
.single2{
  width: 700px;
  .title {
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }
}
</style>