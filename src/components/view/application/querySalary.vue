<template>
<div @click="$emit('makeCla')">
    <div class="bg-white border-gray-300 h-12 dnav border-b-2">
       <el-page-header @back="goBack" content="奖章查询">

         </el-page-header>
    </div>
    <div class="p-5">
    <div class="text-center pl-1 mt-5 mb-5">九龍山庄部落联赛奖章计算系统</div>
    <el-form ref="form" :model="form" label-width="80px">
        <el-form-item label="联赛段位">
            <el-select v-model="form.rank" placeholder="请选择联赛段位">
            <el-option label="冠军1" value="17"></el-option>
            <el-option label="冠军2" value="16"></el-option>
            <el-option label="冠军3" value="15"></el-option>
            <el-option label="大师1" value="14"></el-option>
            <el-option label="大师2" value="13"></el-option>
            <el-option label="大师3" value="12"></el-option>
            <el-option label="水晶1" value="11"></el-option>
            <el-option label="水晶2" value="10"></el-option>
            <el-option label="水晶3" value="9"></el-option>
            <el-option label="黄金1" value="8"></el-option>
            <el-option label="黄金2" value="7"></el-option>
            <el-option label="黄金3" value="6"></el-option>
            <el-option label="白银1" value="5"></el-option>
            <el-option label="白银2" value="4"></el-option>
            <el-option label="白银3" value="3"></el-option>

            </el-select>
        </el-form-item>
        <el-form-item label="部落名次">
            <el-select v-model="form.vicCount" placeholder="请选择部落名次">
            <el-option label="第一名" value="7"></el-option>
            <el-option label="第二名" value="6"></el-option>
            <el-option label="第三名" value="5"></el-option>
            <el-option label="第四名" value="4"></el-option>
            <el-option label="第五名" value="3"></el-option>
            <el-option label="第六名" value="2"></el-option>
            <el-option label="第七名" value="1"></el-option>
            <el-option label="第八名" value="0"></el-option>
     
            </el-select>
        </el-form-item>
             <el-form-item label="获得星数">
            <el-select v-model="form.starts" placeholder="请选择获得星数">
            <el-option label="8星及以上" value="1"></el-option>
            <el-option label="7星" value="0.9"></el-option>
            <el-option label="6星" value="0.8"></el-option>
            <el-option label="5星" value="0.7"></el-option>
            <el-option label="4星" value="0.6"></el-option>
            <el-option label="3星" value="0.5"></el-option>
            <el-option label="2星" value="0.4"></el-option>
            <el-option label="1星" value="0.3"></el-option>
            <el-option label="0星" value="0.2"></el-option>

     
            </el-select>
        </el-form-item>
        <div class="text-center">

             <el-button @click="startCal()" type="primary">开始计算</el-button>
        </div>
    </el-form>
    <div class="mt-2 text-gray-500" v-if="isComputed">

        <div class="text-center">计算结果: </div>
        <div class="text-center">
            <span>可获得奖章数：{{result.salary}}</span>
        </div>
        <div class="text-center">
            <span>额外奖励：{{result.ex}}，</span>
            <span>份数：{{result.count}}</span>
        </div>
    </div>
    </div>
    <div>
        <img src="https://pic.imgdb.cn/item/6190c88b2ab3f51d91bf9819.jpg" alt="">
        <img src="https://pic.imgdb.cn/item/6190c8842ab3f51d91bf9659.jpg" alt="">

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
    created(){
        let lists= new Array()
        let base = [20, 32, 44, 55, 73, 91, 108, 132,156, 179,209,239,268,304,340,375,417,459]
        for (let i = 0; i < 18; i++) {
            lists[i] = new Array()
            lists[i][0] = base[i]
        }
        let count = 0;
        for (let i = 0; i < 18; i++) {
            for(let j = 0; j < 7; j++) {

                lists[i][j+1] = lists[i][j] +2 + Math.round(i/3-0.5)

            }

        }
        this.salaryLists = lists
    },
    methods:{
        goBack() {
        this.$router.back(-1)
      },
      startCal(){
          let result = {
              salary:'',
              ex:'',
              count:''
          }
          let lists = this.salaryLists
          result.salary = Math.round(lists[this.form.rank][this.form.vicCount] * this.form.starts -0.5)
          result.ex = this.baseExSalary[this.form.rank]
        //   result.count =  this.baseCount[Math.round((Number.parseInt(this.form.rank)+1)/ 3 - 0.5) ]  + Number.parseInt(this.form.vicCount)    
        let temp = Math.round(this.form.rank / 3 -0.5)
        result.count = this.baseCount[temp] + Number.parseInt(this.form.vicCount)   
        this.result = result
        this.isComputed = true
      }
    },

    data(){
        return {
            baseExSalary : [35,35,35,35,40,45,50,55,60,65,70,75,80,85,90,95,100,105],
            baseCount: [1,1,2,2,3,4],
            salaryLists :[],
            urlList:[],
            result:{},
            isComputed:false,
            form:{
                rank:'',
                vicCount:'',
                starts:''
            }
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