<template>
  <div >
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
            <div class="weui-cell__hd"><label class="weui-label">是否冷藏</label></div>
            <div class="weui-cell__bd weui-flex">
                <input 
                    class="weui-input" 
                    type="text" 
                    placeholder="待定" 
                    placeholder-class="weui-input__placeholder"
                />
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
        <div><button class="weui-btn_cell weui-btn_cell-primary">登记</button></div>
        </div>
      </div>
      <div :hidden="activeIndex != 1">
          <div class="weui-cells weui-cells_form">
        <div class="weui-cell weui-cell_active">
            <div class="weui-cell__hd"><label class="weui-label">是否冷藏</label></div>
            <div class="weui-cell__bd weui-flex">
                <input 
                    class="weui-input" 
                    type="text" 
                    placeholder="待定" 
                    placeholder-class="weui-input__placeholder"
                />
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
        <div><button class="weui-btn_cell weui-btn_cell-primary">search</button></div>
        </div>
      </div>
      <div :hidden="activeIndex != 2">
          <div class="weui-cells weui-cells_form">
        <div class="weui-cell weui-cell_active">
            <div class="weui-cell__hd"><label class="weui-label">是否冷藏</label></div>
            <div class="weui-cell__bd weui-flex">
                <input 
                    class="weui-input" 
                    type="text" 
                    placeholder="待定" 
                    placeholder-class="weui-input__placeholder"
                />
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
        <div><button class="weui-btn_cell weui-btn_cell-primary">search</button></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Swiper from "@/components/swiper";

export default {
  components: { Swiper },
  data() {
    return {
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
      tabs: [
        {
          name: "货物登记",
          type: "1",
          checked: true
        },
        {
          name: "货车匹配",
          type: "2",
          checked: true
        },
        {
          name: "货库匹配",
          type: "3",
          checked: true
        }
      ],
      activeIndex: 0,
    };
  },
  methods: {
      tabClick(e) {
      this.activeIndex = e.currentTarget.id;
    }
  },
  computed: {
      navbarSliderClass() {
      if (this.activeIndex == 0) {
        return "navbar_slider_0";
      }
      if (this.activeIndex == 1) {
        return "navbar_slider_1";
      }
      if (this.activeIndex == 2) {
        return "navbar_slider_2";
      }
    }
  }
};
</script>

<style>
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
  position: fixed;
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
  width: 6em;
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
  transform: translateX(240rpx);
}

.navbar_slider_2 {
  left: 29rpx;
  transform: translateX(480rpx);
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