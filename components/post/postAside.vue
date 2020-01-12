<template>
  <div class="postAside">
    <div class="top" 
        @mouseleave="handleleave">
      <div
        class="citiesList"
        v-for="(item,index) in typeList"
        :key="index"
        @mouseenter="handleCitiesList(index)"
      >
        {{item.type}}
        <i class="el-icon-arrow-right"></i>
      </div>

      <div class="children" v-show="show">
        <div class="childrenList" v-for="(item,index) in children" :key="index">
          <i>{{index+1}}</i>
          <strong>{{item.city}}</strong>
          <nuxt-link to="#" class="linklist">{{item.desc}}</nuxt-link>
        </div>
      </div>
    </div>
    <div class="tuijian">
      <p>推荐城市</p>
      <nuxt-link to="#">
        <img src="@/images/pic_sea.jpeg" alt />
      </nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      typeList: [],
      currentTab: 0,
      children: [],
      show: false,
      show2: false
    };
  },
  mounted() {
    this.$axios({
      url: "/posts/cities"
    }).then(res => {
      this.typeList = res.data.data;
      // console.log(this.typeList);
      // this.children = this.typeList[this.currentTab].children;
    });
  },
  methods: {
    //鼠标移入时候显示
    handleCitiesList(index) {
      this.currentTab = index;
      this.children = this.typeList[this.currentTab].children;
      this.show = true;
    },
    //鼠标移出时候显示
    handleleave() {
      this.show = false;
    },
  }
};
</script>

<style lang="less" scoped>
.postAside {
  .citiesList {
    height: 40px;
    line-height: 40px;
    border-bottom: 1px solid #ddd;
    border-left: 1px solid #ddd;
    border-right: 1px solid #ddd;
    padding: 0 20px;
    font-size: 14px;
    position: relative;
    > i {
      float: right;
      line-height: 40px;
      color: #999;
    }
  }
  .citiesList:nth-child(1) {
    border-top: 1px solid #ddd;
  }
  .citiesList:hover {
    color: orange;
    i {
      color: orange;
    }
    border-right: 1px solid #fff;
    z-index: 999;
  }

  .tuijian {
    margin-top: 20px;
    p {
      padding: 0 0 10px 0;
      border-bottom: 1px solid #ddd;
      margin-bottom: 10px;
    }
    img {
      width: 260px;
    }
  }
}
.children {
  background: #fff;
  position: absolute;
  left: 259px;
  top: 0px;
  width: 308px;
  padding: 10px 20px;
  border: 1px solid #ddd;
  z-index: 999;
  // display: none;
  .childrenList {
    // display: none;
    height: 36px;
    line-height: 36px;
    font-size: 14px;
    i {
      color: orange;
      font-size: 24px;
      font-style: italic;
    }
    strong {
      color: orange;
      margin: 0 10px;
      font-weight: 400;
    }
    .linklist {
      color: #999;
    }
  }
}
</style>