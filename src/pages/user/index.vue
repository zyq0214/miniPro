<template>
  <div>
      <div class="weui-cells weui-cells_form">
        <div class="weui-cell weui-cell_active weui-cell_select weui-cell_select-after">
          <div class="weui-cell__hd"><label class="weui-label">冷藏支持</label></div>
            <div class="weui-cell__bd weui-flex" @click="showSelector">
            <span class="weui-select">{{province+" "+city+" "+district}}</span>
          </div>
        </div>
      </div>
<!--     <button @click="showSelector">选择省市区</button> -->
    <div>{{province+" "+city+" "+district }}</div>
    <region-selector :isShow="selectorShow"  @hideSelector="hideSelector"></region-selector>
  </div>
</template>

<script>
import regionSelector from '@/components/regionSelector';
export default {
    components:{
        regionSelector,
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
        }
    }
}
</script>

<style scoped>

</style>