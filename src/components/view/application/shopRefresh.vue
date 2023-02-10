<template>
<div @click="$emit('makeCla')">
    <div class="bg-white border-gray-300 h-12 border-b-2 dnav">
       <el-page-header @back="goBack" content="商店刷新">

         </el-page-header>
    </div>
    <div class="p-5">
    <div class="text-center pl-1 mt-5 mb-5">COC部落冲突商店物品刷新时间</div>
        <div class="text-gray-500">每日商店500宝石一本的王书，诱惑真是太大啦！但是好多小伙伴搞不懂他的刷新时间，我特意为大家从网上收集了最新的刷新物品时间表。希望可以对大家有帮助。</div>
    </div>
    <div>
    <div class="border-l-8 border-blue-400 pl-1 mt-5 mb-5">商店刷新图</div>

        <img src="https://pic.imgdb.cn/item/6190e6e22ab3f51d91c8589a.png" alt="">
    </div>
    <div class="p-5">
        <div class="text-gray-500">每人刷新的物品都不一样，需要根据自己今日物品按图索骥，这样可以让自己合理运用宝石！推荐每日商店只买王书！！！其他物品没什么划算了，除了免费的训练药水～</div>
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
        console.log('go back');
        this.$router.back(-1)
      }
    },

    data(){
        return {
            urlList:[]
        }
    }
}
</script>


<style lang="less" scoped>
        
        .el-main {
            padding: 0 !important;
        }
        body{
            background-color: #fafafa !important;
        }
        .apps {
            display: flex !important;
            flex-wrap: wrap !important;
            justify-content: space-between;
        }
</style>