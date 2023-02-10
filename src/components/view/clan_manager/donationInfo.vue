<template>
  <div @click="$emit('makeCla')">
    <el-breadcrumb separator-class="el-icon-arrow-right" class="mb-5">
    <el-breadcrumb-item>首页</el-breadcrumb-item>
    <el-breadcrumb-item>部落管理</el-breadcrumb-item>
    <el-breadcrumb-item>捐收情况</el-breadcrumb-item>
    </el-breadcrumb>   
    <el-table :row-class-name="tableRowClassName" class="text-center" :data="dataList"  style="width: 100%">
        <el-table-column align="center" type="index" label="">
        </el-table-column>
        <el-table-column min-width="120px" prop="name" label="村庄名">
        </el-table-column>
        <el-table-column prop="expLevel" label="等级">
        </el-table-column>
        <el-table-column prop="clan" :formatter="tFormatter" label="分部">
        </el-table-column>
    </el-table>
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
    } = await that.$http.post('/clan/getAllClanInfo')
    that.clansData = res.data
    let list = this.clansData
    if (!list) {
        this.$message.warning('登陆信息过期，请重新登陆')
        this.$router.replace('/Login')
        return
    }
    this.dataList = list.sort((a, b) => {
        return b.expLevel - a.expLevel
    })
  },
  methods: {
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
  },
  data(){
    return {
      dataList: [],
      clanName: ['九龙', '恶城', '异族', '凉城'],
    }
  }
}
</script>

<style>


</style>