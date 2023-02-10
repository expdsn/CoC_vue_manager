<template>
  <div @click="$emit('makeCla')">
    <el-breadcrumb separator-class="el-icon-arrow-right" class="mb-5">
    <el-breadcrumb-item>首页</el-breadcrumb-item>
    <el-breadcrumb-item>部落排行</el-breadcrumb-item>
    <el-breadcrumb-item>捐兵排行</el-breadcrumb-item>
    </el-breadcrumb>    

    <el-table class="text-center" :data="dataList"  :row-class-name="tableRowClassName" style="width: 100%">
        <el-table-column  align="center"  type="index" label="排名">
        </el-table-column>
        <el-table-column  prop="name" min-width="120px" label="村庄名">
        </el-table-column>
        <el-table-column prop="donations" label="捐兵数">
        </el-table-column>
        <el-table-column prop="role"  label="职   位">
           <template slot-scope="scope">
               <el-tag type="info" v-if="scope.row.role==='成员'">{{scope.row.role}}</el-tag>
               <el-tag type="danger" v-if="scope.row.role==='副首领'||scope.row.role==='首领'">{{scope.row.role}}</el-tag>

               <el-tag v-if="scope.row.role==='长老'">{{scope.row.role}}</el-tag>


           </template>
        </el-table-column>
        <el-table-column prop="clan"  :formatter="tFormatter" label="分部">
        </el-table-column>
    </el-table>
  </div>
</template>

<script>

export default {

  components:{
  },
  created(){
    this.getClanData()
  },
  methods: {
    async getClanData(){
      const that = this
      const { data: res} =await  that.$http.post('/clan/getAllClanInfo')
      if(res.code != 200) {
         this.$message.warning('登陆信息过期，请重新登陆')
            this.$router.replace('/Login')
            return
      }
      let list = res.data
      this.donationsRank = list.sort((a, b) => {
       return b.donations - a.donations
      })
      that.dataList = list

    },
    tFormatter(e) {
      return this.clanName[e.clan]
    },
        tableRowClassName({row, rowIndex}) {
        let loginUser = JSON.parse(localStorage.getItem('loginUser'))
        if (row.tag === loginUser.tag) {
            return 'warning-row'
        }

    return '';
    }
  },
  data(){
    return {
      dataList: [],
      clanName: ['九龙', '恶城', '异族', '凉城'],
    }
  }
}
</script>

<style lang="less" scoped>

</style>