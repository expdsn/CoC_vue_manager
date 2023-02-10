<template>
  <div @click="$emit('makeCla')">
    <el-breadcrumb separator-class="el-icon-arrow-right" class="mb-5">
    <el-breadcrumb-item>首页</el-breadcrumb-item>
    <el-breadcrumb-item>部落管理</el-breadcrumb-item>
    <el-breadcrumb-item>黑名单</el-breadcrumb-item>
    </el-breadcrumb>   
  <el-alert
      title="当前身份不是管理员，不能添加或修改"
      type="warning"
      show-icon :closable="false" v-if="loginUser.isAdmin<1">
    </el-alert>
      <el-button type="danger" class="mt-2"
       :disabled="loginUser.isAdmin<1" round @click="handleAdd()">添加黑名单</el-button>
    <div class="border-l-8 border-red-400 pl-1 mt-5" >部落黑名单</div>

    <el-table :row-class-name="tableRowClassName" class="text-center" :data="dataList"  style="width: 100%">
        <el-table-column  prop="name" label="村庄名">
        </el-table-column>
        <el-table-column prop="tag"  label="村庄标签">
        </el-table-column>
        <el-table-column prop="reason" min-width="100px" label="被踢原因">
        </el-table-column>
        <el-table-column prop="clan"  label="操作">
          <template slot-scope="scope">
             <el-button type="danger" icon="el-icon-delete" circle
                @click="handleDelete(scope.$index, scope.row)" :disabled="loginUser.isAdmin<1"></el-button>
          
          </template>
        </el-table-column>
    </el-table>
    <el-dialog title="添加黑名单" :visible.sync="dialogFormVisible">
  <el-form :model="form" ref="loginFormRef" :rules="rules">
    <el-form-item  label="村庄标签" prop="tag" :label-width="formLabelWidth">
      <el-input v-model="form.tag"  autocomplete="off"></el-input>
    </el-form-item>
      <el-form-item  label="拉黑理由" prop="reason" :label-width="formLabelWidth">
      <el-input v-model="form.reason"  autocomplete="off"></el-input>
    </el-form-item>
  </el-form>
  <div slot="footer" class="dialog-footer">
    <el-button @click="dialogFormVisible = false">取 消</el-button>
    <el-button type="danger" @click="addAdmin()">确 定</el-button>
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
    const {
        data: res
    } = await that.$http.post('/admin/getBlackList')
    let list = res.data
    if (!list) {
        this.$message.warning('登陆信息过期，请重新登陆')
        this.$router.replace('/Login')
        return
    }
    this.dataList = list
    that.loginUser = JSON.parse(localStorage.getItem('loginUser'))

  },
  methods: {
    addAdmin(){
      const that = this
      this.$refs.loginFormRef.validate(async valid=>{
            if(!valid) {return}
          if(this.checkExist(this.form.tag)) {
            return
          }

          that.$http.post('/admin/addBlack',{
            tag: that.form.tag,
            dealer: that.loginUser.tag,
            reason: that.form.reason
          }).then(res=>{
            if(res.data.code == 200) {
              that.$message.success('拉黑成功')
              that.reload()
              that.dialogFormVisible = false
            }else {
              that.$message.error('发生未知错误，拉黑失败！')
              that.dialogFormVisible = false

            }
          })

      })
    },
    async reload() {
       const that = this
        const {
            data: res
        } = await that.$http.post('/admin/getBlackList')
        let list = res.data
        if (!list) {
            this.$message.warning('登陆信息过期，请重新登陆')
            this.$router.replace('/Login')
            return
        }
        this.dataList = list
    },
    checkExist(tag){
      let list =this.dataList
      for (const it of list) {
        if (it.tag === tag) {
          this.$message.error('已经存在，请勿重复添加！')
          return true
        }
      }
      return false
    },
    handleAdd(){
      this.dialogFormVisible=true
      
    },
    tableRowClassName({row, rowIndex}) {
        let loginUser = JSON.parse(localStorage.getItem('loginUser'))
        if (row.tag === loginUser.tag) {
            return 'warning-row'
        }

    return '';
    },
    tFormatter(e) {
      return this.clanName[e.clan]
    },
    handleDelete(e){
      let _tag = this.dataList[e].tag
      this.dataList.splice(e, 1)
      const that = this
      that.$http.post('/admin/deleteBlack',{tag:_tag}).then(res=>{
        if(res.data.code ==200) {
          that.$message.success('移出成功！')
        }else {
          that.$message.error('发生错误，移出失败！')
        }
      })
    }
  },
  data(){
    return {

      rules: {
            tag : [
                { required: true, message: '标签不能为空', trigger: 'blur'}, 
                { min: 8, max: 12, message: '请输入正确的标签', trigger: 'blur' }

            ],
            reason: [
                 { required: true, message: '理由不能为空', trigger: 'blur'}, 
                { max: 30, message: '不能太长', trigger: 'blur' }
            ]
      },
      dataList: [],
      loginUser:{},
      formLabelWidth: '80px',
      form: {
      },
      dialogFormVisible:false,
      clanName: ['九龙', '恶城', '异族', '凉城'],
    }
  }
}
</script>

<style>


</style>