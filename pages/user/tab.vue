<template>
  <div class="tab">
    <div class="header">
      <div>
          <span v-for="(item,index) in news" :key="index" @click="handleClick(index)">{{item}}</span>
      </div>
      <ul v-if="current===0">
        <li>新闻1</li>
        <li>新闻2</li>
        <li>新闻3</li>
      </ul>
      <ul v-if="current===1">
        <li>头条1</li>
        <li>头条2</li>
        <li>头条3</li>
      </ul>
      <ul v-if="current===2">
        <li>娱乐1</li>
        <li>娱乐2</li>
        <li>娱乐3</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      news: ["新闻", "头条", "娱乐"],
      current: 0
    };
  },
  methods: {
    handleClick(index) {
      this.current = index;
    }
  }
};
</script>

<style scoped lang="less">
*{
    margin: 0;
    padding: 0;
}
.header{
    margin: 100px 0 0 100px;
}
span{
    padding: 10px;
}
ul li{
    list-style: none;
    margin-top: 20px;
}
.blue{
   background-color: blue;
}
</style>