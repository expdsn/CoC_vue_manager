<template>
    <div>
         <el-breadcrumb separator-class="el-icon-arrow-right" class="mb-5">
            <el-breadcrumb-item>首页</el-breadcrumb-item>
            <el-breadcrumb-item>部落设置</el-breadcrumb-item>
         </el-breadcrumb>   
           <el-alert 
            v-if="loginUser.isAdmin<1"
            title="您的身份为成员，不能对页面进行修改"
            type="info"
            :closable="false">
        </el-alert>
          <el-alert
          v-if="loginUser.isAdmin>=1"
            title="随意修改可能会引发网站崩溃！"
            type="warning"
            close-text="知道了"
            @close="closeAlert"
            >
        </el-alert>
        <div>

        </div>
        <div class="mt-5">

            <el-form :model="stForm"  ref="ruleForm" label-width="80px"  class="demo-ruleForm">
                <div class="text-center text-gray-400 mt-2 mb-2"><span>捐兵提示值设置</span></div>
                <el-form-item label="九龍" prop="clan1">
                    <el-input  v-model.number="stForm.donations[0]" :disabled="!canAlter"></el-input>
                </el-form-item>
               <el-form-item label="恶城" prop="clan2">
                    <el-input v-model.number="stForm.donations[1]" :disabled="!canAlter"></el-input>
                </el-form-item>
                <el-form-item label="异族" prop="clan3">
                    <el-input v-model.number="stForm.donations[2]" :disabled="!canAlter"></el-input>
                </el-form-item>
              <el-divider></el-divider>

            </el-form>
        </div>
                <div class="mt-5">

            <el-form :model="stForm"  ref="ruleForm" label-width="80px"  class="demo-ruleForm">
                <div class="text-center text-gray-400 mt-2 mb-2"><span>捐收比设置</span></div>
                <el-form-item label="九龍" prop="rate">
                    <el-input  v-model="stForm.rate[0]" :disabled="!canAlter"></el-input>
                </el-form-item>
               <el-form-item label="恶城" prop="clan2">
                    <el-input v-model="stForm.rate[1]" :disabled="!canAlter"></el-input>
                </el-form-item>
                <el-form-item label="异族" prop="clan3">
                    <el-input v-model="stForm.rate[2]" :disabled="!canAlter"></el-input>
                </el-form-item>
              <el-divider></el-divider>

            </el-form>
        </div>
       <div class="mt-5 text-center" v-if="canAlter">
           <el-button @click="submitChange()" type="warning">确认修改</el-button>
        </div>



    </div>
</template>

<script>
export default {
    created(){
        this.$http.post('/conf/getClanSetting').then(res=>{
            let conf = res.data.data
            this.stForm.donations = conf.donations
            this.stForm.rate = conf.rate
  
        })
        this.loginUser = JSON.parse(localStorage.getItem('loginUser'))
    },
    data(){
        return {
         stForm: {
                donations:[],
                rate:[]
            },
            loginUser: {},
            canAlter: false
        }
    }
    ,methods:{
        closeAlert(){
            this.canAlter = true
        },
        submitChange() {
            const that = this
                    that.canAlter = false
          
            this.$http.post('/conf/setClanSetting',{config:that.stForm}).then(res=>{
                console.log(res);
                if (res.data.code ==200) {
                    that.$message.success('修改成功')

                }else {
                    that.$message.error('发生了未知的错误！修改失败')
                }
            })

            }
    }
}
</script>

<style lang="less" scoped>

</style>