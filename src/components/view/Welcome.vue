<template>
<div @click="emitCla()">

    <el-row>
        <div><span class="text-3xl antialiased subpixel-antialiased pl-2">{{loginUser.name}}<span class="italic text-lg text-gray-400">{{loginUser.role}}</span>, {{getTime}}</span> </div>
        <div class="mt-1 antialiased text-sm text-right text-gray-400">欢迎登录《九龍山庄》部落管理系统</div>
          <div class="text-red-100 text-center" >当前版本：内测版Beta3.5</div>
    </el-row>


    <el-divider></el-divider>

    <div class="text-center  text-base subpixel-antialiased text-gray-600">各个分部总人数

    </div>
    <div class="text-center text-xs  text-gray-300">点击下面圆框可复制部落标签</div>
    <el-row class="text-center">
        <el-col :span="12">
            <span class="text-gray-500 text-sm">第一分部</span>
            <div class="border-2 m-2 rounded-full"  @click="copy(0)" :class="{
                        
                        'border-red-400':(clanPeople[0]<=30),
                        'border-yellow-400': (clanPeople[0]>30 && clanPeople[0]<=42),
                        'border-green-400' : clanPeople[0]>42 && clanPeople[0]<=48,
                        'border-red-400':(clanPeople[0]>=49)

                    }" >
                <div class="text-gray-400 text-sm">九龙</div>
                <div class="text-gray-500 text-xs"></div>

                <div class="text-xl font-bold">{{clanPeople[0]}}</div>
            </div>
        </el-col>
        <el-col :span="12">
            <span class="text-gray-500 text-sm">第二分部</span>

            <div class="border-2 m-2 rounded-full" @click="copy(1)"   :class="{

                        'border-red-400':(clanPeople[1]<=35),
                        'border-yellow-400': (clanPeople[1]>35 && clanPeople[1]<=42),
                        'border-green-400' : clanPeople[1]>42 && clanPeople[1]<=48,
                        'border-red-400':(clanPeople[1]>48)

                    }">
                <div class="text-gray-400 text-sm">恶城</div>
                <div class="text-xl font-bold">{{clanPeople[1]}}</div>

            </div>
        </el-col>
    </el-row>
    <el-row class="text-center">
        <el-col :span="12">
            <span class="text-gray-500 text-sm">第三分部</span>

            <div class="border-2 m-2 rounded-full"  @click="copy(2)"   :class="{

                        'border-red-400':(clanPeople[2]<=35),
                        'border-yellow-400': (clanPeople[2]>35 && clanPeople[2]<=42),
                        'border-green-400' : clanPeople[2]>42&& clanPeople[2]<=48,
                        'border-red-400':(clanPeople[2]>=49)
                    }">
                <div class="text-gray-400 text-sm">异族</div>
                <div class="text-xl font-bold">{{clanPeople[2]}}</div>
            </div>
        </el-col>
        <el-col :span="12">
            <span class="text-gray-500 text-sm">第四分部</span>

            <div class="border-2 m-2 rounded-full text-gray-400">
                <div class="text-gray-400 text-sm">暂未开通</div>
                <div class="text-xl font-bold">--</div>
            </div>
        </el-col>

    </el-row>
    <div class="border-l-8 border-blue-400 pl-1 mt-3">个人提醒</div>
        <div v-if="personalInfo.length==0" class="shadow-md mt-2 bg-green-300 rounded-2xl w-full p-2 pl-5">
            <span class="text-white text-md">您的捐收比为<span>{{rate}}</span>,达到部落要求,请继续保持</span>
        </div>
          
        <div v-for="(item, index) in personalInfo" :key="index"  class="shadow-md mt-2  rounded-2xl  w-full p-2 pl-5" :class="{
            'bg-blue-300':item.type==0,
            'bg-yellow-300':item.type==1,
            'bg-red-300':item.type==2,
            'bg-green-300':item.type==3,



        }">
            <span class="text-white">{{item.info}}</span>
        </div>

    <div class="border-l-8 border-blue-400 pl-1 mt-3">部落建议</div>
    <div class="text-white">
        <div v-if="infoList.length==0" class="shadow-md mt-2 bg-green-300 rounded-2xl w-full p-2 pl-5">
            <span>部落当前状态良好</span>
        </div>
     
  
        <div v-for="(item, index) in infoList" :key="index"  class="shadow-md mt-2  rounded-2xl  w-full p-2 pl-5" :class="{
            'bg-blue-300':item.type==0,
            'bg-yellow-300':item.type==1,
            'bg-red-300':item.type==2,
            'bg-green-300':item.type==3,



        }">
            <span>{{item.info}}</span>
        </div>

    </div>
    <div class="border-l-8 border-blue-400 pl-1 mt-5">部落应用</div>

    <div class="mt-2">
        <el-row :gutter="15">
            <el-col :span="12">
                <div @click="openApp('Download')" 
                class="w-full bg-download rounded-xl  shadow-md application">
                    <span class="text-white  antialiased subpixel-antialiased font-semibold text-xl">版本下载</span>
                </div>
            </el-col>
            <el-col :span="12">
                 <div @click="openApp('showRefresh')" 
                 class="w-full bg-shop rounded-xl shadow-md application">
                    <span class="text-white  antialiased subpixel-antialiased font-semibold text-xl">商店刷新</span>
                </div>
            </el-col>

        </el-row>
        <el-row :gutter="15" class="mt-3">
            <el-col :span="12">
                 <div @click="openApp('querySalary')" 
                 class="w-full bg-query rounded-xl shadow-md application">
                    <span class="text-white  antialiased subpixel-antialiased font-semibold text-xl">奖章查询</span>
                </div>
            </el-col>
            <el-col :span="12">
                <div @click="openApp('signUp')" 
                 class="w-full bg-sign rounded-xl shadow-md application">
                    <span class="text-white  antialiased subpixel-antialiased font-semibold text-xl">联赛报名</span>
                </div>
            </el-col>

        </el-row>
    </div>
    <div class="border-l-8 border-blue-400 pl-1 mt-5">部落捐兵前10名</div>

    <el-table class="text-center" :data="donationsRank" stripe style="width: 100%">
        <el-table-column align="center" type="index" label="排名">
        </el-table-column>                  
        <el-table-column min-width="120px" prop="name" label="村庄名">
        </el-table-column>
        <el-table-column prop="donations" label="捐兵数">
        </el-table-column>
        <el-table-column prop="clan" :formatter="tFormatter" label="分部">
        </el-table-column>
    </el-table>
    <div class="border-l-8 border-blue-400 pl-1 mt-5">部落收兵前10名</div>

    <el-table class="text-center" :data="receiveRank" stripe style="width: 100%">
        <el-table-column align="center" type="index" label="排名">
        </el-table-column>
        <el-table-column min-width="120px" prop="name" label="村庄名">
        </el-table-column>
        <el-table-column prop="donationsReceived" label="收兵数">
        </el-table-column>
        <el-table-column prop="clan" :formatter="tFormatter" label="分部">
        </el-table-column>
    </el-table>

    <div class="text-gray-300 text-center mt-5">版本号：Beta1.2</div>
    <div class="text-gray-300 text-center">开发者：感觉</div>

</div>
</template>

<script>
import Vue from 'vue'

export default {

    created: async function () {
        //关闭测试信息
        const that = this

        const { data: res } = await this.$http.post('/test/testConn')
        if (res.code != 200) {
            this.$message.error('登录已经过期！')
            this.$router.replace({path: '/Login'})
            localStorage.clear()
            return
        }
        await this.$http.post('/conf/getClanSetting').then(res=>{
            let conf = res.data.data
            this.donationsRule = conf.donations
            this.rateRule = conf.rate
  
        })
    
        //获取数据
        await this.getClanData()
        //获取黑名单并检查
        await this.checkBlackList()
        //获取管理名单并检查
        await this.checkAdminList()
        //检查部落人数
        this.insertCountInfo()
        //检查部落捐兵
        this.checkDonations()
    },
    mounted: function () {
        let obj = JSON.parse(localStorage.getItem('loginUser'))
 
        Vue.set(this.loginUser, 'name', obj.username)
        Vue.set(this.loginUser, 'tag', obj.tag)
        Vue.set(this.loginUser, 'role', obj.role)

    },
    methods: {
        emitCla(){
            this.$emit('makeCla')
        },
        getClan(){
            let loginUser = JSON.parse(localStorage.getItem('loginUser'))

        },
        openApp (e){
            this.$router.push('/application/'+e)
        },
        async checkAdminList(){
            const that = this
            const { data: res} = await that.$http.post('/admin/getAdminList')
            const admin_list = res.data
            let clan_list = that.clansData
            let _infoList = this.infoList

            for (const mem of clan_list) {
                if (mem.role==='副首领') {
                    for (let i = 0; i < admin_list.length; i++) {
                        if (admin_list[i].tag === mem.tag) {

                            break
                        }
                        if (i == admin_list.length) {
                            _infoList.push({
                            info: mem.name + '（'+this.clanName[mem.clan]+
                            '）的副首领任命未经审核，建议撤职',
                            type: 1
                            })

                        }

                        
                    }
                }
            }
        },
        async checkBlackList(){
            const that = this
            let clan_list = that.clansData
            let info_list = that.infoList
            const { data: res} = await that.$http.post('/admin/getBlackList')
            let black_list = res.data
            for (const it1 of black_list) {
                for (const it2 of clan_list) {
                    if (it1.tag === it2.tag) {
                        info_list.push({
                            info: it2.name+'（'+ this.clanName[it2.clan] +'）在黑名单上，请及时踢出',
                            type: 2
                       })
                    }
                }
            }
        },
        async getClanData(){
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
            this.donationsRank = list.sort((a, b) => {
                return b.donations - a.donations
            }).slice(0, 10)
            this.receiveRank = list.sort((a, b) => {
                return b.donationsReceived - a.donationsReceived
            }).slice(0, 10)
            let count = [0, 0, 0, 0]
            for (let i = 0; i < list.length; i++) {
                count[list[i].clan]++;
            }
            this.clanPeople = count

        },
        checkDonations() {
            let list = this.clansData
            let _infoList = this.infoList
            let _personList = this.personalInfo
            for (const it of list) {
                if (it.tag === this.loginUser.tag) {
                    let rate = ''
                    this.loginClan = it.clan
                    if (it.donationsReceived == 0) { this.rate = '∞'
                    
                    }
                    else {
                        rate = it.donations / it.donationsReceived
                        if (rate >= 1) {
                            rate = rate.toFixed()
                        }  
                        // _personList.push({
                        //                 info: '您的捐收较低（' + rate.toFixed(1) +'）,请注意你的捐收！,'+this.clanName[it.clan]+'的捐收比要求是最低0.5',
                        //                 type: 1
                        //             })
                        else {
                           if (rate >= this.rateRule[it.clan]) {
                              rate = rate.toFixed(1)
                           }else {
                             _personList.push({
                                info: '您的捐收较低（' + rate.toFixed(2) +'）,请注意你的捐收！,'+this.clanName[it.clan]+'的捐收比要求是最低为'+this.rateRule[it.clan],
                                type: 1
                            })
                           }
                            
                        }
                  
                        this.rate = rate
                    }
 
                }
                if (it.donations>=this.donationsRule[it.clan]&&it.role=='成员') {
                    _infoList.push({
                        info: it.name + '（'+this.clanName[it.clan]+'）捐兵达标 ('+it.donations +')，建议授予长老职位',
                        type: 3
                    })
                }
            }
       
        },
        //插入部落人数建议信息，并渲染
        insertCountInfo() {
            let counts = this.clanPeople
            let list = this.infoList
            let words = ['一', '二', '三', '四']
            for (let i = 0; i < 3; i++) {
                if (counts[i]>=49) {
                    list.push({
                        info: "第" + words[i] + '分部人数过多，请副首领及时清理死鱼',
                        type: 0
                    })
                }else if (counts[i] <=35){
                    list.push({
                        info: "第" + words[i] + '分部人数过少，请副首领招收新成员',
                        type: 2
                    })
                }else if (counts[i] >35 && counts[i] <= 42) {
                    list.push({
                        info: "第" + words[i] + '分部人数较少，请继续招收新成员',
                        type: 1
                    })
                }
            }
            this.infoList = list
        },

        copy(e) {
            const that = this
            this.$copyText(that.clanTags[e]).then(suceess=>{
                that.$message.success('部落标签成功复制到剪贴板')
            }, error=>{

            })

        },
        tFormatter(e) {
            return this.clanName[e.clan]
        },
       getDateString() {
            let hour = (new Date()).getHours()
            if (hour <= 5) {
                return '凌晨'
            } else if (hour >= 6 && hour <= 13) {
                return '中午'
            } else if (hour > 13 && hour < 18) {
                return '下午'
            } else if (hour >= 18 && hour <= 19) {
                return '傍晚'
            } else {
                return '晚上'

            }
        },
    },
    computed:{
        getTime() {
            
            return this.getDateString() + '好'
        },
        getClanName(e) {
            return this.clanName[e]
        }
    },
    data() {
        return {
            testInfo: true,
            clansData: [],
            clanPeople: [0, 0, 0, 0],
            loginUser: {},
            personalInfo: [],
            loginClan:0,
            donationsRule:[],
            rateRule:[],
            donationsRank: [],
            receiveRank: [],
            clanPeople: ['--', '--', '--', '--'],
            clanName: ['九龙', '恶城', '异族', '凉城'],
            clanTags: ['#LYGV880Y', '#2PURL2U2', '#G2R8CYPR'],
            longText: '',
            infoList: [],
            rate:'?',
            infoTypeClass: ['text-blue-300', 'text-yellow-300', 'text-red-300']
        }
    }
}
</script>

<style lang="less" scoped>

    .application {
        width: 100%;
        height: 70px;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .tips{
        border-left: 10px solid #409EFF;
    }
    .bg-download{
        background-image: linear-gradient(to bottom right, #f76692, #eb295e);
    }
     .bg-download span {

         text-shadow:-2px -2px 4px #ec3059;
     }
    .bg-shop{
        background-image: linear-gradient(to bottom right, #ffb023, #ffd038);
    }
       .bg-shop span {

         text-shadow:-2px -2px 2px #fa8f20;
     }
    .bg-query{
        background-image: linear-gradient(to bottom right, #ff999a, #ff999a);
    }
    .bg-sign{
        background-image: linear-gradient(to bottom right, #55cdd0, #64d9bd);
    }
     .bg-query span {

         text-shadow:-2px -2px 2px #f76c6c;
     }
        .bg-sign span{
        text-shadow:-2px -2px 2px #3da7a7;

    }
</style>
