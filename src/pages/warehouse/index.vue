<template>
  <div>
    <Swiper :images="images" />
    <div class="navbar">
      <block v-for="(item,index) in tabs" :key="index">
        <div :id="index" :class="{'navbar_item_on':activeIndex == index}" class="navbar_item" @click="tabClick">
          <div class="navbar_title">{{item.name}}</div>
        </div>
      </block>
      <div class="navbar_slider" :class="navbarSliderClass"></div>
    </div>
    <div style="margin-top:50px">
      <div :hidden="activeIndex != 0">
        <div class="weui-cells weui-cells_form">
          <div class="weui-cell weui-cell_active">
            <div class="weui-cell__hd"><label class="weui-label">仓库名称</label></div>
            <div class="weui-cell__bd weui-flex">
                <input 
                    class="weui-input" 
                    type="text" 
                    placeholder="请输入仓库名称" 
                    placeholder-class="weui-input__placeholder"
                />
            </div>
          </div>
          <div>
            <div class="weui-cells weui-cells_form">
              <div class="weui-cell weui-cell_active weui-cell_select weui-cell_select-after">
                <div class="weui-cell__hd"><label class="weui-label">地区</label></div>
                  <div class="weui-cell__bd weui-flex" @click="showSelector">
                  <span class="weui-select">{{province+" "+city+" "+district}}</span>
                </div>
              </div>
            </div>
            <region-selector :isShow="selectorShow"  @hideSelector="hideSelector"></region-selector>
          </div>
          <div class="weui-cell weui-cell_active">
            <div class="weui-cell__hd"><label class="weui-label">可租面积</label></div>
            <div class="weui-cell__bd weui-flex">
                <input 
                    class="weui-input" 
                    type="text" 
                    placeholder="请输入仓库可租面积（/㎡）" 
                    placeholder-class="weui-input__placeholder"
                />
            </div>
          </div>
          <div class="weui-cell weui-cell_active">
            <div class="weui-cell__hd"><label class="weui-label">联系人</label></div>
            <div class="weui-cell__bd weui-flex">
                <input 
                    class="weui-input" 
                    type="text" 
                    placeholder="请输入联系人姓名" 
                    placeholder-class="weui-input__placeholder"
                />
            </div>
          </div>
          <div class="weui-cell weui-cell_active">
            <div class="weui-cell__hd"><label class="weui-label">联系方式</label></div>
            <div class="weui-cell__bd weui-flex">
                <input 
                    class="weui-input" 
                    type="text" 
                    placeholder="请输入联系方式" 
                    placeholder-class="weui-input__placeholder"
                />
            </div>
          </div>
          <div class="weui-cell weui-cell_active weui-cell_select weui-cell_select-after">
          <div class="weui-cell__hd"><label class="weui-label">冷藏支持</label></div>
          <div class="weui-cell__bd weui-flex">
            <picker mode="selector" @change="selectorChange" :range="array0">
              <span class="weui-select">{{array0[index]}}</span>
            </picker>
          </div>
        </div>
          <div><button class="weui-btn_cell weui-btn_cell-primary" @click="handleClick">登记</button></div>
        </div>
      </div>
      <div :hidden="activeIndex != 1">
        <div class="weui-cells weui-cells_form">
          <div class="weui-cell weui-cell_active">
            <div class="weui-cell__hd"><label class="weui-label">区域</label></div>
            <div class="weui-cell__bd weui-flex">
                <input 
                    class="weui-input" 
                    type="text" 
                    placeholder="请输入期望城市" 
                    placeholder-class="weui-input__placeholder"
                />
            </div>
          </div>
          <div class="weui-cell weui-cell_active">
            <div class="weui-cell__hd"><label class="weui-label">货物体量</label></div>
            <div class="weui-cell__bd weui-flex">
                <input 
                    class="weui-input" 
                    type="text" 
                    placeholder="请输入货物体量（m³）" 
                    placeholder-class="weui-input__placeholder"
                />
            </div>
          </div>
          <div class="weui-cell weui-cell_active weui-cell_select weui-cell_select-after">
            <div class="weui-cell__hd"><label class="weui-label">冷藏支持</label></div>
            <div class="weui-cell__bd weui-flex">
            <picker mode="selector" @change="selectorChange1" :range="array1">
              <span class="weui-select">{{array1[index1]}}</span>
            </picker>
          </div>
          </div>
          <div class="weui-cell weui-cell_active">
            <div class="weui-cell__hd"><label class="weui-label">持卡人</label></div>
            <div class="weui-cell__bd weui-flex">
                <input 
                    class="weui-input" 
                    type="text" 
                    placeholder="请输入持卡人姓名" 
                    placeholder-class="weui-input__placeholder"
                />
            </div>
          </div>
          <div><button class="weui-btn_cell weui-btn_cell-primary" @click="handleSearch">查询</button></div>
        </div>
      </div>
      <div style="background-color:#6aaebe;margin-top:30px;">
        <div style="font-size:30px;text-align:center">在租仓库展示</div>
        <div class="weui-cells weui-cells_after-title">
          <div class="weui-cell">
            <div class="weui-cell__bd">标题文字</div>
            <div class="weui-cell__ft">说明文字</div>
          </div>
          <div class="weui-cell">
            <div class="weui-cell__bd">标题文字</div>
            <div class="weui-cell__ft">说明文字</div>
          </div>
          <div class="weui-cell">
            <div class="weui-cell__bd">标题文字</div>
            <div class="weui-cell__ft">说明文字</div>
          </div>
          <div class="weui-cell" >
            <img src="/static/images/qq.png" style="width:80px;height:80px" @click="previewImg(index)">
            <img src="/static/images/qq.png" style="width:80px;height:80px">
            <img src="/static/images/qq.png" style="width:80px;height:80px">
            <img src="/static/images/qq.png" style="width:80px;height:80px">
          </div>
        </div>
        <div class="weui-cells weui-cells_after-title">
          <div class="weui-cell">
            <div class="weui-cell__bd">标题文字</div>
            <div class="weui-cell__ft">说明文字</div>
          </div>
        </div>
        <div class="weui-cells weui-cells_after-title">
          <div class="weui-cell">
            <div class="weui-cell__bd">标题文字</div>
            <div class="weui-cell__ft">说明文字</div>
          </div>
        </div>
        <div class="weui-cells weui-cells_after-title">
          <div class="weui-cell">
            <div class="weui-cell__bd">标题文字</div>
            <div class="weui-cell__ft">说明文字</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import Swiper from "@/components/swiper";
import regionSelector from '@/components/regionSelector';

export default {
  components: { Swiper,regionSelector },
  data(){
    return {
      selectorShow:false,
      province:"北京市",
      city:"北京市",
      district:"东城区",
      index:0,
      array0:['仓库支持冷藏','仓库不支持冷藏'],
      index1:0,
      array1:['仓库支持冷藏','仓库不支持冷藏'],
      images: [
      {
        url:
          "/static/images/green.png"
      },
      {
        url:
          "/static/images/pink.png"
      },
      {
        url:
          "/static/images/white.png"
      },
      {
        url:
          "/static/images/blue.png"
      }
    ],
    im:['/static/images/green.png','/static/images/qq.png','/static/images/qq.png','/static/images/qq.png'],
      tabs: [
        {
          name: "仓库登记",
          type: "1",
          checked: true
        },
        {
          name: "库货匹配",
          type: "2",
          checked: true
        }
      ],
      activeIndex: 0,
    }
  },
  mounted(){
    this.globalData.openId = "hah"
    console.log(this.globalData.openId)
  },
  methods:{
    tabClick(e) {
      this.activeIndex = e.currentTarget.id;
    },
    selectorChange(e){
      this.index=e.target.value
    },
    selectorChange1(e){
      this.index1=e.target.value
    },
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
    handleClick(){
      mpvue.navigateTo({url: '/pages/successPage/main'})
    },
    handleSearch(){
      mpvue.navigateTo({url: '/pages/searchResult/main'})
    },
    previewImg(index){
      let that = this;
      wx.previewImage({
        current:that.im[1],
        urls:that.im
      });
      console.log(index)
    },
  },
  onPullDownRefresh () {
      console.log('下拉刷新')
  },
  onReachBottom () {
      console.log('触底了')
  },
  computed: {
      navbarSliderClass() {
      if (this.activeIndex == 0) {
        return "navbar_slider_0";
      }
      if (this.activeIndex == 1) {
        return "navbar_slider_1";
      }
    }
  }
}
</script>

<style scoped>
.message {
  color: red;
  padding: 10px;
  text-align: center;
}
.content {
  box-sizing: border-box;
  height: 100%;
  padding-top: 50px;
  /* overflow: auto; */
  -webkit-overflow-scrolling: touch;
}

.swiper-item {
  height: 100%;
  text-align: center;
}

.navbar {
  display: -webkit-box;
  display: -webkit-flex;
  display: flex;
  position: absolute;
  z-index: 500;
  height: 50px;
  width: 100%;
  background-color: #298de5;
  border-bottom: 1rpx solid #ccc;
}

.navbar_item {
  position: relative;
  display: block;
  -webkit-box-flex: 1;
  -webkit-flex: 1;
  flex: 1;
  padding: 13px 0;
  text-align: center;
  font-size: 0;
}

.navbar_item .navbar_item_on {
  color: white;
}

.navbar_title {
  color: white;
  font-weight: 500;
  display: inline-block;
  font-size: 15px;
  max-width: 8em;
  width: auto;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  word-wrap: normal;
}

.navbar_slider {
  position: absolute;
  content: " ";
  left: 0;
  bottom: 0;
  width: 45%;
  height: 3px;
  background-color: white;
  -webkit-transition: -webkit-transform 0.1s;
  transition: -webkit-transform 0.1s;
  transition: transform 0.1s;
  transition: transform 0.1s, -webkit-transform 0.1s;
}

.navbar_slider_0 {
  left: 29rpx;
  transform: translateX(0);
}

.navbar_slider_1 {
  left: 29rpx;
  transform: translateX(350rpx);
}

.controls {
  display: -webkit-box;
  display: -webkit-flex;
  display: flex;
  position: fixed;
  z-index: 8888;
  top: 80;
  height: 50px;
  width: 100%;
  background-color: #298de5;
}
</style>