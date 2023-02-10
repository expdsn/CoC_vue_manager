<template>
  <div>
    <el-breadcrumb separator-class="el-icon-arrow-right" class="mb-5">
    <el-breadcrumb-item>首页</el-breadcrumb-item>
    <el-breadcrumb-item>修改公告</el-breadcrumb-item>

    </el-breadcrumb>    
        <el-input
                type="textarea"
                :rows="2"
                placeholder="请输入内容"
                v-model="textarea">
        </el-input>

  </div>
</template>

<script>
export default {
    data(){
        return{
            textarea:""
        }
    }
}
</script>

<style>

</style>