<template>
    <div class="filters">
        <el-row type="flex" class="filters-top" justify="space-between" align="middle">
            <el-col :span="8">
                单程： 
                {{data.info.departCity}} - {{data.info.destCity}} 
                / 
                {{data.info.departDate}}
            </el-col>
            <el-col :span="4">
                <el-select size="mini" v-model="airport" placeholder="起飞机场" >
                    <el-option
                    v-for="(item,index) in data.options.airport"
                    :key="index"
                    :label="item"
                    :value="item"
                    >
                    </el-option>
                </el-select>
            </el-col>
            <el-col :span="4">
                <el-select size="mini" v-model="flightTimes"  placeholder="起飞时间" >
                    <el-option
                    v-for="(item, index) in data.options.flightTimes"
                    :key="index"
                    :label="`${item.from}:00 - ${item.to}:00`"
                    :value="`${item.from},${item.to}`"
                    >
                    </el-option>
                </el-select>
            </el-col>
            <el-col :span="4">
                <el-select size="mini" v-model="company"  placeholder="航空公司" >
                    <el-option
                    v-for="(item, index) in data.options.company"
                    :key="index"
                    :label="item"
                    :value="item">
                    </el-option>
                </el-select>
            </el-col>
            <el-col :span="4">
                <el-select size="mini" v-model="airSize" placeholder="机型" >
                    <el-option
                    v-for="(item, index) in sizeOptions"
                    :key="index"
                    :label="item.name"
                    :value="item.size">
                    </el-option>
                </el-select>
            </el-col>
        </el-row>
        <div class="filter-cancel">
            筛选：
            <el-button 
                       type="primary" 
                       round 
                       plain 
                       size="mini" 
                       @click="handleFiltersCancel">
                撤销
    		</el-button>
        </div>
        <!-- 随便调用为了函数可以执行 -->
        <span>{{filterData}}</span>
    </div>
</template>

<script>
export default {
    props: {
        data:{
            type:Object,
            default(){return {}}
        }
    },
    data(){
        return {
            airport: "",        // 机场
            flightTimes: "",    // 出发时间
            company: "",        // 航空公司
            airSize: "",
           sizeOptions:[
                {name:"大",size:"L"},
                {name:"中",size:"M"},
                {name:"小",size:"S"},
            ]        // 机型大小
        }
    },
    computed: {
        filterData(){
            const arr =this.data.flights.filter(item=>{
                let valid=true;
                if(this.airport && item.org_airport_name !==this.airport){
                    valid=false;
                }
                if(this.flightTimes){
                   const [from,to]=this.flightTimes.split(",");
                const start = +item.dep_time.split(":")[0];
                if(start < from ||start>= +to) {
                    valid=false;
                }
                }
                if(this.company && item.airline_name !== this.company){
                    valid = false;
                }

                if(this.airSize && item.plane_size !== this.airSize){
                    valid = false;
                }
                return valid;
            })
            this.$emit("setDataList",arr);
            // 为了页面渲染空的字符串
            return "";
        }
    },
    mounted () {
        // console.log(this.data)
    },
    methods: {
        // 选择机场时候触发
        // handleAirport(value){
        //     // console.log(this.data)
        //     const arr = this.data.flights.filter(v=>{
        //         v.org_airport_name===value
        //         return value;
        //     });
        //     // console.log(arr)
        //     this.$emit("setDataList",arr);
        // },

        // // 选择出发时间时候触发
        // handleFlightTimes(value){
        //     const [from,to]=value.split(",");
        //     const arr = this.data.flights.filter(v=>{
        //         const start = +v.dep_time.split(":")[0];
        //         return start >= from &&start < +to;
        //     })
        //     this.$emit("setDataList",arr);
        // },

        //  // 选择航空公司时候触发
        // handleCompany(value){
        //     const arr = this.data.flights.filter(v => 
        //         v.airline_name === value
        //     );

        //     this.$emit("setDataList", arr);
        // },

        //  // 选择机型时候触发
        // handleAirSize(value){
        //    const arr = this.data.flights.filter(v => 
        //         v.plane_size === value
        //     );

        //     this.$emit("setDataList", arr);
        // },
        
        // 撤销条件时候触发
        handleFiltersCancel(){
            this.airport = "";
            this.flightTimes = "";
            this.company = "";
            this.airSize = "";
            
            this.$emit("setDataList", this.data.flights);
        },
    }
}
</script>

<style scoped lang="less">
    .filters{
        margin-bottom:20px;
    }

    .filters-top{
        > div{
            /deep/ .el-select{
                margin-left:10px;
            }
        }
    }

    .filter-cancel{
        margin-top:10px;
    }
</style>