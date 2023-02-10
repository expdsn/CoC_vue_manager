<template>
  <div>
      <div class="text-red-300 text-center">当前服务器正在维护，请稍后访问</div>
      <span class="text-gray-200 ">   {{dataList}}</span>
   
  </div>
</template>

<script>
export default {
    created(){
        const that = this
        this.$http.post('/test/getOriginData').then(res=>{
            console.log(res);
            console.log(res.data);
            that.dataList = res.data
        })
    },
    data(){
        return {
            dataList: []
        }
    }
}
</script>

<style>

</style>