<template>
  <div @click="$emit('makeCla')">
    <el-breadcrumb separator-class="el-icon-arrow-right" class="mb-5">
    <el-breadcrumb-item>首页</el-breadcrumb-item>
    <el-breadcrumb-item>部落管理</el-breadcrumb-item>
    <el-breadcrumb-item>副首管理</el-breadcrumb-item>
    </el-breadcrumb>   
 <el-alert
    title="您的身份不是超级管理员, 无法对页面进行修改"
    type="warning"
    show-icon :closable="false" v-if="loginUser.isAdmin<2">
  </el-alert>
    <el-row class="mt-4">
        <el-col :span="6" :offset="15">
          <el-button icon="el-icon-plus" @click="dialogFormVisible = true" type="primary" :disabled="loginUser.isAdmin<2">
          添加副手</el-button></el-col>
        
    </el-row>
    <div class="mt-10">
      <div v-for="(item, index) in dataList" :key='index' c>

      <div class="border-l-8 border-blue-400 pl-1 mt-8 mb-3">{{clanName[index]}}</div>

      <el-table  :show-header="false" :row-class-name="tableRowClassName" class="text-center" :data="dataList[index]"  style="width: 100%">
          <el-table-column min-width="120px" prop="admin_name" label="村庄名">
          </el-table-column>
          
          <el-table-column min-width="120px" :formatter="tFormatter" prop="rank" label="职序">
          </el-table-column>
          <el-table-column label="操作">
            <template slot-scope="scope">
              <el-button 
                size="mini"
                @click="handleEdit(scope.$index, scope.row)" :disabled="loginUser.isAdmin<2">编辑</el-button>
              <el-button
                size="mini"
                type="danger"
                @click="handleDelete(scope.$index, scope.row)" :disabled="loginUser.isAdmin<2">删除</el-button>
            </template>
          </el-table-column>
      </el-table>
      </div>

    </div>
<el-dialog
  title="提示"
  :visible.sync="deleteVisible"
  width="82%"
  :before-close="handleClose">
  <span>确认删除？</span>
  <span slot="footer" class="dialog-footer">
    <el-button @click="deleteVisible = false">取 消</el-button>
    <el-button type="danger" @click="deleteAdmin">删 除</el-button>
  </span>
</el-dialog>
<el-dialog title="添加副手" :visible.sync="dialogFormVisible">
  <el-form :model="form" ref="loginFormRef" :rules="rules">
    <el-form-item  label="村庄标签" prop="tag" :label-width="formLabelWidth">
      <el-input v-model="form.tag"  autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="职称" :label-width="formLabelWidth">
      <el-select v-model="form.rank" placeholder="请选择职称">
        <el-option label="一把手" value="0"></el-option>
        <el-option label="二把手" value="1"></el-option>
        <el-option label="三把手" value="2"></el-option>
        <el-option label="荣誉副手" value="3"></el-option>

      </el-select>
    </el-form-item>
     <el-form-item label="职称" :label-width="formLabelWidth">
      <el-select v-model="form.clan" placeholder="请选择职称">
        <el-option label="第一分部" value="0"></el-option>
        <el-option label="第二分部" value="1"></el-option>
        <el-option label="第三分部" value="2"></el-option>

      </el-select>
    </el-form-item>
  </el-form>
  <div slot="footer" class="dialog-footer">
    <el-button @click="dialogFormVisible = false">取 消</el-button>
    <el-button type="primary" @click="addAdmin()">确 定</el-button>
  </div>
</el-dialog>
  </div>
</template>

<script>

export default {

  components:{
  },
  created: async function(){
    const that = this
  
    that.loginUser = JSON.parse(localStorage.getItem('loginUser'))
    const {
        data: res
    } = await that.$http.post('/admin/getAdminList')
    let list = res.data
    if (!list) {
        this.$message.warning('登陆信息过期，请重新登陆')
        this.$router.replace('/Login')
        return
    }
    let adminList = [[],[],[]]
    for (let i = 0; i < list.length; i++) {
      adminList[list[i].clan].push(list[i])
    }

   for(let i = 0; i < adminList.length; i++) {
     adminList[i] = adminList[i].sort((a, b)=>{
       return a.rank- b.rank
     })
   }
   console.log(adminList);
    this.dataList=adminList
  },

  methods: {
    tableRowClassName({row, rowIndex}) {
        let loginUser = JSON.parse(localStorage.getItem('loginUser'))
        if (row.admin_tag === loginUser.tag) {
            return 'warning-row'
        }

    return '';
    },
    addAdmin(){
        this.$refs.loginFormRef.validate(async valid=>{
          console.log(valid);
                      if (!valid) return
            let list = this.dataList
            console.log(list);
            if (this.form.rank <= 2) {

      
              for (let i = 0; i < list[this.form.clan].length; i++) {

                console.log(list[this.form.clan][i].rank);
                console.log(this.form.rank);
                if (list[this.form.clan][i].rank == this.form.rank) {
                  this.$message.error('该职位已经存在')

                  return
                }
                   if (list[this.form.clan][i].tag == this.form.tag) {
                  this.$message.error('该标签已经存在')

                  return
                }
              }
            }
            
            let obj = {
              tag : this.form.tag,
              clan : this.form.clan,
              dealer_tag:this.loginUser.tag,
              rank:this.form.rank
            }

            this.$message.success('添加成功')
            this.$http.post('/admin/addAdmin', {admin: obj}).then(res=>{
              console.log(res);
            })
            this.reload()
      })
    },
    reload(){

    },
    tFormatter(e) {
      if (e.rank<=2)
      return this.rankName[e.rank]
      else {
        return '荣誉副手'
      }
    },
      handleEdit(index, row) {
        this.addAdmin()
      },
      handleDelete(index, row) {
         this.deleteVisible = true
         this.tempTag = row.admin_tag
         this.tempClan = row.clan
         this.tempRank = row.rank
      },
       handleClose(done) {
    
            done();

      },

      deleteAdmin() {
        this.deleteVisible = false
        let lists = this.dataList[this.tempClan]
        console.log(lists);
        for(let i = 0; i < lists.length; i++){
          if (lists[i].admin_tag === this.tempTag) {
              lists.splice(i, 1)
              return
            }
        }


      }
  },
  data(){
    return {
      tempTag: '',
      tempClan: -1,
      tempRank: -1,
      dataList: [],
      form:{
        tag:'',
        rank:'',
        clan:''
      },
      rules: {
            tag : [
                { required: true, message: '标签不能为空', trigger: 'blur'}, 
                { min: 8, max: 12, message: '请输入正确的标签', trigger: 'blur' }

            ]
      },
      rankName: ['一把手','二把手', '三把手'],
      clanName: ['九龙（第一分部）', '恶城（第二分部）', '异族（第三分部）', '凉城（第一分部）'],
      loginUser:{},
      deleteVisible: false,
      dialogFormVisible:false,
      formLabelWidth: '80px'
    }
  }
}
</script>

<style lang="less" >

.el-dialog {
  width: 80% !important;
}
.cell .el-button+.el-button {
    margin-top: 2px;
    margin-left: 0 !important;

}
.el-message-box {
  width: 82% !important;
}
</style>