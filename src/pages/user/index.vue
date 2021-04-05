<template>
  <div>
      <div class="weui-cells weui-cells_form">
        <div class="weui-cell weui-cell_active weui-cell_select weui-cell_select-after">
          <div class="weui-cell__hd"><label class="weui-label test">冷藏支持</label></div>
            <div class="weui-cell__bd weui-flex" @click="showSelector">
            <span class="weui-select">{{province+" "+city+" "+district}}</span>
          </div>
        </div>
      </div>
<!--     <button @click="showSelector">选择省市区</button> -->
    <div>{{province+" "+city+" "+district }}</div>
    <region-selector :isShow="selectorShow"  @hideSelector="hideSelector"></region-selector>
    <upload width="120rpx" height="120rpx" max="6" @choosed="choosed" ></upload>
  </div>
</template>

<script>
import regionSelector from '@/components/regionSelector';
import Upload from "@/components/upload"
export default {
    components:{
        regionSelector,
        Upload
    },
    data(){
        return {
            selectorShow:false,
            province:"北京市",
            city:"北京市",
            district:"东城区"
        }
    },
    methods:{
        showSelector(){
            this.selectorShow = true;
        },
        hideSelector(info){
            console.log(info)
            if(info){
                this.province=info[0].name,
                this.city=info[1].name,
                this.district=info[2].name
            }
            this.selectorShow=false
        },
    },
    onPullDownRefresh () {
        console.log('下拉刷新')
    },
    onReachBottom () {
        console.log('触底了')
    },
    mounted (){

    let _this=this;
    wx.login({
        success(res) {
            console.log(res)
            _this.globalData.code=res.code
            console.log(_this.globalData.code)
            /* if (res.code) {
                // 发起网络请求
                wx.request({
                url: 'https://api.weixin.qq.com/sns/jscode2session',
                data: {
                    appid:"wx212fe30dc9b5319f",  //开发者appid
                    secret:"d73c38823e51a312bf70165417e9256c", //开发者AppSecret(小程序密钥)	
                    grant_type:"authorization_code",  //默认authorization_code
                    js_code: res.code    //wx.login登录获取的code值
                },
                success(res) {
                    _this.globalData.openid=res.data.openid;			   
                }
                })
            } else {
                console.log('登录失败！' + res.errMsg)
            } */
        
        }
    })
    console.log(_this.globalData.openId)
}
}
</script>

<style scoped>
    label.test::before{
        content:'*';
        color : red
    }
</style>