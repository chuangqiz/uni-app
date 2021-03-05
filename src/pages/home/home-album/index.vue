<template>
  <view>
    <!-- 轮播图开始 -->
    <view class="album_swiper">
      <swiper
        indicator-dots
        autoplay
        circular
      >
        <swiper-item
          v-for="item in banner"
          :key="item.id"
        >
          <image :src="item.thumb"></image>
        </swiper-item>
      </swiper>
    </view>
    <!-- 轮播图结束 -->
    <!-- 列表开始 -->
    <view class="album_list">
      <view class="album_item"
        v-for="item in album"
        :key="item.id"
      >
        <view class="album_img">
          <image :src="item.cover" mode="widthFix"></image>
        </view>
        <view class="album_info">
          <view class="album_name">{{ item.name }}</view>
          <view class="album_desc">{{ item.desc }}</view>
          <view class="album_btn">
            <view class="album_attention">关注</view>
          </view>
        </view>
      </view>
    </view>
    <!-- 列表结束 -->
  </view>
</template>

<script>
export default {
  data () {
    return {
      params: {
        limit: 30,
        order: 'new',
        skip: 0
      },
      banner: [],
      album: []
    }
  },
  mounted () {
    uni.setNavigationBarTitle({ title: "专辑" })
    this.getList()
  },
  methods: {
    getList () {
      this.$api({
        url: 'http://service.picasso.adesk.com/v1/wallpaper/album',
        // 603f0ee5e7bce71a8ed5df09
        data: this.params
      }).then(result => {
        console.log(result)
        this.banner = result.res.banner
        this.album = result.res.album
      })
    }
  }
}
</script>

<style lang="scss">
  @import "./index.scss";
</style>