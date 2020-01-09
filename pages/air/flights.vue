<template>
  <section class="contianer">
    <el-row type="flex" justify="space-between">
      <!-- 顶部过滤列表 -->
      <div class="flights-content">
        <!-- 过滤条件 -->
        <FlightsFilters :data="cacheFlightsData" @setDataList="setDataList"></FlightsFilters>

        <!-- 航班头部布局 -->
        <FlightsListHead></FlightsListHead>

        <!-- 航班信息 -->
        <div>
          <FlightsItem v-for="(item,index) in dataList" :key="index" :data="item"></FlightsItem>
        </div>
        <el-row type="flex" justify="center" style="margin-top:10px;">
          <!-- size-change：切换条数时候触发 -->
          <!-- current-change：选择页数时候触发 -->
          <!-- current-page: 当前页数 -->
          <!-- page-size：当前条数 -->
          <!-- total：总条数 -->
          <el-pagination
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
            :current-page="pageIndex"
            :page-sizes="[5, 10, 15, 20]"
            :page-size="pageSize"
            layout="total, sizes, prev, pager, next, jumper"
            :total="flightsData.total"
          ></el-pagination>
        </el-row>
      </div>
      <!-- <span>{{a}}</span> -->
      <!-- 侧边栏 -->
      <div class="aside">
        <!-- 侧边栏组件 -->
        <FlightsAside />
      </div>
    </el-row>
  </section>
</template>

<script>
import moment from "moment";
import FlightsListHead from "@/components/air/flightsListHead.vue";
import FlightsItem from "@/components/air/flightsItem.vue";
import FlightsFilters from "@/components/air/flightsFilters.vue";
import FlightsAside from "@/components/air/flightsAside.vue";
export default {
  data() {
    return {
      // 航班总数据
      flightsData: {
        flights: [], //航班总列表
        info: {},
        options: {}
      },
      // dataList: [], // 航班列表数据，用于循环flightsItem组件，单独出来是因为要分页
      pageIndex: 1, // 当前页数
      pageSize: 5, // 显示条数
      cacheFlightsData: {
        flights: [],
        info: {},
        options: {}
      }
    };
  },
  components: {
    FlightsListHead,
    FlightsItem,
    FlightsFilters,
    FlightsAside
  },
  methods: {
    getData() {
      this.$axios({
        url: `airs`,
        params: this.$route.query
      }).then(res => {
        this.flightsData = res.data;
        this.cacheFlightsData = { ...res.data };
        // this.dataList = this.flightsData.flights;
        // this.setDataList(); //初始化dataList数据，获取1 - 10条
      });
    },
    setDataList(arr) {
      if (arr) {
        this.pageIndex = 1;
        this.flightsData.flights = arr;
        this.flightsData.total = arr.length;
      }
    },
    // 切换条数时触发
    handleSizeChange(value) {
      this.pageSize = value;
      this.pageIndex = 1;
      // this.setDataList();
    },
    // 切换页数时触发
    handleCurrentChange(value) {
      // console.log(value);
      this.pageIndex = value;
      // console.log(this.pageIndex)
      // this.setDataList();
    }
  },
  mounted() {
    this.getData();
  },
  watch: {
    $route() {
      this.getData();
    }
  },
  computed: {
    //他必须被调用
    dataList() {
      // this.pageIndex = 1;
      const start = (this.pageIndex - 1) * this.pageSize;
      const end = start + this.pageSize;
        // console.log(this.flightsData.flights.slice(start, end));
      return this.flightsData.flights.slice(start, end);
    }
  }
};
</script>

<style scoped lang="less">
.contianer {
  width: 1000px;
  margin: 20px auto;
}

.flights-content {
  width: 745px;
  font-size: 14px;
}

.aside {
  width: 240px;
}
</style>