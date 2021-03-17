<template>
  <div class="selector-container" :animation="animationData">
    <div class="main">
      <div class="btn-controler">
        <div class="cancel-btn" @click="hideSelector(null)">取消</div>
        <div class="confirm-btn" @click="confirm">确定</div>
      </div>
      <picker-view
        :value="selected"
        class="picker-container"
        indicator-style="height: 50px"
        @change="handleChange"
      >
        <picker-view-column class="picker-column">
          <view v-for="(item, index) in mapInfo" :key="index">{{ item.name }}</view>
        </picker-view-column>
        <picker-view-column class="picker-column">
          <view v-for="(item, index) in currentCites" :key="index">{{ item.name }}</view>
        </picker-view-column>
        <picker-view-column class="picker-column">
          <view v-for="(item, index) in currentDistricts" :key="index">{{ item.name }}</view>
        </picker-view-column>
      </picker-view>
    </div>
    <div class="layer" @click="hideSelector(null)"></div>
  </div>
</template>

<script>
import mapInfo from "../../mapInfo/mapInfo";

export default {
  data() {
    return {
      mapInfo: {},    //存放所有的省市区信息
      selectedProvince: 0,
      selectedCity: 0,
      selectedDistrict: 0,
      animationData: {}
    };
  },
  props: ['isShow', 'province', 'city', 'district'],
  computed: {
    currentCites() {
      let i = this.selectedProvince;
      return this.mapInfo[i].cities;
    },
    currentDistricts() {
      let i = this.selectedCity;
      return this.currentCites[i].districts;
    },
    selected() {
      return [this.selectedProvince, this.selectedCity, this.selectedDistrict];
    }
  },
  watch: {
    isShow(val) {
      if (val) {
        this.showSelector();
      } else {
        this.hideSelector();
      }
    }
  },
  methods: {
    initialize() {
      this.mapInfo = wx.getStorageSync("mapInfo").provinces;
    },
    handleChange(e) {
      let newIndex = e.mp.detail.value,
        currentIndex = this.selected;
      if (newIndex[0] !== currentIndex[0]) {
        this.selectedProvince = newIndex[0];
        this.selectedDistrict = this.selectedCity = 0;
        return;
      } else if (newIndex[1] !== currentIndex[1]) {
        this.selectedCity = newIndex[1];
        this.selectedDistrict = 0;
        return;
      } else if (newIndex[2] !== currentIndex[2]) {
        this.selectedDistrict = newIndex[2];
        return;
      }
    },
    confirm() {
      let province = this.mapInfo[this.selectedProvince],
          city = this.currentCites[this.selectedCity],
          district = this.currentDistricts[this.selectedDistrict];

      province.index = this.selectedProvince;
      city.index = this.selectedCity;
      district.index = this.selectedDistrict;

      let info = [province, city, district].map((item) => {
        let { id, name, index } = item;
        return { id, name, index };
      });
      this.hideSelector(info);
    },
    defaultSelected() {
      if (!this.province || !this.city || !this.district) return;
      let i, j, k, currentCites, currentDistricts;
      try {
        i = this.mapInfo.findIndex((pro) => pro.name === this.province);
        currentCites = this.mapInfo[i].cities;
        j = currentCites.findIndex((city) => city.name === this.city);
        currentDistricts = currentCites[j].districts;
        k = currentDistricts.findIndex((dis) => dis.name === this.district);
      } catch (e) {
        [this.selectedProvince, this.selectedCity, this.selectedDistrict] = [0, 0, 0];
        return;
      }

      [this.selectedProvince, this.selectedCity, this.selectedDistrict] = [i, j, k];
    },
    showSelector() {
      this.defaultSelected();
      this.startAnimation('0vh');
    },
    hideSelector(info) {
      this.$emit('hideSelector', info);
      this.startAnimation('110vh');
    },
    startAnimation(ins) {
      let data = wx.createAnimation({ duration: 300, timingFunction: 'ease' });
      data.translateY(ins).step();
      this.animationData = data.export();
    }
  },
  beforeCreate() {
    if (!wx.getStorageSync('mapInfo')) {
      wx.setStorageSync("mapInfo", mapInfo);
    }
  },
  created() {
    this.initialize();
  }
};

</script>

<style scoped>
.selector-container {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100vw;
  height: 100vh;
  z-index: 10;
  transform: translateY(100vh);
  -webkit-transform: translateY(100vh);
}
.main {
  position: absolute;
  width: 100vw;
  background-color: #ffffff;
  left: 0;
  bottom: 0;
  z-index: 20;
}
.layer {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.3);
  z-index: 1;
}
.btn-controler {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100vw;
  height: 50px;
  border-bottom: 0.5px solid #eeeeee;
}
.cancel-btn, .confirm-btn {
  padding: 0 20px;
  font-size: 15px;
  font-weight: bold;
}
.cancel-btn {
  color: #949494;
}
.confirm-btn {
  color: #19c66c;
}
.picker-container {
  width: 100vw;
  height: 250px;
  font-size: 12px;
}
.picker-column {
  line-height: 50px;
  text-align: center;
}
</style>
