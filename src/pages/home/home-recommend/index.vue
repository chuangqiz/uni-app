<template>
  <view>
    <view class="recommend_wrapper">
      <view class="recommend_items"
        v-for="item in items"
        :key="item.id"
      >
        <image :src="item.thumb" />  
      </view>
    </view>
  </view>
</template>

<script>
export default {
  mounted () {
    this.$api({
      url: 'http://service.picasso.adesk.com/v3/homepage/vertical',
      data: {
        // 要获取几条
        limit: 30,
        // 关键词
        order: 'hot',
        // 要跳过多少条
        skip: 0
      }
    }).then(result => {
      console.log(result)
      this.items = result.res.homepage[1].items
    })
  },
  data () {
    return {
      items: []
    }
  }
}
</script>

<style>

</style>