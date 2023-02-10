<template>
  <div>
    <div class="bg-white border-gray-300 h-12 dnav border-b-2">
    <el-page-header @back="goBack" content="联赛报名"></el-page-header>
    </div>
    <div class="p-5 shadow-md mt-7 sign">

        <div class="text-2xl text-gray-400 text-center"><span>九龍联赛报名系统</span></div>

        <div class="sct1">
            <div class="text-md text-gray-500 text-center">请选择你的分部</div>
            <div class="h-20">
                
            </div>
        </div>
        <el-steps  :active="active" finish-status="success" align-center>
        <el-step title="选择分部"></el-step>
        <el-step title="确认场次"></el-step>
        <el-step title="完成报名"></el-step>
        </el-steps>
    </div>

  </div>
</template>

<script>
export default {
    beforeCreate () {
    window.scroll(0, 0);
    document.querySelector('.el-main').setAttribute('style', 'padding: 0 !important;')
    },
    //销毁前清除
    beforeDestroy () {
        document.querySelector('.el-main').removeAttribute('style')
    },
    methods:{
        goBack() {
        this.$router.back(-1)
      }
    },
    data(){
        return {
            active :0       
        }
    }
}
</script>

<style scoped>
.sign{
    min-height: 400px;
    position: relative;
}
.el-steps {
    position: absolute;
    bottom:10px;
    width: 100%;
    left:10px;
    }
</style>