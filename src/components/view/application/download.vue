<template>
<div @click="$emit('makeCla')"> 
    <div class="bg-white border-gray-300 h-12 dnav border-b-2">
       <el-page-header @back="goBack" content="版本下载">

         </el-page-header>
    </div>
    <div class="p-5">
    <div class="border-l-8 border-blue-400 pl-1 mt-5 mb-5">coc下载</div>

    <ul class="apps">
        <li class="active">
            <a target="_blank" href="http://coc.kunlun.com/" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">昆仑版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="http://www.9game.cn/coc/" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">九游版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="https://games.qq.com/tencent/COC/" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">腾讯版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="https://appstore.huawei.com/app/C10329573" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">华为版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="http://www.anzhi.com/pkg/ea7c_com.supercell.clashofclans.anzhi.html" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">安智版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="http://www.google.com/" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">谷歌版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="https://www.wandoujia.com/apps/7597066" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">豌豆荚版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="https://mobile.baidu.com/item?pid=1540839" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="1529984491.png">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">百度版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="http://www.guopan.cn/blct/" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">果盘版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="https://www.oppomobile.com/index.html" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">OPPO版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="http://game.vivo.com.cn/#/detail/35790" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">VIVO版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="http://news.4399.com/buluozz/" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">4399版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="http://zhushou.2345.com/game/174645.html" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">2345版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="http://update.coc.kunlun.com/?channel=360&amp;go=1" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">360版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="https://game.xiaomi.com/game/62231040" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">小米版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="http://www.qmzs.com/gamedetail/appid_5ysre" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">全民版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="https://android.d.cn/game/84833.html" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">当乐版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="http://www.kpzs.com/game/blctcoc1.html" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">靠谱助手版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="https://www.muzhiwan.com/com.supercell.clashofclans.ewan.mzw.html" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">拇指玩版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="http://www.ewan.cn/game-id-20275.html" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">益玩版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="https://www.xyaz.cn/gc/apps-586-1.html" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">逍遥版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="http://dl.wan.sogoucdn.com/dl0/1387/app12195_default_0009000500395.apk" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">搜狗版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="https://app.yeshen.com/games/single/9360" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">夜神版</span>
            </a>
        </li>
        <li class="active">
            <a target="_blank" href="https://www.lenovomm.com/appdetail/com.supercell.clashofclans.lenovo/1138" class="detail">
                <div class="img">
                    <img src="http://leiren520.com/assets/img/download/download-1.png" alt="">
                </div>
                <span style="display: inline-block;white-space:nowrap; text-overflow:ellipsis;overflow:hidden; width:80px;">联想版</span>
            </a>
        </li>

    </ul>
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