<template>
  <div class="app-container mainPage">
    <div class="basicContent whiteContet">
      <div>                
          <h5 style="padding-left:24px;padding-top:14px;margin-bottom:14px;color:#303133;">员工信息</h5>
      </div>
      <el-row>
          <el-col :span='24'>
              <div style="width:100%;height:0;border-bottom: #E1E1E1 1px dashed;margin-bottom:8px;"></div>
          </el-col>
      </el-row>
      <div>
        <el-row>
          <el-form style="padding-left:20px;" :model="queryData" :label-position="labelPosition" :rules="UserFormRole" ref="FormRole">
            <el-row>
              <el-col :span="21">
                <el-row>
                  <el-col :span="8">
                    <el-form-item label="姓名：" prop="name">
                        <el-input class="miniInput" maxlength="100" id="roleCode" v-model="queryData.name" size="mini" placeholder="请输入员工姓名" clearable></el-input>
                    </el-form-item>
                  </el-col>
                  <el-col :span="8">
                      <el-form-item label="联系电话：" prop="mobile">
                          <el-input class="miniInput" maxlength="100" id="roleCode" v-model="queryData.mobile" size="mini" placeholder="请输入" clearable></el-input>
                      </el-form-item>
                  </el-col>
                </el-row>
                <el-row>
                    <el-col :span='8'>
                        <el-form-item label="档案号：" prop="archiveNumber">
                            <el-input class="miniInput" maxlength="100" id="roleCode" v-model="queryData.archiveNumber" size="mini" placeholder="请输入存档编号" clearable></el-input>
                        </el-form-item> 
                    </el-col>
                    <el-col :span='8'>
                        <el-form-item label="员工类型：" prop="type">                           
                            <span v-for="(item,index) in staffStautsList" @click="iconSel(item,index)" :key="item.type" :value="item.type" :class='index==isactive2?classVal:classVal2' style="display:inline-block;width:50px;height:30px;border-radius:3px;text-align:center;line-height:30px;cursor:pointer;margin-left:0px;margin-right:10px">{{item.typeText}}</span> 
                        </el-form-item>
                    </el-col>
                </el-row>
              </el-col>
            </el-row>
          </el-form>
        </el-row>
      </div>
    </div>
  </div>
</template>
<script>
import path from 'path'
import { deepClone } from '@/utils'
import { getRoutes, getRoles, addRole, deleteRole, updateRole } from '@/api/role'

const defaultRole = {
  key: '',
  name: '',
  description: '',
  routes: []
}

export default {
  data() {
    return {
      staffStautsList:[{
        type:0,
        typeText:"待入职"
      },{
        type:0,
        typeText:"正式"
      },{
        type:0,
        typeText:"试用"
      },{
        type:0,
        typeText:"临时"
      }],
      classVal:"styleFont",
      classVal2:"defaultFont",
      classVal3:"defaultFont",
      isactive2:0,// 控制弹框中的奖惩处罚的选项
      queryData:{},
      labelPosition:"right",
      UserFormRole:{

      },
      role: Object.assign({}, defaultRole),
      routes: [],
      rolesList: [],
      dialogVisible: false,
      dialogType: 'new',
      checkStrictly: false,
      defaultProps: {
        children: 'children',
        label: 'title'
      }
    }
  },
  computed: {
    
  },
  created() {
    
  },
  methods: {
    
  }
}
</script>

<style lang="scss" scoped>
.app-container {
  .roles-table {
    // margin-top: 30px;
  }
  background-color: #ccc;
  .permission-tree {
    // margin-bottom: 30px;
  }
}
 .el-form-item__error{
        top:92%;
        left:127px;
    }
.el-cascader--mini{
      width:80%;
  }
    .titleSize{
        font-size: 14px;
        font-weight: bold;
        color: #333333;
    }
 .el-button--primary>span{
      color:#ffffff !important;
  }
 .is-plain>span{
        color:#31D9A4 !important;
    }
    .el-form-item__label{
        width:125px !important;
    }    
    .defaultFont{
        color:#31D9A4;
        background:#D6F7ED;
    }
    .editPersonDialog .el-row .el-col{
        height:46px;
    }
    .bgPage{
        background:#F2F2F2;
        padding-top:1px;
        padding-bottom:1px;
    }
    .whiteContet{
        margin-left:16px;
        margin-right:16px;
        background:#FFFFFF;
        margin-top:16px;
        margin-bottom:16px;
        border-radius: 10px;
    } 
     .el-form-item__label{
             width:120px;              
    }
     .footerBottom{
        margin-top:23px;
        margin-left:11px;
    }
    .footerBottom button{
        margin-bottom:22px;
    }
   .listContent{
        margin-left:120px;
   }
    .el-form-item {
         margin-bottom:10px;
    }
     .tableContent {
      margin-left: 17px;
      margin-right: 17px;
  }
.listContent p{
    margin:0px;
}
 .el-form-item__label{
  color:#303133 !important;
}
 span{
  color:#303133 !important;
}
 p{
  color:#303133 !important;
}

 h5,.jobTxt{
  color:#303133;
}
.el-textarea{
    width:80%;
}
 .styleFont{
    color:#fff;
    background:#31D9A4;
}
 .el-button--primary.is-plain:hover{
    background:#EAFBF6;
}

</style>
