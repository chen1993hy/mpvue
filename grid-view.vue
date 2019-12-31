<template>
  <div class="grid-view">
    <swiper :current="current_index" @change="bindSwiperChange">
      <swiper-item v-for="(item, index) in gridGroup" :key="index">
        <div class="flex-wrp" style="height:50%;" v-for="(itemchild, _index) in item" :key="_index">
          <div class="flex-clm flex-center child-item" :class="'child-item_'+column_lie"  v-for="(itemchild1, _index1) in itemchild" :key="_index1" :data-obj="itemchild1" @click="item_click">
            <img :src="itemchild1.pic" mode="scaleToFill" :class="'child-img_'+column_lie" />
            <div :class="'child-title_'+column_lie">{{ itemchild1.name }}</div>
          </div>
        </div>
      </swiper-item>
    </swiper>
    <div class="flex flex-center" style="width:100%;padding:4rpx 0">
      <div class="flex ">
        <div class="item-index" :class=" index==current_index?'item-index-select':'' " v-for="(item, index) in gridGroup" :key="index"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Array,
      default: []
    },
    column_lie: {
      type: [String, Number],
      default: 5
    }
  },
  data () {
    return {
      current_index: 0
    }
  },
  computed: {
    gridGroup () {
      let group = []
      let num = (this.data.length % this.column_lie) > 0 ? (parseInt(this.data.length / this.column_lie) + 1) : parseInt(this.data.length / this.column_lie)
      for (let i = 0; i < num; i += 2) {
        let arr = this.data.slice(this.column_lie * i, this.column_lie * (i + 1))
        let arr1 = this.data.slice(this.column_lie * (i + 1), this.column_lie * (i + 2))
        var arr2 = [arr, arr1]
        group.push(arr2)
      }
      return group
    }
  },
  methods: {
    item_click: function (event) {
      // console.log('item_click:', event)
      this.$emit('itemClick', event.currentTarget.dataset.obj)
    },
    bindSwiperChange: function (event) {
      // console.log('bindSwiperChange:', event)
      this.current_index = event.target.current
    }
  }
}
</script>

<style scoped>

.grid-view{
  background-color:#fff;
}

.child-item{
  border-radius:20upx;
}

.child-item:active{
  background-color:#f5f5f5;
}

.child-item_5{
  width:20%;
}

.child-img_5{
  width:82rpx;height:82rpx;
}

.child-title_5{
  font-size:24rpx;color:#3d3d3d;margin-top:10rpx;line-height:1;
}

.child-item_4{
  width:25%;
}

.child-img_4{
  width:85rpx;height:85rpx;
}

.child-title_4{
  font-size:24rpx;color:#3d3d3d;margin-top:10rpx;line-height:1;
}

.item-index{
  width:24rpx;height:4rpx;border-radius:20rpx;background-color:#e4e4e4;margin:0 8rpx 0 4rpx;
}

.item-index-select{
  background-color:#888;
}

</style>