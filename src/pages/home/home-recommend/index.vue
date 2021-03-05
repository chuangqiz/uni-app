<template>
  <scroll-view class="recommend_view" scroll-y @scrolltolower="handleToLower" v-if="recommends.length > 0">
    <!-- 推荐开始 -->
    <view class="recommend_wrapper">
      <view class="recommend_items"
        v-for="item in recommends"
        :key="item.id"
      >
        <image :src="item.thumb" mode="widthFix" />  
      </view>
    </view>
    <!-- 推荐结束 -->
    <!-- 月份开始 -->
    <view class="months_wrap">
      <view class="months_title">
        <view class="months_title_info">
          <view class="months_info">
            <text>{{ months.DD }} / </text>
            {{ months.MM }}月
          </view>
          <view class="months_text">{{ months.title }}</view>
        </view>
        <view class="months_title_more">更多 ></view>
      </view>
      <view class="months_content">
        <view class="months_item"
          v-for="item in months.items"
          :key="item.id"
        >
          <image :src="item.thumb + item.rule.replace('$<Height>',360)" mode="aspectFill" />
        </view>
      </view>
    </view>
    <!-- 月份结束 -->
    <!-- 热门开始 -->
    <view class="hots_wrapper">
      <view class="hots_title">热门</view>
      <view class="hots_content">
        <view
          class="hots_items"
          v-for="item in hots"
          :key="item.id"
        >
          <image :src="item.thumb" mode="widthFix" />
        </view>
      </view>
    </view>
    <!-- 热门结束 -->
  </scroll-view>
</template>

<script>
import moment from "moment";
export default {
  data () {
    return {
      recommends: [],
      months: {},
      hots: [],
      params: {
        // 要获取几条
        limit: 30,
        // 关键词
        order: 'hot',
        // 要跳过多少条
        skip: 0
      },
      load: true
    }
  },
  mounted () {
    uni.setNavigationBarTitle({ title: "推荐" })
    this.getList()
  },
  methods: {
    getList () {
      this.$api({
        url: 'http://service.picasso.adesk.com/v3/homepage/vertical',
        data: this.params
      }).then(result => {
        if (result.res.vertical.length === 0) {
          this.load = false
          return
        }
        if (this.recommends.length === 0) {
          this.recommends = result.res.homepage[1].items
          this.months = result.res.homepage[2]
          this.months.MM = moment(this.months.stime).format('MM')
          this.months.DD = moment(this.months.stime).format('DD')
        }
        this.hots = [...this.hots, ...result.res.vertical]
      })
    },
    handleToLower() {
      if (this.load) {
        this.params.skip += this.params.limit
        this.getList()
      } else {
        uni.showToast({
          title: '没有数据可加载',
          icon: 'none'
        })
      }
    }
  }
}
</script>

<style lang="scss">
  @import "./index.scss";
</style>