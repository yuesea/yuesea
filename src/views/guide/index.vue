<template>
  <div class="app-container">
    <aside>
      The guide page is useful for some people who entered the project for the first time. You can briefly introduce the
      features of the project. Demo is based on
      <a href="https://github.com/kamranahmedse/driver.js" target="_blank">driver.js.</a>
    </aside>
    <el-button icon="el-icon-question" type="primary" @click.prevent.stop="guide">
      Show Guide
    </el-button>
    <div>
        <el-table :data="tableData" border style="width: 100%;margin-top:30px;" size='mini'>
            <el-table-column prop="date" label="日期" width="180"></el-table-column>
            <el-table-column prop="name" label="姓名" width="180"></el-table-column>
            <el-table-column prop="address" label="地址"></el-table-column>
            <el-table-column  label="操作" width="100">
                <el-button type="text" @click="downLoads">下载</el-button>
            </el-table-column>
        </el-table>
    </div>
  </div>
</template>
<script>
import Driver from 'driver.js' // import driver.js
import 'driver.js/dist/driver.min.css' // import driver.js css
import steps from './steps'
export default {
  name: 'Guide',
  data() {
    return {
      driver: null,
       tableData: [{
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1517 弄'
        }, {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }]
    }
  },
  mounted() {
    this.driver = new Driver()
  },
  methods: {
    downLoads(){
        console.log('下载');
    },
    guide() {
      this.driver.defineSteps(steps)
      this.driver.start()
    },
    selChange(val){
      console.log(val);
     var str = this.value;
     this.value = this.options[0]
     this.options = [];
     this.options.push(str)
     // this.options[0] = str;

    }
  }
}

</script>
<style>
  p{
    width:100px;
    border:1px solid pink;
    height:30px;
    text-align:center;
    line-height:30px;
    cursor:pointer;
    }
</style>
