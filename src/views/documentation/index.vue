<template>
  <div class="app-container documentation-container">
    <!-- <a class="document-btn" target="_blank" href="https://store.akveo.com/products/vue-java-admin-dashboard-spring?utm_campaign=akveo_store-Vue-Vue_demo%2Fgithub&utm_source=vue_admin&utm_medium=referral&utm_content=demo_English_button">Java backend integration</a> -->
    <!-- <a class="document-btn" target="_blank" href="https://panjiachen.github.io/vue-element-admin-site/">Documentation</a> -->
    <!-- <a class="document-btn" target="_blank" href="https://github.com/PanJiaChen/vue-element-admin/">Github Repository</a> -->
    <!-- <a class="document-btn" target="_blank" href="https://panjiachen.gitee.io/vue-element-admin-site/zh/">国内文档</a> -->
    <!-- <dropdown-menu class="document-btn" :items="articleList" title="系列文章" /> -->
    <!-- <a class="document-btn" target="_blank" href="https://panjiachen.github.io/vue-element-admin-site/zh/job/">内推招聘</a> -->
    <el-table :data="dataList" style="width: 100%;" size="small" border show-header>
        <el-table-column label="序号" width="140" prop="num" v-model="dataList.num"></el-table-column>
        <el-table-column label="名称" width="120">
            <!-- 关键代码 -->
            <template slot-scope="scope">
                <el-input v-if="scope.row.isnameSelected" v-model="scope.row.name"
                    @focus="focusEvent(scope.row,scope.$index,scope.column)"
                    @blur="blurEvent(scope.row,scope.$index,scope.column)" v-focus></el-input>
                <p @click="cellClick(scope.row, scope.column)" v-else>{{scope.row.name}}</p>
            </template>
        </el-table-column>
        <el-table-column label="年龄" width="120">
            <!-- 通过isageSelected显示或隐藏 -->
            <template slot-scope="scope">
                <el-input v-if="scope.row.isageSelected" v-model="scope.row.age"
                    @focus="focusEvent(scope.row,scope.$index,scope.column)"
                    @blur="blurEvent(scope.row,scope.$index,scope.column)" v-focus></el-input>
                <p @click="cellClick(scope.row, scope.column)" v-else>{{scope.row.age}}</p>
            </template>
        </el-table-column>
        <el-table-column label="金额" width="120">
            <template slot-scope="scope">
                <!-- 通过issalSelected显示或隐藏 -->
                <el-input v-if="scope.row.issalSelected" v-model="scope.row.money"
                    @focus="focusEvent(scope.row,scope.$index,scope.column)"
                    @blur="blurEvent(scope.row,scope.$index,scope.column)" v-focus></el-input>
                <p @click="cellClick(scope.row, scope.column)" v-else>{{scope.row.money}}</p>
            </template>
        </el-table-column>
    </el-table>
    <el-table :data="tableList" size='mini' border show-header style="width:100%" row-key="countryCode" :expand-row-keys="expands">
        <el-table-column type="expand" width="1"></el-table-column>
        <el-table-column label="国家" align='center'>
            <template slot-scope="scope">
                        <span style='cursor: pointer;color: #4784C4;' @click="applyAllClick(scope.row,scope.row.countryCode)">国家</span>
                    </template>
                    <template slot-scope="scope">
                        <div style="cursor: pointer;" >
                            <div style="float: left;">{{scope.row.countryName}}</div>
                            <div style="float: right;color: #666666;">
                                <span v-if="scope.row.expandStatus" class="iconfont zby-arrow-down"></span>
                                <span v-else class="iconfont zby-arrow-up"></span>
                            </div>
                            <div class="clearfix"></div>
                        </div>
                    </template>
        </el-table-column>
        <el-table-column align='center' width="445">
            <template slot="header" slot-scope="scope">
                <div style="width: 445px;line-height: 20px;margin-left: 20px;">
                    <span>运费</span>
                </div>
            </template>
            <template slot-scope="scope">
                <span>
                    <span style="font-size: 0;">
                        <el-input size="mini" class="input80Style" placeholder="" clearable v-model="scope.row.price" @keyup.native="inputNumKeyUp('price',scope.row.price,scope.row.countryCode)"></el-input>
                        <el-input size="mini" class="input55Style" placeholder="" v-model="scope.row.price" disabled></el-input>
                    </span>
                </span>
            </template>
        </el-table-column>
        <el-table-column label="最长妥投天数" align='center' width='125'>
            <template slot-scope="scope">
                <el-input size="mini" placeholder="" v-model="scope.row.maxDeliveryDays"></el-input>
            </template>
        </el-table-column>
        <el-table-column label="启用国家/地区" align='center' width='100'>
            <template slot-scope="scope">
                <el-checkbox v-model="scope.row.isEnabled"></el-checkbox>
            </template>
        </el-table-column>
        <el-table-column label="操作" align='center'>
            <template slot-scope="scope">
                <span style='cursor: pointer;color: #4784C4;' @click="applyAllClick(scope.row,scope.row.countryCode)">应用给所有国家/地区</span>
            </template>
        </el-table-column>
    </el-table>
  </div>
</template>
<script>
import DropdownMenu from '@/components/Share/DropdownMenu'
export default {
  name: 'Documentation',
  components: { DropdownMenu },
  data() {
    return {
        // 需要展示的数据，模拟从接口或组件传递过来的值
    dataList: [
        { name: "测试1", age: 24, num: 10010, money: "1200" },
        { name: "测试2", age: 24, num: 10011, money: "1200" },
        { name: "测试3", age: 24, num: 10012, money: "1200" },
        { name: "测试4", age: 24, num: 10013, money: "1200" }
    ],
        expands:[],
        tableList:[{
            warehouseId: "5a277fc5ef7b897f2d5fb3ce",
            warehouseName: "UK",
            shippingList:[{
                countryName: "英国",
                currencyCode: "CNY",
                destination: "GB",
                id: 63,
                isEnabled: true,
                maxDeliveryDays: 2,
                price: 20,
                stateShippingList:[]
            },{
                warehouseId: "59f169906fa88cf16281e66c",
                warehouseName: "EXPRESS-US",
                shippingList:[{
                    countryName: "美国",
                    currencyCode: "CNY",
                    destination: "US",
                    id: 64,
                    isEnabled: true,
                    maxDeliveryDays: 3,
                    price: 21,
                    stateShippingList:[{
                        currencyCode: "CNY",
                        destination: "MO",
                        id: 158,
                        isEnabled: true,
                        maxDeliveryDays: 5,
                        price: 22,
                        state: "Missouri"
                    },{
                        currencyCode: "CNY",
                        destination: "PA",
                        id: 159,
                        isEnabled: true,
                        maxDeliveryDays: 3,
                        price: 21,
                        state: "Pennsylvania"
                    },{
                        currencyCode: "CNY",
                        destination: "NV",
                        id: 160,
                        isEnabled: true,
                        maxDeliveryDays: 3,
                        price: 21,
                        state: "Nevada"
                    },{
                        currencyCode: "CNY",
                        destination: "NE",
                        id: 161,
                        isEnabled: true,
                        maxDeliveryDays: 3,
                        price: 21,
                        state: "Nebraska"
                    },{
                        currencyCode: "CNY",
                        destination: "NH",
                        id: 162,
                        isEnabled: true,
                        maxDeliveryDays: 3,
                        price: 21,
                        state: "New Hampshire" 
                    },{
                        currencyCode: "CNY",
                        destination: "AP",
                        id: 163,
                        isEnabled: true,
                        maxDeliveryDays: 2,
                        price: 23,
                        state: "AP"
                    }]
                }]
            }]
        },{
            warehouseId: "5a2e402ce62bbc058738e277",
            warehouseName: "FRANCE",
            shippingList:[{
                countryName: "法国",
                currencyCode: "CNY",
                destination: "FR",
                id: 62,
                isEnabled: true,
                maxDeliveryDays: 7,
                price: 27,
                stateShippingList:[{
                    currencyCode: "CNY",
                    destination: "YT",
                    id: 148,
                    isEnabled: false,
                    maxDeliveryDays: 7,
                    price: 27,
                    state: "Mayotte"
                },{
                    currencyCode: "CNY",
                    destination: "GF",
                    id: 149,
                    isEnabled: false,
                    maxDeliveryDays: 7,
                    price: 27,
                    state: "French Guiana"
                },{
                    currencyCode: "CNY",
                    destination: "PF",
                    id: 150,
                    isEnabled: false,
                    maxDeliveryDays: 7,
                    price: 27,
                    state: "French Polynesia" 
                },{
                    currencyCode: "CNY",
                    destination: "WF",
                    id: 151,
                    isEnabled: false,
                    maxDeliveryDays: 7,
                    price: 27,
                    state: "Wallis and Futuna"
                },{
                    currencyCode: "CNY",
                    destination: "GP",
                    id: 152,
                    isEnabled: true,
                    maxDeliveryDays: 5,
                    price: 22,
                    state: "Guadeloupe"
                },{
                    currencyCode: "CNY",
                    destination: "PM",
                    id: 153,
                    isEnabled: false,
                    maxDeliveryDays: 7,
                    price: 27,
                    state: "Saint Pierre and Miquelon"
                },{
                    currencyCode: "CNY",
                    destination: "RE",
                    id: 154,
                    isEnabled: false,
                    maxDeliveryDays: 7,
                    price: 27,
                    state: "Reunion"
                },{
                    currencyCode: "CNY",
                    destination: "NC",
                    id: 155,
                    isEnabled: false,
                    maxDeliveryDays: 7,
                    price: 27,
                    state: "New Caledonia"
                },{
                    currencyCode: "CNY",
                    destination: "MF",
                    id: 157,
                    isEnabled: true,
                    maxDeliveryDays: 2,
                    price: 26.5,
                    state: "Saint Martin"
                }]
            }]
        }],
      articleList: [
        { title: '基础篇', href: 'https://juejin.im/post/59097cd7a22b9d0065fb61d2' },
        { title: '登录权限篇', href: 'https://juejin.im/post/591aa14f570c35006961acac' },
        { title: '实战篇', href: 'https://juejin.im/post/593121aa0ce4630057f70d35' },
        { title: 'vue-admin-template 篇', href: 'https://juejin.im/post/595b4d776fb9a06bbe7dba56' },
        { title: 'v4.0 篇', href: 'https://juejin.im/post/5c92ff94f265da6128275a85' },
        { title: '自行封装 component', href: 'https://segmentfault.com/a/1190000009090836' },
        { title: '优雅的使用 icon', href: 'https://juejin.im/post/59bb864b5188257e7a427c09' },
        { title: 'webpack4（上）', href: 'https://juejin.im/post/59bb864b5188257e7a427c09' },
        { title: 'webpack4（下）', href: 'https://juejin.im/post/5b5d6d6f6fb9a04fea58aabc' }
      ]
    }
  },
  //自定义指令
directives: {
    focus: {
        inserted: function (el) {
            el.querySelector('input').focus()
        }
    }
},
created() {
    this.getList()
},
  methods:{
      applyAllClick(row,culm){
          console.log('aa');
          console.log('goods');
      },
      //请求接口
      getList() {
            //遍历，给每项数据添加上某列是否被选中的flag，需要改成可修改的列数都要添加flag，且与上面v-if的一致
            this.dataList = this.dataList.map((item) => {
                return { ...item, isnameSelected: false, isageSelected: false, issalSelected: false }
            });
      },
      //点击文本触发，显示input框，隐藏p标签
    cellClick(row, column) {
        if (column.label == "名称") {
            row.isnameSelected = !row.isnameSelected
        } else if (column.label == "年龄") {
            row.isageSelected = !row.isageSelected
        } else if (column.label == "金额") {
            row.issalSelected = !row.issalSelected
        }
    },
    //点击输入框聚焦，存储当前值
    focusEvent(row, index, column) {
        if (column.label == "名称") {
            row.oldName = row.name
        } else if (column.label == "年龄") {
            row.oldAge = row.age
        } else if (column.label == "金额") {
            row.oldSal = row.money
        }
    },
    //输入框失去焦点触发,此处用提示框提示修改
                blurEvent(row, curIndex, column) {
                    if (column.label == "名称") {
                        row.isnameSelected = !row.isnameSelected
                        if (row.name !== row.oldName) {
                            this.$message({
                                message: '修改成功',
                                type: 'success',
                                duration: 1000
                            })
                        }
                    } else if (column.label == "年龄") {
                        row.isageSelected = !row.isageSelected
                        if (row.age !== row.oldAge) {
                            this.$message({
                                message: '修改成功',
                                type: 'success',
                                duration: 1000
                            })
                        }
                    } else if (column.label == "金额") {
                        row.issalSelected = !row.issalSelected
                        if (row.money !== row.oldSal) {
                            this.$message({
                                message: '修改成功',
                                type: 'success',
                                duration: 1000
                            })
                        }
                    }
                },
  }
}
</script>

<style lang="scss" scoped>
.documentation-container {
  margin: 50px;
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;

  .document-btn {
    flex-shrink: 0;
    display: block;
    cursor: pointer;
    background: black;
    color: white;
    height: 60px;
    padding: 0 16px;
    margin: 16px;
    line-height: 60px;
    font-size: 20px;
    text-align: center;
  }
}
</style>
